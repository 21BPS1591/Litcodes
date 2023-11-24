#include <iostream>
#include <vector>
#include <functional>

using namespace std;

bool isBipartite(vector<vector<int>>& graph) {
    int n = graph.size();
    vector<int> color(n, -1);

    std::function<bool(int, int)> dfs = [&](int u, int c) {
        color[u] = c;
        for (int v : graph[u]) {
            if (color[v] == -1) {
                if (!dfs(v, c ^ 1)) return false;
            } else if (color[v] == c) {
                return false;
            }
        }
        return true;
    };

    for (int i = 0; i < n; ++i) {
        if (color[i] == -1 && !dfs(i, 0)) return false;
    }

    return true;
}

int main() {
    int n;
    cin >> n;
    vector<vector<int>> graph(n);
    for (int i = 0; i < n; ++i) {
        int u;
        while (cin >> u) {
            graph[i].push_back(u);
            if (cin.get() == '\n') break;
        }
    }

    cout << (isBipartite(graph) ? "true" : "false") << endl;

    return 0;
}