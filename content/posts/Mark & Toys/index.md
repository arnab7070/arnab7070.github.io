---
title: "Mark & Toys"
date: 2022-11-07T19:19:17+05:30
draft: false
description: Given a list of toy prices and an amount to spend, determine the maximum number of gifts he can buy.
tags: ["Hackerrank","C++","Practice Question"]
image: hackerrank.png
---
> This question is taken from HackerRank Website. Here is the [link](https://www.hackerrank.com/challenges/mark-and-toys/problem)
# Problem Statement
Mark and Jane are very happy after having their first child. Their son loves toys, so Mark wants to buy some. There are a number of different toys lying in front of him, tagged with their prices. Mark has only a certain amount to spend, and he wants to maximize the number of toys he buys with this money. Given a list of toy prices and an amount to spend, determine the maximum number of gifts he can buy.

**Note** Each toy can be purchased only once.
# Example
```
prices = [1,2,3,4]
k = 7
```
The budget is 7 units of currency. He can buy items that cost [1,2,3] for 6, or [3,4] for 7 units. The maximum is 3 items.
#### Sample Input
```
7 50
1 12 5 111 200 1000 10
```
#### Sample Output
```
4
```
#### Explanation
```
He can buy only 4 toys at most. These toys have the following prices: [1,5,10,12].
```
### Algorithm
---
1. Sort the array.
2. Initialize i = 0, count = 0.
3. Now until we reach K<=0 we run a loop to iterate all of the prices in increasing manner so that we can get the maximum number of toys.
4. Now when the loop ends the corner case comes. If K < 0 then we should decrement the value of count by 1 just once. 
5. Finally return count value to get the answer.
---
### Code
```cpp
#include <bits/stdc++.h>

using namespace std;

string ltrim(const string &);
string rtrim(const string &);
vector<string> split(const string &);

/*
 * Complete the 'maximumToys' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts following parameters:
 *  1. INTEGER_ARRAY prices
 *  2. INTEGER k
 */
//----> Main Code Snippet Begins
int maximumToys(vector<int> prices, int k) {
    sort(prices.begin(), prices.end());
    int i = 0, count = 0;
    while(k>0){
        k -= prices[i];
        count++;
        i++;
    }
    if(k<0){
        count--;
    }
    return count;
}
//<--- Code Snippet Ends
int main()
{
    ofstream fout(getenv("OUTPUT_PATH"));

    string first_multiple_input_temp;
    getline(cin, first_multiple_input_temp);

    vector<string> first_multiple_input = split(rtrim(first_multiple_input_temp));

    int n = stoi(first_multiple_input[0]);

    int k = stoi(first_multiple_input[1]);

    string prices_temp_temp;
    getline(cin, prices_temp_temp);

    vector<string> prices_temp = split(rtrim(prices_temp_temp));

    vector<int> prices(n);

    for (int i = 0; i < n; i++) {
        int prices_item = stoi(prices_temp[i]);

        prices[i] = prices_item;
    }

    int result = maximumToys(prices, k);

    fout << result << "\n";

    fout.close();

    return 0;
}

string ltrim(const string &str) {
    string s(str);

    s.erase(
        s.begin(),
        find_if(s.begin(), s.end(), not1(ptr_fun<int, int>(isspace)))
    );

    return s;
}

string rtrim(const string &str) {
    string s(str);

    s.erase(
        find_if(s.rbegin(), s.rend(), not1(ptr_fun<int, int>(isspace))).base(),
        s.end()
    );

    return s;
}

vector<string> split(const string &str) {
    vector<string> tokens;

    string::size_type start = 0;
    string::size_type end = 0;

    while ((end = str.find(" ", start)) != string::npos) {
        tokens.push_back(str.substr(start, end - start));

        start = end + 1;
    }

    tokens.push_back(str.substr(start));

    return tokens;
}

```
> Time Complexity for this code O(n)
#### Output for the given code
----
##### Input
```
7 50
1 12 5 111 200 1000 10
```
##### Output
`4`
##### Expected Output
`4`

---