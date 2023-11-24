#include <iostream>
using namespace std;

void egyptianFraction(int n, int d) {
    if (d == 0 || n == 0) {
        return;
    }
    if (d % n == 0) {
        cout << d / n << endl;
        return;
    }
    if (n % d == 0) {
        cout << n / d << endl;
        return;
    }
    if (n > d) {
        cout << n / d << endl;
        egyptianFraction(n % d, d);
        return;
    }
    int x = d / n + 1;
    cout << x << endl;
    egyptianFraction(n * x - d, d * x);
}

int main() {
    int numerator, denominator;
    cin >> numerator;
    cin >> denominator;
    
    egyptianFraction(numerator, denominator);
    
    return 0;
}
