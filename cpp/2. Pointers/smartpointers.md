# Smart Pointers in C++

Smart pointers are one of the most significant additions to modern C++ (C++11 and later). They provide automatic memory management through RAII (Resource Acquisition Is Initialization), eliminating most memory leaks and dangling pointer issues that plague raw pointer usage.

## The Problem with Raw Pointers

Before diving into smart pointers, let's understand what problems they solve:

```cpp
void problematicFunction() {
    int* ptr = new int(42);
    
    // Problem 1: What if an exception is thrown here?
    if (someCondition) {
        throw std::runtime_error("Error!");
        // Memory leak! delete never called
    }
    
    // Problem 2: Multiple return paths
    if (anotherCondition) {
        return;  // Memory leak again!
    }
    
    delete ptr;  // Only reached in "happy path"
}

// Problem 3: Ownership ambiguity
int* getData() {
    return new int(42);
    // Who is responsible for deleting this?
}

// Problem 4: Double deletion
int* ptr = new int(42);
int* ptr2 = ptr;
delete ptr;
delete ptr2;  // CRASH! Double deletion
```

Smart pointers solve all these problems through automatic lifetime management.

## RAII Principle

Smart pointers leverage RAII, a fundamental C++ idiom:
- **Resource Acquisition Is Initialization**: Resources are acquired in the constructor
- **Automatic cleanup**: Resources are released in the destructor
- **Exception safety**: Destructors are called even when exceptions occur

```cpp
{
    std::unique_ptr<int> ptr(new int(42));
    // Use ptr...
} // Destructor automatically called, memory freed
```

## std::unique_ptr

`unique_ptr` represents exclusive ownership of a dynamically allocated object. Only one `unique_ptr` can own a resource at a time.

### Basic Usage

```cpp
#include <memory>
#include <iostream>

// Construction
std::unique_ptr<int> ptr1(new int(42));

// Preferred: make_unique (C++14)
auto ptr2 = std::make_unique<int>(100);

// Array support
auto arr = std::make_unique<int[]>(10);
arr[0] = 5;
arr[9] = 50;
```

**Why prefer `make_unique`?**
- Exception safe
- More concise and readable
- Slightly more efficient (single allocation in some cases)
- Prevents issues like: `func(std::unique_ptr<T>(new T), std::unique_ptr<U>(new U))` where evaluation order could cause leaks

### Accessing the Managed Object

```cpp
auto ptr = std::make_unique<int>(42);

// Dereference
std::cout << *ptr;  // 42

// Arrow operator for member access
struct Person {
    std::string name;
    void greet() { std::cout << "Hello, " << name; }
};

auto person = std::make_unique<Person>();
person->name = "Alice";
person->greet();

// Get raw pointer (doesn't transfer ownership)
int* rawPtr = ptr.get();

// Check if it owns an object
if (ptr) {
    std::cout << "ptr owns an object";
}
// Or explicitly:
if (ptr != nullptr) {
    // ...
}
```

### Transferring Ownership

`unique_ptr` cannot be copied (ownership is unique), but it can be moved:

```cpp
auto ptr1 = std::make_unique<int>(42);

// This won't compile:
// auto ptr2 = ptr1;  // ERROR: copy constructor deleted

// Move ownership
auto ptr2 = std::move(ptr1);
// Now ptr1 is null, ptr2 owns the object

if (ptr1 == nullptr) {
    std::cout << "ptr1 no longer owns the object\n";
}
std::cout << *ptr2;  // 42
```

### Returning unique_ptr from Functions

```cpp
// Factory pattern - caller receives ownership
std::unique_ptr<Widget> createWidget(int id) {
    auto widget = std::make_unique<Widget>();
    widget->initialize(id);
    return widget;  // Move semantics, no explicit std::move needed
}

auto myWidget = createWidget(123);
// myWidget owns the object
```

The compiler automatically applies move semantics when returning a local `unique_ptr`, so you don't need `std::move` in the return statement.

### Passing unique_ptr to Functions

There are several ways to pass `unique_ptr`, each with different semantics:

