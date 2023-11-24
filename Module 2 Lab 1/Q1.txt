#include <iostream>
#include <unordered_set>
#include <algorithm>

int lengthOfLongestSubstring(std::string s) {
    int n = s.size();
    int maxLength = 0;
    std::unordered_set<char> charSet;
    int left = 0;
    
    for (int right = 0; right < n; ++right) {
        while (charSet.find(s[right]) != charSet.end()) {
            charSet.erase(s[left]);
            ++left;
        }
        charSet.insert(s[right]);
        maxLength = std::max(maxLength, right - left + 1);
    }
    
    return maxLength;
}

int main() {
    std::string input;
    std::cin >> input;
    
    int result = lengthOfLongestSubstring(input);
    std::cout << result << std::endl;
    
    return 0;
}
