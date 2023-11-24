#include <iostream>
#include <vector>

using namespace std;

int main() {
    int size, queries;
    cin >> size >> queries;
    vector<int> array(size + 1, 0);

    for (int i = 0; i < queries; ++i) {
        int left, right, value;
        cin >> left >> right >> value;
        array[left] += value;
        if (right + 1 <= size) {
            array[right + 1] -= value;
        }
    }

    int maxVal = array[1];
    for (int i = 2; i <= size; ++i) {
        array[i] += array[i - 1];
        maxVal = max(maxVal, array[i]);
    }

    cout << maxVal << endl;
    return 0;
}
