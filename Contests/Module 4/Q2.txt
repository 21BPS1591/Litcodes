#include <bits/stdc++.h>

using namespace std;

struct Job {
    char name;
    int deadline;
    int profit;
};

class Solution {
public:
    vector<char> jobSequencing(vector<Job>& jobData) {
        sort(jobData.begin(), jobData.end(), [](const Job& a, const Job& b) {
            return (a.profit > b.profit) || (a.profit == b.profit && a.deadline > b.deadline);
        });

        vector<char> result;
        set<int> timeSlots;
        for (const Job& job : jobData) {
            for (int t = job.deadline; t > 0; --t) {
                if (timeSlots.find(t) == timeSlots.end()) {
                    timeSlots.insert(t);
                    result.push_back(job.name);
                    break;
                }
            }
        }

        return result;
    }
};

int main() {
    Solution solution;

    int n;
    cin >> n;

    vector<Job> jobs(n);
    for (int i = 0; i < n; ++i) {
        cin >> jobs[i].name;  // Job name
    }
    for (int i = 0; i < n; ++i) {
        cin >> jobs[i].deadline;  // Deadline
    }
    for (int i = 0; i < n; ++i) {
        cin >> jobs[i].profit;  // Profit
    }

    vector<char> result = solution.jobSequencing(jobs);

    for (char ch : result) {
        cout << ch << " ";
    }
    cout << endl;

    return 0;
}