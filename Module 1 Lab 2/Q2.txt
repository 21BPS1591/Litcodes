#include <iostream>
#include <stack>
#include <sstream>
#include <string>

class CustomQueue {
private:
    std::stack<int> inputStack;
    std::stack<int> outputStack;

public:
    void enqueue(int x) {
        inputStack.push(x);
    }

    void dequeue() {
        if (outputStack.empty()) {
            // Transfer elements from input stack to output stack
            while (!inputStack.empty()) {
                outputStack.push(inputStack.top());
                inputStack.pop();
            }
        }
        if (!outputStack.empty()) {
            outputStack.pop();
        }
    }

    int front() {
        if (outputStack.empty()) {
            // Transfer elements from input stack to output stack
            while (!inputStack.empty()) {
                outputStack.push(inputStack.top());
                inputStack.pop();
            }
        }
        if (!outputStack.empty()) {
            return outputStack.top();
        }
        return -1; // Return -1 if the queue is empty
    }
};

int main() {
    CustomQueue queue;
    std::string input;
    std::getline(std::cin, input);
    std::istringstream iss(input);
    std::string query;
    while (std::getline(iss, query, ',')) {
        int type = query[0] - '0';
        if (type == 1) {
            // Enqueue operation
            int value = std::stoi(query.substr(2));
            queue.enqueue(value);
        } else if (type == 2) {
            // Dequeue operation
            queue.dequeue();
        } else if (type == 3) {
            // Print Front operation
            int frontValue = queue.front();
            std::cout << frontValue << std::endl;
        }
    }
    return 0;
}
