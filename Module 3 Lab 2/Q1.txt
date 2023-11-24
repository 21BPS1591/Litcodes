#include <bits/stdc++.h>

using namespace std;

vector<int> slidingSubarrayBeauty(vector<int>& arr, int k, int n) {
    vector<int> result;
    deque<int> dq;

    for (int i = 0; i < arr.size(); ++i) {
        while (!dq.empty() && dq.front() < i - k + 1) {
            dq.pop_front();
        }

        while (!dq.empty() && arr[dq.back()] > arr[i]) {
            dq.pop_back();
        }

        dq.push_back(i);

        if (i >= k - 1) {
            result.push_back(arr[dq.front() + n - 1]);
        }
    }

    return result;
}

int main() {
    string input;
    getline(cin, input);
    stringstream ss(input);
    vector<int> arr;
    int num;
    while (ss >> num) {
        arr.push_back(num);
    }

    int k, n;
    cin >> k >> n;

    vector<int> result = slidingSubarrayBeauty(arr, k, n);

    for (int i = 0; i < result.size(); ++i) {
        cout << result[i] << " ";
    }

    cout << endl;

    return 0;
}
