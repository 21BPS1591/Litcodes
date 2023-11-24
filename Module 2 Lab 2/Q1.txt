#include <iostream>

using namespace std;

class Solution {
public:
    int minimumNumbers(int num, int k) {
        if (num == 0) return 0;
        for (int i = 1; i <= num; ++i) {
            int t = num - k * i;
            if (t >= 0 && t % 10 == 0) return i;
        }
        return -1;
    }
};

int main() {
    Solution solution;
    int num, k;
    cin >> num;
    cin >> k;

    int result = solution.minimumNumbers(num, k);
    if (result == -1) {
        cout << "-1" << endl;
    } else {
        cout << result << endl;
    }

    return 0;
}
