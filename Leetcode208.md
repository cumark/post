---
title: Leetcode 208. Implement Trie (Prefix Tree) 实现Trie（前缀树）
author: Mark
summary: >-
  设计TrieNode节点，当insert时，则插入字典树所不存在的字符，并在插入完之后，将isWord置为true。当search时，从root节点，遍历字典树。
tags:
  - leetcode
  - algorithm
categories:
  - 算法
abbrlink: 756a1399
date: 2021-09-28 13:30:00
---

A [**trie**](https://en.wikipedia.org/wiki/Trie) (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string `word` into the trie.
- `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

 

**Example 1:**

```
Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
```

 

**Constraints:**

- `1 <= word.length, prefix.length <= 2000`
- `word` and `prefix` consist only of lowercase English letters.
- At most `3 * 104` calls **in total** will be made to `insert`, `search`, and `startsWith`.





## 分析

这道题要求设计一个Trie数的类，首先需定义一个节点，TrieNode节点应该包括如下部分：

1.包含TrieNode节点值

2.包含是否完整词汇的判断

3.包含TrieNode节点的子节点，其中应该包括26个英文字母

4.包含创建TrieNode的方法，具体有TrieNode()空函数值，及赋node节点值的方法

设计TrieNode节点后，可以设置一个root空节点，当insert时，则插入于root空节点之后



#### 方法

设计TrieNode节点，当insert时，则插入字典树所不存在的字符，并在插入完之后，将isWord置为true。

当search时，从root节点，遍历字典树。

#### 代码

```java
class TrieNode {
    public char val;
    public boolean isWord=false;
    public TrieNode[] children=new TrieNode[26];
    public TrieNode(){}
    TrieNode(char c) {
        TrieNode node=new TrieNode();
        node.val=c;
    }
}
class Trie {
    public TrieNode root;
    public Trie() {
        root=new TrieNode();
        root.val=' ';
    }
    
    public void insert(String word) {
        TrieNode node=root;
        for(int i=0;i<word.length();i++) {
            char ch=word.charAt(i);
            if(node.children[ch-'a']==null) {
                node.children[ch-'a']=new TrieNode(ch);
            }
            node=node.children[ch-'a'];
        }
        node.isWord=true;
    }
    
    public boolean search(String word) {
        TrieNode node=root;
        for(char ch:word.toCharArray()) {
            if(node.children[ch-'a']!=null) {
                node=node.children[ch-'a'];
            } else {
                return false;
            }
        }
        return node.isWord;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode node=root;
        for(char ch:prefix.toCharArray()) {
            if(node.children[ch-'a']!=null) {
                node=node.children[ch-'a'];
            } else {
                return false;
            }
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

