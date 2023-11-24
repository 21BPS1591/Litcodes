#include <iostream>
#include <sstream>
#include <stack>

class CustomStack {
private:
    std::string text;
    std::stack<std::pair<int, std::string>> operations;

public:
    void insert(const std::string& value) {
        text.insert(text.end(), value.begin(), value.end());
        operations.push({1, value});
    }

    void deleteChars(int value) {
        std::string deletedChars = text.substr(text.length() - value);
        text.resize(text.length() - value);
        operations.push({2, deletedChars});
    }

    char getChar(int index) {
        char result = text[index - 1];
        std::cout << result << std::endl;
        operations.push({3, std::string(1, result)});
        return result;
    }

    void undo() {
        if (!operations.empty()) {
            auto operation = operations.top();
            operations.pop();
            if (operation.first == 1) {
                text.resize(text.length() - operation.second.length());
            } else if (operation.first == 2) {
                text += operation.second;
            } else if (operation.first == 3) {
                // No need to undo get operation
            }
        }
    }
};

int main() {
    CustomStack editor;
    std::string input;
    std::getline(std::cin, input);
    std::stringstream ss(input);
    std::string command, value;
    
    while (std::getline(ss, command, ',')) {
        std::istringstream iss(command);
        iss >> command >> value;
        if (command == "1") {
            editor.insert(value);
        } else if (command == "3") {
            int intValue = std::stoi(value);
            editor.getChar(intValue);
        } else if (command == "2") {
            int intValue = std::stoi(value);
            editor.deleteChars(intValue);
        } else if (command == "4") {
            editor.undo();
        }
    }

    return 0;
}
