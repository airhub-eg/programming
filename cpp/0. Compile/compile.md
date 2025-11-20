# Compile a C++ File
![alt text](assets/image/Compilation-Process-in-C.png)
![alt text](assets/image/cpp_separate_compilation_03.svg)
### 1. Pre-processing
Generate preprocessed files (`.i`) for both source files:
```bash
g++ -Iinc -E lib/src/lib1.cpp -o build/Pre-processing/lib1.i
g++ -Iinc -E main.cpp -o build/Pre-processing/main.i
```
- `-Iinc`: Adds the `inc` directory to the include path
- `-E`: Stops after pre-processing
- Output: Expanded source code with headers included

### 2. Compilation
Generate assembly files (`.s`) from preprocessed files:
```bash
g++ -S build/Pre-processing/lib1.i -o build/Compilation/lib1.s
g++ -S build/Pre-processing/main.i -o build/Compilation/main.s
```
- `-S`: Compiles to assembly without assembling

### 3. Assembly
Generate object files (`.o`) from assembly:
```bash
g++ -c build/Compilation/lib1.s -o build/Assembly/lib1.o
g++ -c build/Compilation/main.s -o build/Assembly/main.o
```
- `-c`: Compiles/assembles without linking

### 4. Linking
Link object files into final executable:
```bash
g++ build/Assembly/main.o build/Assembly/lib1.o -o build/Linking/program
```
- Combines all object files into executable `program`

---

### Alternative Single-Command Approach
For practical use, you can combine all steps:
```bash
g++ -Iinc lib/src/lib1.cpp main.cpp -o build/Linking/program
```

### Verification
Test the executable:
```bash
./build/Linking/program
```

### Directory Structure After Compilation
```
build/
  Assembly/
    ib1.o
    main.o
  Compilation/
    lib1.s
    main.s
  Linking/
    program
  Pre-processing/
    lib1.i
    main.i
lib/
  inc/
    lib1.h
  src/
    lib1.cpp
main.cpp
```