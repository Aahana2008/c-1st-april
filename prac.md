# Q1.
#include <iostream>
using namespace std;

class Student {
protected:
    int roll_number;
    string name;
    float marks[5];

public:
    // Default Constructor
    Student() {
        roll_number = 0;
        name = "Unknown";
        for(int i = 0; i < 5; i++) marks[i] = 0;
    }

    // Parameterized Constructor (Full Info)
    Student(int r, string n, float m[]) {
        roll_number = r;
        name = n;
        for(int i = 0; i < 5; i++)
            marks[i] = m[i];
    }

    // Overloaded Constructor (Only Roll Number)
    Student(int r) {
        roll_number = r;
        name = "Not Assigned";
        for(int i = 0; i < 5; i++) marks[i] = 0;
    }

    // Destructor
    ~Student() {
        cout << "Destructor called for Roll No: " << roll_number << endl;
    }

    // Add Student
    void addStudent() {
        cout << "Enter Roll Number: ";
        cin >> roll_number;
        cout << "Enter Name: ";
        cin >> name;
        cout << "Enter Marks (5 subjects): ";
        for(int i = 0; i < 5; i++)
            cin >> marks[i];
    }

    // Modify Student
    void modifyStudent() {
        cout << "Modify Name: ";
        cin >> name;
        cout << "Modify Marks: ";
        for(int i = 0; i < 5; i++)
            cin >> marks[i];
    }

    // Display Student
    void displayStudent() {
        cout << "\nRoll Number: " << roll_number;
        cout << "\nName: " << name;
        cout << "\nMarks: ";
        for(int i = 0; i < 5; i++)
            cout << marks[i] << " ";
        cout << "\nAverage: " << calculateAverage() << endl;
    }

    // Calculate Average
    float calculateAverage() {
        float sum = 0;
        for(int i = 0; i < 5; i++)
            sum += marks[i];
        return sum / 5;
    }
};

class GraduateStudent : public Student {
private:
    string specialization;

public:
    void addGraduateStudent() {
        addStudent(); // Base class function
        cout << "Enter Specialization: ";
        cin >> specialization;
    }

    void displayGraduateStudent() {
        displayStudent();
        cout << "Specialization: " << specialization << endl;
    }
};
class StudentOperations {
public:
    // Overloaded addStudent methods
    void addStudent(Student &s) {
        s.addStudent();
    }

    void addStudent(Student &s, int r) {
        cout << "Adding student with Roll No only: " << r << endl;
    }
};
// MAIN FUNCTION
int main() {
    float marks[5] = {80, 85, 90, 75, 88};

    // Using Parameterized Constructor
    Student s1(1, "Amit", marks);
    s1.displayStudent();

    // Using Default Constructor
    Student s2;
    s2.addStudent();
    s2.displayStudent();

    // Using Overloaded Constructor
    Student s3(3);
    s3.displayStudent();

    // Using Inheritance
    GraduateStudent g1;
    g1.addGraduateStudent();
    g1.displayGraduateStudent();

    return 0;
}

# OUTPUT
  <img width="617" height="833" alt="image" src="https://github.com/user-attachments/assets/010a1e8d-0421-4ac7-a54d-2b962899e5d6" />

 # q2.
  #include <iostream>
using namespace std;

class Game {
private:
    char board[3][3];
    char turn;     // 'X' or 'O'
    char winner;

public:
    // Constructor
    Game() {
        resetGame();
    }

    // Reset Game
    void resetGame() {
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
        turn = 'X';
        winner = ' ';
    }

    // Print Board
    void printBoard() {
        cout << "\n";
        for(int i = 0; i < 3; i++) {
            cout << " ";
            for(int j = 0; j < 3; j++) {
                cout << board[i][j];
                if(j < 2) cout << " | ";
            }
            cout << "\n";
            if(i < 2) cout << "---|---|---\n";
        }
        cout << "\n";
    }

