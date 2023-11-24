#include <iostream>
#include <vector>

bool isValid(std::vector<std::vector<char>>& board, int row, int col, char num) {
    for (int i = 0; i < 9; ++i) {
        if (board[row][i] == num || board[i][col] == num || board[row - row % 3 + i / 3][col - col % 3 + i % 3] == num) {
            return false;
        }
    }
    return true;
}

bool solveSudoku(std::vector<std::vector<char>>& board) {
    for (int row = 0; row < 9; ++row) {
        for (int col = 0; col < 9; ++col) {
            if (board[row][col] == '.') {
                for (char num = '1'; num <= '9'; ++num) {
                    if (isValid(board, row, col, num)) {
                        board[row][col] = num;
                        if (solveSudoku(board)) {
                            return true;
                        } else {
                            board[row][col] = '.';
                        }
                    }
                }
                return false;
            }
        }
    }
    return true; 
}

int main() {
    int size;
    std::cin >> size;
    std::vector<std::vector<char>> board(size, std::vector<char>(size));
    for (int i = 0; i < size; ++i) {
        for (int j = 0; j < size; ++j) {
            std::cin >> board[i][j];
        }
    }

    if (solveSudoku(board)) {
        std::cout << "YES" << std::endl;
    } else {
        std::cout << "NO" << std::endl;
    }

    return 0;
}
