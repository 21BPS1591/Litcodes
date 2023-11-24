#include <bits/stdc++.h>
using namespace std;

void stringAnalysis(const string& str){
    double uppercase=0, lowercase=0, digit=0, specialchar=0;
    int n = str.length();
    for(int i=0; i<n; i++)
    {
        if(isdigit(str[i]))
            digit = digit+1;
        else if(str[i] >= 'a' && str[i] <= 'z')
            lowercase = lowercase+1;
        else if(str[i] >= 'A' && str[i] <= 'Z')
            uppercase = uppercase+1;
        else
            specialchar = specialchar+1;
    }
    cout << fixed << setprecision(3);
    cout << (uppercase/n)*100 << "%" << endl;
    cout << (lowercase/n)*100 << "%" << endl;
    cout << (digit/n)*100 << "%" << endl;
    cout << (specialchar/n)*100 << "%" << endl;
}

int main() {
    string str;
    cin >> str;
    stringAnalysis(str);
}