#include <iostream>

using namespace std;

const int MOD = 1000000007;
const int MAXN = 1000;

long long T[MAXN + 1][MAXN + 1];
long long B[MAXN + 1], G[MAXN + 1];

void init() {
    T[1][0] = 1;
    for (int j = 1; j <= MAXN; j++) {
        T[1][j] = T[1][j - 1];
        if (j >= 2) T[1][j] = (T[1][j] + T[1][j - 2]) % MOD;
        if (j >= 3) T[1][j] = (T[1][j] + T[1][j - 3]) % MOD;
        if (j >= 4) T[1][j] = (T[1][j] + T[1][j - 4]) % MOD;
    }
    for (int i = 2; i <= MAXN; i++) {
        for (int j = 1; j <= MAXN; j++) {
            T[i][j] = (T[i - 1][j] * T[1][j]) % MOD;
        }
    }
}

int main() {
    init();
    int n, m;
    cin >> n >> m;
    B[1] = 0;
    G[1] = 1;
    for (int j = 2; j <= m; j++) {
        B[j] = 0;
        for (int k = 1; k < j; k++) {
            B[j] = (B[j] + (T[n][j - k] * G[k]) % MOD) % MOD;
        }
        G[j] = (T[n][j] + MOD - B[j]) % MOD;
    }
    cout << G[m] << endl;
    return 0;
}
