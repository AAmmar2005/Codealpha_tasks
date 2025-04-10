# Codealpha_tasks
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>

using namespace std;

void registerUser() {
    string username, password;

    cout << "Register User\n";
    cout << "Enter username: ";
    cin >> username;
    cout << "Enter password: ";
    cin >> password;

    // Create or open a file named "users.txt"
    ofstream userFile;
    userFile.open("users.txt", ios::app);
    
    // Write the username and password to the file
    userFile << username << " " << password << endl;

    userFile.close();
    cout << "User registered successfully!\n";
}

bool loginUser() {
    string username, password;
    string fileUsername, filePassword;

    cout << "Login\n";
    cout << "Enter username: ";
    cin >> username;
    cout << "Enter password: ";
    cin >> password;

    // Open the file to read user credentials
    ifstream userFile("users.txt");
    if (!userFile) {
        cerr << "Unable to open users.txt\n";
        return false;
    }

    // Check if the entered credentials match
    while (userFile >> fileUsername >> filePassword) {
        if (fileUsername == username && filePassword == password) {
            userFile.close();
            return true; // Successful login
        }
    }

    userFile.close();
    cout << "Invalid username or password.\n";
    return false; // Unsuccessful login
}

int main() {
    int choice;

    while (true) {
        cout << "1. Register\n";
        cout << "2. Login\n";
        cout << "3. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                registerUser();
                break;
            case 2:
                if (loginUser()) {
                    cout << "Login successful!\n";
                }
                break;
            case 3:
                cout << "Exiting the program...\n";
                exit(0);
            default:
                cout << "Invalid choice! Please select again.\n";
        }
    }

    return 0;
}       
