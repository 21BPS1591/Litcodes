#include <iostream>
#include <string>

using namespace std;

long long maximumSubsequenceCount(string text, string pattern) {
    long long res = 0, cnt1 = 0, cnt2 = 0;
    for (char& c: text) {   
        if (c == pattern[1])
            res += cnt1, cnt2++;
        if (c == pattern[0])
            cnt1++;
    }
    return res + max(cnt1, cnt2);
}

int main() {
    string text, pattern;
    cin >> text;
    cin >> pattern;

    long long result = maximumSubsequenceCount(text, pattern);
    cout << result << endl;

    return 0;
}
