#include <bits/stdc++.h>

using namespace std;

class Solution {
public:
    int minStepsToReachTargetSweetness(int target, vector<int>& candies) {
        priority_queue<int, vector<int>, greater<int>> minHeap(candies.begin(), candies.end());

        int steps = 0;
        while (minHeap.top() < target) {
            int leastSweet = minHeap.top();
            minHeap.pop();
            int secondLeastSweet = minHeap.top();
            minHeap.pop();

            int newSweetness = leastSweet + 2 * secondLeastSweet;
            minHeap.push(newSweetness);
            steps++;
        }

        return steps;
    }
};

int main() {
    Solution solution;
    int target;
    cin >> target;

    cin.ignore();

    string input;
    getline(cin, input);
    
    stringstream ss(input);
    vector<int> candies;
    int sweetness;
    while (ss >> sweetness) {
        candies.push_back(sweetness);
    }

    int steps = solution.minStepsToReachTargetSweetness(target, candies);
    cout << steps << endl;

    return 0;
}
