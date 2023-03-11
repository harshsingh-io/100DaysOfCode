# Day 10

Date Completed: March 11, 2023 2:40 AM

Date Started: March 10, 2023 11:50 PM

Difficulty: ⭐⭐⭐

Done: Yes

Languages: Java

Related to Progress (Days): 10%

Topic: Longest Word with all Prefixes(Medium), Unique Substrings Problem(Hard)

## What I Learned Today

How to count Unique Substrings in a String? Using SUFFIX

How to find Longest Word with all Prefixes?

## Key Concepts

### Unique Substrings in a String? Using SUFFIX

Given a string of length n of lowercase alphabet characters, we need to count total number of distinct substrings of this string. Examples:

```

Input  : str = “ababa”

Output : 10

Total number of distinct substring are 10, which are,

"", "a", "b", "ab", "ba", "aba", "bab", "abab", "baba"

and "ababa"

```

The idea is create a **[Trie of all suffixes](https://www.geeksforgeeks.org/pattern-searching-using-trie-suffixes/)**

 of given string. Once the Trie is constricted, our answer is total number of nodes in the constructed Trie. For example below diagram represent Trie of all suffixes for “ababa”. Total number of nodes is 10 which is our answer.

**How does this work?**

- Each root to node path of a **[Trie](https://www.geeksforgeeks.org/trie-insert-and-search/)** represents a prefix of words present in Trie. Here we words are suffixes. So each node represents a prefix of suffixes.

- Every substring of a string “str” is a prefix of a suffix of “str”.

### Longest Word with all Prefixes

Given an array of strings `words`, find the **longest** string in `words` such that **every prefix** of it is also in `words`.

- For example, let `words = ["a", "app", "ap"]`. The string `"app"` has prefixes `"ap"` and `"a"`, all of which are in words.

**Example :**

**Input:** words = [“a”, “banana”, “app”, “appl”, “ap”, “apply”, “apple”]

**Output:** “apple”

**Explanation:** Both “apple” and “apply” have all their prefixes in words. However, “apple” is lexicographically smaller, so we return that.

## **Solution**

Use a trie to store all the words. Then do depth first search on the trie. Search the nodes from left to right to make sure that the leftmost nodes (with lexicographically smallest letters) are visited first. For the words that all nodes are ends of words, update the longest word. Finally, return the longest word.

### Quick Links

---

[**Documentation**](https://www.geeksforgeeks.org/count-distinct-substrings-string-using-suffix-trie/)

[**Documentation**](https://leetcode.ca/2021-07-14-1858-Longest-Word-With-All-Prefixes/)

## Code Snippets

```java

public class UniqueSubstring {

    static class Node {

        Node[] children = new Node[26];

        boolean eow = false;

        Node() {

            for (int i = 0; i < 26; i++) {

                children[i] = null;

            }

        }

    }

    public static void insert(String word) { //O(L) where L is length of largest word

        Node curr = root;

        for (int level = 0; level < word.length(); level++) {

            int idx = word.charAt(level) - 'a';

            if (curr.children[idx] == null) {

                curr.children[idx] = new Node();

            }

            curr = curr.children[idx];

        }

        curr.eow = true;

    }

    public static boolean search(String word) { //O(L)

        Node curr = root;

        for (int level = 0; level < word.length(); level++) {

            int idx = word.charAt(level) - 'a';

            if (curr.children[idx] == null) {

                return false;

            }

            curr = curr.children[idx];

        }

        return curr.eow;

    }

    public static boolean startsWith(String prefix) { //O(L) where l is the length of prefix

        Node curr = root;

        for (int level = 0; level < prefix.length(); level++) {

            int idx = prefix.charAt(level) - 'a';

            if (curr.children[idx] == null) {

                return false;

            }

            curr = curr.children[idx];

        }

        return true;

    }

    public static int countNodes(Node root) {

        if (root == null) {

            return 0;

        }

        int count = 0;

        for (int i = 0; i < 26; i++) {

            if (root.children[i] != null) {

                count += countNodes(root.children[i]);

            }

        }

        return count + 1;

    }

    public static Node root = new Node();

    public static void main(String[] args) {

        String str = "ababa"; //ans = 10

        for (int i = 0; i < str.length(); i++) {

            String suffix = str.substring(i);

            insert(suffix);

        }

        System.out.println(countNodes(root));

    }

}

```

```java

class Solution {

    String longestWord = "";

    public String longestWord(String[] words) {

        TrieNode root = new TrieNode();

        for (String word : words) {

            TrieNode node = root;

            int length = word.length();

            for (int i = 0; i < length; i++) {

                char letter = word.charAt(i);

                int index = letter - 'a';

                if (node.children[index] == null)

                    node.children[index] = new TrieNode();

                node = node.children[index];

            }

            node.wordEnd = true;

        }

        depthFirstSearch(root, new StringBuffer());

        return longestWord;

    }

    public void depthFirstSearch(TrieNode node, StringBuffer sb) {

        if (node.wordEnd && sb.length() > longestWord.length())

            longestWord = sb.toString();

        for (int i = 0; i < 26; i++) {

            TrieNode child = node.children[i];

            if (child != null && child.wordEnd) {

                sb.append((char) ('a' + i));

                depthFirstSearch(child, sb);

                sb.deleteCharAt(sb.length() - 1);

            }

        }

    }

}

class TrieNode {

    boolean wordEnd;

    TrieNode[] children;

    public TrieNode() {

        wordEnd = false;

        children = new TrieNode[26];

    }

}

```

## Challenges Experienced

Suffered in adding character in string builder in the forloop

## Resources Used

GeeksForGeeks, LeetCode