    // Make Move
    bool makeMove(int row, int col) {
        if(row < 0 || row > 2 || col < 0 || col > 2) {
            cout << "Invalid position!\n";
            return false;
        }

        if(board[row][col] != ' ') {
            cout << "Cell already occupied!\n";
            return false;
        }

        board[row][col] = turn;
        return true;
    }

    // Check Winner
    void checkWinner() {
        // Rows & Columns
        for(int i = 0; i < 3; i++) {
            if(board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ')
                winner = board[i][0];

            if(board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ')
                winner = board[0][i];
        }

        // Diagonals
        if(board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
            winner = board[0][0];

        if(board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')
            winner = board[0][2];
    }

    // Check Draw
    bool isDraw() {
        for(int i = 0; i < 3; i++)
            for(int j = 0; j < 3; j++)
                if(board[i][j] == ' ')
                    return false;

        return (winner == ' ');
    }

    // Switch Turn
    void switchTurn() {
        turn = (turn == 'X') ? 'O' : 'X';
    }

    // Get Winner
    char getWinner() {
        return winner;
    }

    // Get Turn
    char getTurn() {
        return turn;
    }
};
// main function 
int main() {
    Game game;
    int row, col;

    while(true) {
        game.printBoard();

        cout << "Player " << game.getTurn() << ", enter row and column (0-2): ";
        cin >> row >> col;

        if(game.makeMove(row, col)) {
            game.checkWinner();

            if(game.getWinner() != ' ') {
                game.printBoard();
                cout << "Player " << game.getWinner() << " wins!\n";
                break;
            }

            if(game.isDraw()) {
                game.printBoard();
                cout << "It's a draw!\n";
                break;
            }

            game.switchTurn();
        }
    }

    return 0;
}
# output
<img width="830" height="841" alt="image" src="https://github.com/user-attachments/assets/7623bd75-c1e3-4f75-a60b-90b52430b658" />

# Q3. 
#include <iostream>
#include <fstream>
using namespace std;

class Employee {
private:
    int employee_id;
    string name;
    float salary;

public:
    // Constructor
    Employee() {
        employee_id = 0;
        name = "";
        salary = 0;
    }

    // Input employee data
    void input() {
        cin >> employee_id >> name >> salary;
    }

    // Display employee data
    void display() {
        cout << employee_id << " " << name << " " << salary << endl;
    }

    // Calculate Salary (bonus + deduction)
    void calculateSalary() {
        float bonus = salary * 0.10;     // 10% bonus
        float deduction = salary * 0.05; // 5% deduction
        salary = salary + bonus - deduction;
    }

    // Write to file
    void writeToFile(ofstream &outFile) {
        outFile << employee_id << " " << name << " " << salary << endl;
    }

    // Read from file
    bool readFromFile(ifstream &inFile) {
        if(inFile >> employee_id >> name >> salary)
            return true;
        return false;
    }
};
// MAIN FUNCTION
int main() {
    ifstream inFile("employees.txt");
    ofstream outFile("updated_employees.txt");

    // Error handling
    if(!inFile) {
        cout << "Error: Input file not found!\n";
        return 1;
    }

    if(!outFile) {
        cout << "Error: Cannot create output file!\n";
        return 1;
    }

    Employee emp;

    cout << "Processing Employee Records...\n";

    // Read → Process → Write
    while(emp.readFromFile(inFile)) {
        emp.calculateSalary();
        emp.writeToFile(outFile);
    }

    cout << "Updated records saved to file.\n";

    inFile.close();
    outFile.close();

    return 0;
}

#  output 
<img width="1032" height="956" alt="image" src="https://github.com/user-attachments/assets/82135573-7898-4a91-97ac-976e097eb83b" />

### updated

<img width="613" height="285" alt="image" src="https://github.com/user-attachments/assets/283f693b-3ce9-4d3f-a836-7ec08e85fb66" />


