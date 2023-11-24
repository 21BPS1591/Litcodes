#include <bits/stdc++.h>
using namespace std;

string toGoatLatin(string S) {
    istringstream iss(S);
    vector<string> words((istream_iterator<string>(iss)), istream_iterator<string>());
    string vowels = "aeiouAEIOU";
    for (int i = 0; i < words.size(); ++i) {
        if (vowels.find(words[i][0]) != string::npos) {
            words[i] += "ma";
        } else {
            words[i] = words[i].substr(1) + words[i][0] + "ma";
        }
        words[i] += string(i + 1, 'a');
    }
    ostringstream oss;
    copy(words.begin(), words.end(), ostream_iterator<string>(oss, " "));
    string res = oss.str();
    res.pop_back();
    return res;
}

int main() {
    string S;
    getline(cin, S);
    cout << toGoatLatin(S) << endl;
    return 0;
}