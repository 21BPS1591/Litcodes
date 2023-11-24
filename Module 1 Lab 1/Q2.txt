#include <iostream>
#include <unordered_map>
#include <vector>
#include <sstream>

class Solution {
public:
    int findMaxLength(std::vector<int>& nums) {
        if(nums.size() == 0) {
            return 0;
        }
        
        int maxLen = 0;
        int presum = 0;
        std::unordered_map<int, int> map;
        map[0] = -1;
        
        for(int i = 0; i < nums.size(); ++i) {
            if(nums[i] == 0) {
                presum -= 1;
            } else if(nums[i] == 1) {
                presum += 1;
            }
            
            if(map.find(presum) != map.end()) {
                int idx = map[presum];
                int currLen = i - idx;
                maxLen = std::max(maxLen, currLen);
            } else {
                map[presum] = i;
            }
        }
        return maxLen;
    }
};

int main() {
    Solution solution;
    std::string input;
    std::getline(std::cin, input);
    std::istringstream iss(input);
    
    std::vector<int> nums;
    int num;
    while (iss >> num) {
        nums.push_back(num);
    }

    int result = solution.findMaxLength(nums);
    std::cout << result << std::endl;
    return 0;
}