```cpp
// 1. By value - transfers ownership (consumes the pointer)
void takeOwnership(std::unique_ptr<Widget> ptr) {
    // This function now owns the object
    ptr->doSomething();
}  // Object destroyed when function ends

auto widget = std::make_unique<Widget>();
takeOwnership(std::move(widget));  // Must explicitly move
// widget is now null


// 2. By const reference - observe without taking ownership
void observeWidget(const std::unique_ptr<Widget>& ptr) {
    if (ptr) {
        ptr->doSomething();
    }
}  // Caller still owns the object

auto widget = std::make_unique<Widget>();
observeWidget(widget);  // No move needed
// widget still valid


// 3. By non-const reference - allows modification/resetting
void maybeResetWidget(std::unique_ptr<Widget>& ptr) {
    if (someCondition) {
        ptr.reset(new Widget());  // Replace the object
    }
}


// 4. By raw pointer - most flexible for observation
void useWidget(Widget* ptr) {
    if (ptr) {
        ptr->doSomething();
    }
}

auto widget = std::make_unique<Widget>();
useWidget(widget.get());  // Pass raw pointer
```

**Guidelines:**
- Pass by value to transfer ownership
- Pass by `const&` if you need to check for null or re-seat
- Pass by raw pointer (`T*`) for simple observation (most common)
- Pass by non-const reference to allow modification of the `unique_ptr` itself

### Custom Deleters

Sometimes you need custom cleanup logic:

```cpp
// File handle example
struct FileCloser {
    void operator()(FILE* fp) {
        if (fp) {
            std::cout << "Closing file\n";
            fclose(fp);
        }
    }
};

std::unique_ptr<FILE, FileCloser> openFile(const char* filename) {
    FILE* fp = fopen(filename, "r");
    return std::unique_ptr<FILE, FileCloser>(fp);
}

// Lambda deleter
auto fileDeleter = [](FILE* fp) {
    if (fp) fclose(fp);
};

std::unique_ptr<FILE, decltype(fileDeleter)> file(
    fopen("data.txt", "r"), 
    fileDeleter
);

// Array with custom deleter
auto customArrayDeleter = [](int* arr) {
    std::cout << "Custom array deletion\n";
    delete[] arr;
};

std::unique_ptr<int[], decltype(customArrayDeleter)> arr(
    new int[10],
    customArrayDeleter
);
```

### Releasing Ownership

```cpp
auto ptr = std::make_unique<int>(42);

// Release ownership without deleting
int* rawPtr = ptr.release();
// ptr is now null, rawPtr points to the object
// You're now responsible for deletion!
delete rawPtr;

// Reset to a new object (deletes current)
ptr.reset(new int(100));

// Reset to null (deletes current)
ptr.reset();
// Or simply:
ptr = nullptr;
```

### unique_ptr with Arrays

```cpp
// Correct array syntax
auto arr1 = std::make_unique<int[]>(10);
arr1[0] = 5;

// Without make_unique:
std::unique_ptr<int[]> arr2(new int[10]);

// Note: operator[] is available for array version
for (int i = 0; i < 10; i++) {
    arr1[i] = i * 2;
}

// Array version uses delete[] automatically
```

**Important:** For single objects, use `unique_ptr<T>`. For arrays, use `unique_ptr<T[]>`. They have different deleters.

### Real-World Example: Pimpl Idiom

The "Pointer to Implementation" idiom uses `unique_ptr` to hide implementation details:

```cpp
// Widget.h
class Widget {
public:
    Widget();
    ~Widget();
    
    void doSomething();
    
private:
    class Impl;  // Forward declaration
    std::unique_ptr<Impl> pImpl;
};

// Widget.cpp
class Widget::Impl {
public:
    void doSomethingImpl() {
        // Complex implementation hidden from header
    }
    
private:
    // Private data members not visible in header
    std::vector<int> data;
    std::string config;
};

Widget::Widget() : pImpl(std::make_unique<Impl>()) {}

Widget::~Widget() = default;  // Must be in .cpp where Impl is complete

void Widget::doSomething() {
    pImpl->doSomethingImpl();
}
```

## std::shared_ptr

`shared_ptr` implements shared ownership through reference counting. Multiple `shared_ptr` instances can own the same object, and the object is destroyed when the last `shared_ptr` is destroyed.

### Basic Usage

```cpp
#include <memory>

// Create shared_ptr
std::shared_ptr<int> ptr1 = std::make_shared<int>(42);

// Preferred way - more efficient
auto ptr2 = std::make_shared<int>(100);

// Can copy (unlike unique_ptr)
auto ptr3 = ptr2;  // Both own the same object
std::cout << ptr2.use_count();  // 2

// All copies point to same object
*ptr2 = 200;
std::cout << *ptr3;  // 200
```

### Why Prefer make_shared?

