#include <bits/stdc++.h>

using namespace std;

struct TrieNode {
    TrieNode* children[26];
    bool isEnd;

    TrieNode() {
        for (int i = 0; i < 26; ++i) {
            children[i] = nullptr;
        }
        isEnd = false;
    }
};

class Trie {
public:
    Trie() {
        root = new TrieNode();
    }

    void insert(const string& word) {
        TrieNode* node = root;
        for (char ch : word) {
            int index = ch - 'a';
            if (node->children[index] == nullptr) {
                node->children[index] = new TrieNode();
            }
            node = node->children[index];
        }
        node->isEnd = true;
    }

    bool hasPrefix(const string& word) {
        TrieNode* node = root;
        for (char ch : word) {
            int index = ch - 'a';
            if (node->children[index] == nullptr) {
                return false;
            }
            node = node->children[index];
            if (node->isEnd) {
                return true;
            }
        }
        return false;
    }

private:
    TrieNode* root;
};

bool isGoodPassword(const vector<string>& passwords) {
    Trie trie;
    for (const string& password : passwords) {
        if (trie.hasPrefix(password)) {
            cout << "BAD PASSWORD" << endl;
            return false;
        }
        trie.insert(password);
    }
    cout << "GOOD PASSWORD" << endl;
    return true;
}

int main() {
    string input;
    getline(cin, input);
    stringstream ss(input);
    vector<string> passwords;
    string password;
    while (ss >> password) {
        passwords.push_back(password);
    }

    isGoodPassword(passwords);

    return 0;
}
