# Exercise 14: Quiz Application
Create three classes:
- `Question` class: questionText, correctAnswer, options[4]
- `Quiz` class: array of Questions, quizTitle
- `Student` class: name, score
- Implement methods to: add questions, take quiz, calculate score, display results
- Create a quiz with 10 questions and simulate 5 students taking it

**Solution:**
<details> <summary>Solution</summary>

```cpp
#include <iostream>
#include <string>
using namespace std;

class Question {
private:
    string questionText;
    string options[4];
    int correctAnswer;  // 0-3 index

public:
    // Constructor
    Question(string q = "", string opt1 = "", string opt2 = "", 
             string opt3 = "", string opt4 = "", int correct = 0) {
        questionText = q;
        options[0] = opt1;
        options[1] = opt2;
        options[2] = opt3;
        options[3] = opt4;
        correctAnswer = correct;
    }

    // Display question
    void display() {
        cout << questionText << endl;
        for (int i = 0; i < 4; i++) {
            cout << (i + 1) << ". " << options[i] << endl;
        }
    }

    // Check if answer is correct
    bool checkAnswer(int answer) {
        return (answer - 1) == correctAnswer;
    }

    // Getter for correct answer
    int getCorrectAnswer() {
        return correctAnswer + 1;  // Return 1-based index
    }
};

class Quiz {
private:
    Question questions[10];
    int questionCount;
    string quizTitle;

public:
    // Constructor
    Quiz(string title) {
        quizTitle = title;
        questionCount = 0;
    }

    // Add question
    void addQuestion(string q, string opt1, string opt2, 
                     string opt3, string opt4, int correct) {
        if (questionCount < 10) {
            questions[questionCount] = Question(q, opt1, opt2, opt3, opt4, correct);
            questionCount++;
        }
    }

    // Get question count
    int getQuestionCount() {
        return questionCount;
    }

    // Take quiz
    int takeQuiz() {
        int score = 0;
        cout << "\n========== " << quizTitle << " ==========" << endl;
        cout << "Answer the following questions (enter 1-4):\n" << endl;

        for (int i = 0; i < questionCount; i++) {
            cout << "Question " << (i + 1) << ":" << endl;
            questions[i].display();
            cout << "Your answer: ";
            
            int answer;
            cin >> answer;

            if (questions[i].checkAnswer(answer)) {
                cout << "Correct!" << endl;
                score++;
            } else {
                cout << "Wrong! Correct answer was: " 
                     << questions[i].getCorrectAnswer() << endl;
            }
            cout << endl;
        }

        return score;
    }

    // Get quiz title
    string getTitle() {
        return quizTitle;
    }
};

class StudentQuiz {
private:
    string name;
    int score;
    int totalQuestions;

public:
    // Constructor
    StudentQuiz(string n = "", int s = 0, int total = 0) {
        name = n;
        score = s;
        totalQuestions = total;
    }

    // Calculate percentage
    double getPercentage() {
        if (totalQuestions == 0) return 0;
        return (score * 100.0) / totalQuestions;
    }

    // Display result
    void displayResult() {
        cout << name << " scored " << score << "/" << totalQuestions 
             << " (" << getPercentage() << "%)" << endl;
    }

    // Getters
    string getName() { return name; }
    int getScore() { return score; }
    double getPercent() { return getPercentage(); }
};

int main() {
    // Create quiz
    Quiz quiz("C++ Programming Quiz");

    // Add questions
    quiz.addQuestion(
        "What is the size of int data type in C++?",
        "2 bytes", "4 bytes", "8 bytes", "Depends on compiler",
        3  // Correct answer index (0-based)
    );

    quiz.addQuestion(
        "Which operator is used to access members of a class?",
        "->", ".", "::", "All of the above",
        3
    );

    quiz.addQuestion(
        "What is the default access specifier for class members?",
        "public", "private", "protected", "None",
        1
    );

    quiz.addQuestion(
        "Which keyword is used to define a class?",
        "class", "struct", "object", "define",
        0
    );

    quiz.addQuestion(
        "What is inheritance?",
        "Creating new class", "Deriving class from existing class", 
        "Hiding data", "None of the above",
        1
    );

    quiz.addQuestion(
        "Which of these is not a loop in C++?",
        "for", "while", "do-while", "repeat",
        3
    );

    quiz.addQuestion(
        "What is the correct syntax for constructor?",
        "ClassName()", "~ClassName()", "void ClassName()", "constructor ClassName()",
        0
    );

    quiz.addQuestion(
        "Which operator is used for dynamic memory allocation?",
        "malloc", "new", "alloc", "create",
        1
    );

    quiz.addQuestion(
        "What does OOP stand for?",
        "Object Oriented Programming", "Object Oriented Procedure",
        "Oriented Object Programming", "None of the above",
        0
    );

    quiz.addQuestion(
        "What is encapsulation?",
        "Hiding implementation", "Data binding", 
        "Both A and B", "None of the above",
        2
    );

    cout << "========== QUIZ SYSTEM ==========" << endl;
    cout << "Quiz created: " << quiz.getTitle() << endl;
    cout << "Total questions: " << quiz.getQuestionCount() << endl;

    // Simulate 5 students taking the quiz (manual input)
    StudentQuiz students[5];
    string studentNames[5] = {"Alice", "Bob", "Charlie", "Diana", "Eve"};

    cout << "\n========== STUDENTS TAKING QUIZ ==========" << endl;
    cout << "Note: In this simulation, enter answers for each student.\n" << endl;

    for (int i = 0; i < 5; i++) {
        cout << "\n***** Student: " << studentNames[i] << " *****" << endl;
        int score = quiz.takeQuiz();
        students[i] = StudentQuiz(studentNames[i], score, quiz.getQuestionCount());
        
        cout << "\n" << studentNames[i] << "'s Score: " 
             << score << "/" << quiz.getQuestionCount() << endl;
        cout << "Percentage: " << students[i].getPercentage() << "%" << endl;
    }

    // Display all results
    cout << "\n========== QUIZ RESULTS ==========" << endl;
    for (int i = 0; i < 5; i++) {
        students[i].displayResult();
    }

    // Find highest scorer
    int topIndex = 0;
    for (int i = 1; i < 5; i++) {
        if (students[i].getScore() > students[topIndex].getScore()) {
            topIndex = i;
        }
    }

    cout << "\n***** TOP SCORER *****" << endl;
    cout << "Congratulations to " << students[topIndex].getName() << "!" << endl;
    students[topIndex].displayResult();

    // Calculate class average
    double totalPercentage = 0;
    for (int i = 0; i < 5; i++) {
        totalPercentage += students[i].getPercent();
    }
    cout << "\nClass Average: " << (totalPercentage / 5) << "%" << endl;

    return 0;
}
```

</details>