```cpp
// Less efficient: two allocations
std::shared_ptr<Widget> ptr1(new Widget());
// 1. new Widget() - allocation for object
// 2. Control block allocation for reference count

// More efficient: single allocation
auto ptr2 = std::make_shared<Widget>();
// Single allocation contains both object and control block
```

`make_shared` is:
- More efficient (single allocation)
- Exception safe
- Cleaner syntax

**Caveat:** `make_shared` keeps memory alive until the last `weak_ptr` expires, not just the last `shared_ptr`.

### Reference Counting

```cpp
auto ptr1 = std::make_shared<int>(42);
std::cout << ptr1.use_count();  // 1

{
    auto ptr2 = ptr1;
    std::cout << ptr1.use_count();  // 2
    
    auto ptr3 = ptr1;
    std::cout << ptr1.use_count();  // 3
}  // ptr2 and ptr3 destroyed

std::cout << ptr1.use_count();  // 1
```

### Thread Safety

The reference count operations are thread-safe:

```cpp
std::shared_ptr<int> globalPtr = std::make_shared<int>(42);

void threadFunction() {
    auto localPtr = globalPtr;  // Thread-safe increment
    // Use localPtr...
}  // Thread-safe decrement

std::thread t1(threadFunction);
std::thread t2(threadFunction);
t1.join();
t2.join();
```

**Important distinction:**
- The reference count manipulation is thread-safe
- The pointed-to object is NOT automatically thread-safe
- Reading/writing `*ptr` requires separate synchronization

```cpp
std::shared_ptr<int> ptr = std::make_shared<int>(0);

// This is NOT thread-safe:
void unsafeIncrement() {
    (*ptr)++;  // Race condition!
}

// Need mutex for the data:
std::mutex mtx;
void safeIncrement() {
    std::lock_guard<std::mutex> lock(mtx);
    (*ptr)++;
}
```

### Passing shared_ptr to Functions

```cpp
// 1. By value - shares ownership (increments ref count)
void shareOwnership(std::shared_ptr<Widget> ptr) {
    // Both caller and function own the object
    ptr->doSomething();
}  // Ref count decremented

auto widget = std::make_shared<Widget>();
shareOwnership(widget);  // Copy made, ref count temporarily increases


// 2. By const reference - doesn't affect ref count
void observeWidget(const std::shared_ptr<Widget>& ptr) {
    if (ptr) {
        ptr->doSomething();
    }
}  // No ref count change

observeWidget(widget);  // More efficient, no copy


// 3. By raw pointer - best for simple use
void useWidget(Widget* ptr) {
    if (ptr) {
        ptr->doSomething();
    }
}

useWidget(widget.get());  // Most efficient
```

**Guidelines:**
- Pass by `const&` if you need to check for null or extend lifetime conditionally
- Pass by value if function needs to store a copy or extend lifetime unconditionally
- Pass by raw pointer for simple observation (most efficient)

### Aliasing Constructor

`shared_ptr` supports aliasing: pointing to one object while owning another:

```cpp
struct Person {
    std::string name;
    int age;
};

auto person = std::make_shared<Person>();
person->name = "Alice";
person->age = 30;

// Create shared_ptr to member, but shares ownership of person
std::shared_ptr<std::string> namePtr(person, &person->name);
std::shared_ptr<int> agePtr(person, &person->age);

// These keep person alive
person.reset();  // Original shared_ptr released
std::cout << *namePtr;  // Still valid! "Alice"
// Person object kept alive by namePtr and agePtr
```

### Converting Between Smart Pointers

```cpp
// unique_ptr to shared_ptr (OK - transfer ownership)
auto uniquePtr = std::make_unique<int>(42);
std::shared_ptr<int> sharedPtr = std::move(uniquePtr);
// uniquePtr is now null

// shared_ptr to unique_ptr (NOT directly possible)
// Because shared ownership can't become exclusive
// But you can do this if use_count() == 1:
std::shared_ptr<int> shared = std::make_shared<int>(42);
if (shared.use_count() == 1) {
    std::unique_ptr<int> unique(shared.release());  // Won't compile!
    // No release() method for shared_ptr
}
```

### Custom Deleters

```cpp
// Custom deleter with shared_ptr
auto deleter = [](int* ptr) {
    std::cout << "Custom deletion\n";
    delete ptr;
};

std::shared_ptr<int> ptr1(new int(42), deleter);

// Deleter type is NOT part of shared_ptr type
std::shared_ptr<int> ptr2 = ptr1;  // OK, same type

// Different from unique_ptr where deleter IS part of type
```

