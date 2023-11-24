#include <bits/stdc++.h>
using namespace std;

string isBalanced(const string& s) {
    stack<char> st;
    for (char c : s) {
        switch (c) {
            case '(': case '[': case '{':
                st.push(c);
                break;
            case ')':
                if (st.empty() || st.top() != '(') return "NO";
                st.pop();
                break;
            case ']':
                if (st.empty() || st.top() != '[') return "NO";
                st.pop();
                break;
            case '}':
                if (st.empty() || st.top() != '{') return "NO"; // Fix the missing single quote here
                st.pop();
                break;
        }
    }
    return st.empty() ? "YES" : "NO";
}

int main() {
    string input;
    getline(cin, input);
    stringstream ss(input);
    string s;
    while (getline(ss, s, ',')) {
        cout << isBalanced(s) << endl;
    }
    return 0;
}
