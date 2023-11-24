#include <bits/stdc++.h>

using namespace std;

class Solution {
public:
    vector<int> smallestTrimmedNumbers(vector<string>& nums, vector<vector<int>>& queries) {
        vector<int> res;
        for(auto x:queries)
        {
            priority_queue<pair<string,int>> v;
            for(int i=0;i<nums.size();i++)
            {
                int t=nums[i].length()-x[1];
                string p=nums[i].substr(t,x[1]);
                if(v.size()<x[0])
                    v.push({p,i});
                else
                {
                    if(v.top().first > p)
                    {
                        v.pop();
                        v.push({p,i});
                    }
                }
            }
            int val=v.top().second;
            res.push_back(val);
        }
        return res;
    }
};

int main() {
    Solution solution;
    vector<string> nums;
    string input;
    getline(cin, input);
    stringstream ss(input);
    string temp;
    while (ss >> temp) {
        nums.push_back(temp);
    }

    int q;
    cin >> q;
    vector<vector<int>> queries(q, vector<int>(2));
    for (int i = 0; i < q; ++i) {
        cin >> queries[i][0] >> queries[i][1];
    }

    vector<int> result = solution.smallestTrimmedNumbers(nums, queries);

    for (int num : result) {
        cout << num << " ";
    }
    cout << endl;

    return 0;
}
