#include <iostream>

using namespace std;

class Solution {
public:
    int clumsy(int N) {
        long ans = 0;
        for (int i = N; i >= 1; i -= 4) {
            long x = (i == N ? 1 : -1) * i;
            if (i - 1 >= 1) {
                x *= i - 1;
                if (i - 2 >= 1) {
                    x /= i - 2;
                    if (i - 3 >= 1) {
                        x += i - 3;
                    }
                }
            } 
            ans += x;
        }
        return ans;
    }
};

int main() {
    Solution solution;
    int N;
    cin >> N;
    int clumsyFactorial = solution.clumsy(N);
    cout << clumsyFactorial << endl;
}
