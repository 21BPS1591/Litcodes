#include <iostream>
#include <vector>

using namespace std;

int countServers(vector<vector<int>>& matrix) {
    if (matrix.empty() || matrix[0].empty()) {
        return 0;
    }

    int m = matrix.size();
    int n = matrix[0].size();
    vector<int> rowCounts(m, 0);
    vector<int> colCounts(n, 0);
    int totalServers = 0;

    // Count servers in each row and column
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            if (matrix[i][j] == 1) {
                rowCounts[i]++;
                colCounts[j]++;
                totalServers++;
            }
        }
    }

    // Count servers that communicate with at least one other server
    int communicatingServers = 0;
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            if (matrix[i][j] == 1 && (rowCounts[i] > 1 || colCounts[j] > 1)) {
                communicatingServers++;
            }
        }
    }

    return communicatingServers;
}

int main() {
    // Accept input from the user
    int m, n;
    cin >> m;
    n = m;

    vector<vector<int>> matrix(m, vector<int>(n, 0));

    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            cin >> matrix[i][j];
        }
    }

    // Call the countServers function
    int result = countServers(matrix);

    // Display the result
    cout << result << endl;

    return 0;
}