### Array Support (C++17 and later)

```cpp
// C++17: shared_ptr with array
std::shared_ptr<int[]> arr1(new int[10]);
arr1[0] = 5;

// C++20: make_shared for arrays
auto arr2 = std::make_shared<int[]>(10);

// Note: Before C++17, arrays with shared_ptr required custom deleter
std::shared_ptr<int> oldStyleArr(new int[10], [](int* p) { delete[] p; });
```

## std::weak_ptr

`weak_ptr` is a non-owning observer of an object managed by `shared_ptr`. It doesn't contribute to the reference count.

### The Circular Reference Problem

```cpp
struct Node {
    std::shared_ptr<Node> next;
    std::shared_ptr<Node> prev;  // Problem!
};

auto node1 = std::make_shared<Node>();
auto node2 = std::make_shared<Node>();

node1->next = node2;
node2->prev = node1;  // Circular reference!

// When node1 and node2 go out of scope:
// - node1's ref count is 1 (node2->prev holds it)
// - node2's ref count is 1 (node1->next holds it)
// Memory leak! Neither can be deleted
```

### Solution with weak_ptr

```cpp
struct Node {
    std::shared_ptr<Node> next;
    std::weak_ptr<Node> prev;  // Doesn't increment ref count
};

auto node1 = std::make_shared<Node>();
auto node2 = std::make_shared<Node>();

node1->next = node2;  // shared_ptr
node2->prev = node1;  // weak_ptr doesn't prevent deletion

// When node1 and node2 go out of scope:
// - node1's ref count is 1 (only node2->prev, but it's weak)
// - node2's ref count is 1 (only node1->next)
// Both are properly deleted!
```

### Basic Usage

```cpp
std::shared_ptr<int> shared = std::make_shared<int>(42);
std::weak_ptr<int> weak = shared;

std::cout << weak.use_count();  // 1 (same as shared)
std::cout << shared.use_count();  // 1 (weak doesn't count)

// Can't access directly
// std::cout << *weak;  // ERROR: no operator*

// Must convert to shared_ptr first
if (auto locked = weak.lock()) {
    std::cout << *locked;  // 42
} else {
    std::cout << "Object was deleted";
}
```

### Checking if Object Still Exists

```cpp
std::weak_ptr<int> weak;

{
    auto shared = std::make_shared<int>(42);
    weak = shared;
    
    std::cout << weak.expired();  // false
}  // shared destroyed here

std::cout << weak.expired();  // true

// Attempting to lock returns null
if (auto locked = weak.lock()) {
    // Won't execute
} else {
    std::cout << "Object no longer exists";
}
```

### Cache Implementation Example

`weak_ptr` is perfect for implementing caches:

```cpp
class ResourceCache {
private:
    std::map<std::string, std::weak_ptr<Resource>> cache;
    
public:
    std::shared_ptr<Resource> getResource(const std::string& id) {
        // Check if resource exists in cache
        auto it = cache.find(id);
        if (it != cache.end()) {
            // Try to lock the weak_ptr
            if (auto resource = it->second.lock()) {
                std::cout << "Cache hit\n";
                return resource;  // Return existing resource
            }
        }
        
        // Resource not in cache or was deleted
        std::cout << "Cache miss, loading resource\n";
        auto resource = std::make_shared<Resource>(id);
        cache[id] = resource;  // Store weak_ptr
        return resource;
    }
};

// Usage:
ResourceCache cache;

{
    auto res1 = cache.getResource("image.png");  // Cache miss
    auto res2 = cache.getResource("image.png");  // Cache hit
}  // res1 and res2 destroyed

auto res3 = cache.getResource("image.png");  // Cache miss (was deleted)
```

### Observer Pattern Implementation

```cpp
class Subject {
private:
    std::vector<std::weak_ptr<Observer>> observers;
    
public:
    void attach(std::shared_ptr<Observer> observer) {
        observers.push_back(observer);
    }
    
    void notify() {
        // Clean up expired observers while notifying
        auto it = observers.begin();
        while (it != observers.end()) {
            if (auto observer = it->lock()) {
                observer->update();
                ++it;
            } else {
                // Observer was deleted, remove from list
                it = observers.erase(it);
            }
        }
    }
};
```

## enable_shared_from_this

When you need a `shared_ptr` to `this` inside a member function:

### The Problem

