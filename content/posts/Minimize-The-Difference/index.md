---
title: "Minimize the Difference"
date: 2022-10-12T08:37:21+05:30
draft: false
description: Minimize the difference between maximum and minimum elements of the array after performing the increment or decrement on every element of the array.
tags: ["Practice Question","Code Studio","Love Babbar DSA Sheet"]
image: DSA CRACKER.png
---

# Problem Statement
You are given an array ‘A’ of length ‘N’ consisting only of positive integers and an integer ‘K’. You have to update every element of the array by increasing or decreasing its value by ‘K’ only once. Your task is to minimize the difference between maximum and minimum elements of the array after performing the increment or decrement on every element of the array.
> Note: After the operation, every value of the array should remain non-negative.
---
Let’s say the array ‘A’ = [1, 2, 3, 4, 5] and ‘K’ = 2, then after increasing each element by ‘K’. The array ‘A’ will become [3, 4, 5, 6, 7]. So the maximum - minimum will be 7 - 3 = 4. 
### Sample Input
```
2
4 2
1 5 8 10
5 2
1 2 3 4 5
```
### Sample Output
```
5
3
```
### Explanation for this example
* For test case 1:
The final array will look like [3, 3, 6, 8]. So the difference between maximum and minimum is 8 - 3 = 5.
* For test case 2:
The final array will look like [3, 4, 1, 2, 3]. So the difference between maximum and minimum is 4 - 1 = 3.

---
# Solution
---
### Greedy Approach

Approach: We sort the given array, and then for each index, we perform the decrement operation on all the indexes greater than index ‘i’ and increment operation until the index ‘i’. Find the difference between maximum and minimum and update the answer. This works because we decrease all the greater values and increase the smaller ones, ultimately leading to a smaller difference.

### Algorithm:

* Sort ‘A’.
* Create a variable, ‘ans’, and initialize it to the difference between the last and first terms of ‘A’.
* Create two variables, ‘minimum’ and ‘maximum’ and initialize them to ‘A[0] + K’ and ‘A[N - 1] - K’, respectively.
* Create two variables, ‘current_minimum’ and ‘current_maximum’.
* Iterate using a for loop from i = ‘0’ to ‘N - 1’.
    * Update ‘current_minimum’ to min(minimum, A[i + 1] - K).
    * Update ‘current_maximum’ to max(maximum, A[i] + K).
    * If ‘current_minimum’ is non-negative. Update ‘ans’ to min(ans, current_maximum - current_minimum).
* Print ‘ans’.

# Code
```cpp
/*
    Time Complexity: O(N).
    Space Complexity: O(1).

    Where 'N' is the length of the array.
*/
// This is the main minimizeIt function to this solution.
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int minimizeIt(vector<int> A, int K)
{
    int n = A.size();
    sort(A.begin(), A.end());
    int ans = A[n - 1] - A[0];
    int minimum = A[0] + K;
    int maximum = A[n - 1] - K;
    int current_minimum, current_maximum;
    for (int i = 0; i < n - 1; i++)
    {
        // Finding the minimum and the maximum value if we perform the decrement operation on all the
        // indexes greater than index ‘i’ and increment operation until the index ‘i’.
        current_minimum = min(A[i + 1] - K, minimum);
        current_maximum = max(A[i] + K, maximum);
        // Checking if minimum value is non-negative or not.
        if (current_minimum >= 0)
        {
            ans = min(ans, current_maximum - current_minimum);
        }
    }
    return ans;
}
// Driver Code
int main(){
    int testcase;
    cin>>testcase;
    while(testcase--){
        int size,k;
        cin>>size>>k;
        vector<int> arr(size);
        for(int i = 0; i < size; i++){
            cin>>arr[i];
        }

        cout<<minimizeIt(arr,k)<<endl;
    }
    return 0;
}
```
> Code is provided by Code Studio. This is the *[Link](https://www.codingninjas.com/codestudio/problems/minimize-the-difference_3208652?topList=love-babbar-dsa-sheet-problems&leftPanelTab=0)*.