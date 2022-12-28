---
title: "Reverse Words in a Given String"
date: 2022-10-12T16:51:37+05:30
draft: false
description: Given a String S, reverse the string without reversing its individual words. Words are separated by dots.
image: DSA.png
tags: ["Practice Question","GFG","SDE Sheet"]
---
# Question
Given a String S, reverse the string without reversing its individual words. Words are separated by dots.
### Example
###### Input: 
`S = i.like.this.program.very.much`
###### Output: 
`much.very.program.this.like.i`
###### Explanation: 
After reversing the whole string(not individual words), the input string becomes
`much.very.program.this.like.i`
# Algorithm
> It's a really basic problem based upon `string & stack`. First of all we need to store the words seperated by dots into a stack. Then we need to pop one word after another from the stack and add a dot infront of it in the `answer string`. Then simply return the string. 
# Code
---
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution
{
    public:
    //Function to reverse words in a given string.
    string reverseWords(string S) 
    { 
        string curr_str = "";
        stack<string> string_stack;
        for(int i = 0; i < S.length(); i++){
            if(S[i]=='.'){
                string_stack.push(curr_str);
                curr_str = "";
                continue;
            }
            curr_str += S[i];
        }
        //For the last word
        string_stack.push(curr_str);
        
        string newString = "";
        while(!string_stack.empty()){
            newString += string_stack.top();
            string_stack.pop();
            //Because we dont want to add full stop for the last word
            if(!string_stack.empty()){
                newString += '.';
            }
        }
        
        return newString;
    } 
};

//{ Driver Code Starts }.
int main() 
{
    int t;
    cin >> t;
    while (t--) 
    {
        string s;
        cin >> s;
        Solution obj;
        cout<<obj.reverseWords(s)<<endl;
    }
}
```
# Company Tags
- `Accolite`
- `Adobe`
- `Amazon`
- `Goldman Sachs`
- `Microsoft`
- `Paytm`