```cpp
class Widget {
public:
    void doSomething() {
        // Want to pass 'this' as shared_ptr to async operation
        std::shared_ptr<Widget> ptr(this);  // WRONG! Double delete
        asyncOperation(ptr);
    }
};

auto widget = std::make_shared<Widget>();
widget->doSomething();  // Creates second control block, will crash!
```

### The Solution

```cpp
class Widget : public std::enable_shared_from_this<Widget> {
public:
    void doSomething() {
        // Correct way to get shared_ptr to this
        auto ptr = shared_from_this();
        asyncOperation(ptr);
    }
    
    void anotherMethod() {
        // Can also get weak_ptr
        std::weak_ptr<Widget> weak = weak_from_this();
        // ...
    }
};

// Must be managed by shared_ptr
auto widget = std::make_shared<Widget>();
widget->doSomething();  // Safe!

// WARNING: shared_from_this() only works if object is already
// owned by a shared_ptr. This will throw std::bad_weak_ptr:
Widget widget;
// widget.doSomething();  // WRONG! Not managed by shared_ptr
```

### Factory Method Pattern

```cpp
class Widget : public std::enable_shared_from_this<Widget> {
private:
    Widget() = default;  // Private constructor
    
public:
    // Factory method ensures object is always in shared_ptr
    static std::shared_ptr<Widget> create() {
        // Can't use make_shared with private constructor
        return std::shared_ptr<Widget>(new Widget());
    }
    
    void startAsyncWork() {
        auto self = shared_from_this();
        std::thread([self]() {
            // self keeps Widget alive during async work
            self->doWork();
        }).detach();
    }
    
private:
    void doWork() {
        std::cout << "Doing work safely\n";
    }
};

// Usage:
auto widget = Widget::create();
widget->startAsyncWork();
// Widget stays alive even if widget goes out of scope
```

## Performance Considerations

### unique_ptr Performance

```cpp
// unique_ptr has ZERO overhead compared to raw pointer
sizeof(std::unique_ptr<int>) == sizeof(int*)  // true (usually)

// No reference counting, no atomic operations
// As fast as raw pointer in optimized builds
```

### shared_ptr Performance

```cpp
// shared_ptr is larger due to control block pointer
sizeof(std::shared_ptr<int>) == 2 * sizeof(int*)  // true (usually)

// Reference count operations are atomic (thread-safe)
// Copying shared_ptr: atomic increment (expensive)
// Destroying shared_ptr: atomic decrement + possible deletion

// Benchmark comparison:
// Raw pointer assignment: ~1ns
// unique_ptr assignment: ~1ns
// shared_ptr copy: ~10-20ns (due to atomic operations)
```

### Optimization Tips

```cpp
// 1. Use make_shared (single allocation)
auto ptr1 = std::make_shared<Widget>();  // Better

// vs two allocations:
std::shared_ptr<Widget> ptr2(new Widget());  // Worse


// 2. Move instead of copy when possible
std::shared_ptr<int> ptr1 = std::make_shared<int>(42);
std::shared_ptr<int> ptr2 = std::move(ptr1);  // Fast, no ref count change


// 3. Pass by const reference to avoid ref count changes
void observe(const std::shared_ptr<Widget>& ptr);  // No copy


// 4. Use weak_ptr in caches and observers
// Avoids keeping objects alive unnecessarily


// 5. Prefer unique_ptr when exclusive ownership is sufficient
// Much cheaper than shared_ptr
```

## Common Pitfalls and Best Practices

### Pitfall 1: Creating Multiple Control Blocks

```cpp
// WRONG:
Widget* raw = new Widget();
std::shared_ptr<Widget> ptr1(raw);
std::shared_ptr<Widget> ptr2(raw);  // Creates SECOND control block!
// Double delete when both are destroyed

// CORRECT:
auto ptr1 = std::make_shared<Widget>();
auto ptr2 = ptr1;  // Shares control block
```

### Pitfall 2: Circular References

```cpp
// WRONG:
struct Node {
    std::shared_ptr<Node> parent;
    std::shared_ptr<Node> child;  // Memory leak!
};

// CORRECT:
struct Node {
    std::weak_ptr<Node> parent;  // Weak reference breaks cycle
    std::shared_ptr<Node> child;
};
```

### Pitfall 3: Deleting this Through shared_ptr

```cpp
class Widget : public std::enable_shared_from_this<Widget> {
public:
    void suicide() {
        auto ptr = shared_from_this();
        ptr.reset();  // Doesn't delete this immediately!
        // this is still valid here
        // Deleted when function returns and ptr is destroyed
    }
};
```

### Pitfall 4: Storing this in Member shared_ptr

```cpp
// WRONG:
class Widget {
    std::shared_ptr<Widget> self;  // Don't do this!
    
public:
    Widget() : self(this) {}  // Creates second control block
};

// CORRECT: Use enable_shared_from_this if you need this
```

### Summary

1. **Prefer `make_unique` and `make_shared`** over raw `new`
2. **Default to `unique_ptr`**, use `shared_ptr` only when you truly need shared ownership
3. **Use `weak_ptr` to break cycles** in data structures
4. **Never create `shared_ptr` from `this`** unless using `enable_shared_from_this`
5. **Pass smart pointers by:**
   - Value when transferring/sharing ownership
   - `const&` when checking for null or conditionally extending lifetime
   - Raw pointer for simple observation
6. **Don't create multiple control blocks** for the same object
7. **Be aware of thread safety**: control block is thread-safe, object is not
8. **Use `weak_ptr`** for caches, observers, and parent pointers
9. **Move instead of copy** when ownership transfer is clear
10. **Consider performance**: `shared_ptr` has overhead from atomic operations

## Example

Smart pointers in a real scenario:

```cpp
#include <memory>
#include <vector>
#include <string>
#include <iostream>

// Forward declarations
class Document;
class Editor;

// Observer interface
class DocumentObserver {
public:
    virtual ~DocumentObserver() = default;
    virtual void onDocumentChanged(const Document& doc) = 0;
};

// Document class with observers
class Document : public std::enable_shared_from_this<Document> {
private:
    std::string content;
    std::vector<std::weak_ptr<DocumentObserver>> observers;
    
public:
    void setContent(const std::string& newContent) {
        content = newContent;
        notifyObservers();
    }
    
    const std::string& getContent() const { return content; }
    
    void addObserver(std::shared_ptr<DocumentObserver> observer) {
        observers.push_back(observer);
    }
    
    void notifyObservers() {
        auto it = observers.begin();
        while (it != observers.end()) {
            if (auto observer = it->lock()) {
                observer->onDocumentChanged(*this);
                ++it;
            } else {
                it = observers.erase(it);  // Clean up dead observers
            }
        }
    }
    
    // Method that needs shared_ptr to this
    void saveAsync() {
        auto self = shared_from_this();
        std::thread([self]() {
            // self keeps document alive during async save
            std::cout << "Saving: " << self->content << "\n";
        }).detach();
    }
};

// Editor is an observer
class Editor : public DocumentObserver {
private:
    std::string name;
    std::weak_ptr<Document> document;  // Weak to avoid cycle
    
public:
    explicit Editor(const std::string& editorName) : name(editorName) {}
    
    void openDocument(std::shared_ptr<Document> doc) {
        document = doc;
        doc->addObserver(shared_from_this());
    }
    
    void onDocumentChanged(const Document& doc) override {
        std::cout << "Editor " << name << " notified: " 
                  << doc.getContent() << "\n";
    }
    
    void editDocument(const std::string& newContent) {
        if (auto doc = document.lock()) {
            doc->setContent(newContent);
        } else {
            std::cout << "Document no longer available\n";
        }
    }
};

// Factory for creating documents
class DocumentFactory {
private:
    std::map<std::string, std::weak_ptr<Document>> cache;
    
public:
    std::shared_ptr<Document> getDocument(const std::string& id) {
        auto it = cache.find(id);
        if (it != cache.end()) {
            if (auto doc = it->second.lock()) {
                return doc;  // Return cached document
            }
        }
        
        // Create new document
        auto doc = std::make_shared<Document>();
        cache[id] = doc;
        return doc;
    }
};

// Usage
int main() {
    DocumentFactory factory;
    
    auto doc = factory.getDocument("report.txt");
    
    {
        auto editor1 = std::make_shared<Editor>("Alice");
        auto editor2 = std::make_shared<Editor>("Bob");
        
        editor1->openDocument(doc);
        editor2->openDocument(doc);
        
        editor1->editDocument("Hello World");
        // Both editors notified
        
    }  // editor1 and editor2 destroyed, but doc still alive
    
    doc->setContent("Updated content");
    // No observers to notify (were cleaned up automatically)
    
    doc->saveAsync();
    // Document kept alive during async operation
    
    return 0;
}
```

