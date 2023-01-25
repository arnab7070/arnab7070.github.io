---
title: "Tower Of Hanoi"
date: 2023-01-25T00:24:43+05:30
tags: [DSA, C++, Tower Of Hanoi]
image: TOH.gif
description: Implement the the Tower Of Hanoi using recursion
draft: false
---
# Tower Of Hanoi
-----------------
### Algorithm
```
/*
START
Procedure Hanoi(disk, source, dest, aux)
   IF disk == 1, THEN
      move disk from source to dest
   ELSE
      Hanoi(disk - 1, source, aux, dest)     // Step 1
      move disk from source to dest          // Step 2
      Hanoi(disk - 1, aux, dest, source)     // Step 3
   END IF

END Procedure
STOP
*/
```
### Code
```cpp
#include <iostream>
using namespace std;
void TowerOfHanoi(int n, char src, char aux, char dest) {
  if (n == 1) {
    cout << "Move Disk No. " << n << " from " << src << " to " << dest << endl;
    return;
  }
  TowerOfHanoi(n - 1, src, dest, aux);
  cout << "Move Disk No. " << n << " from " << src << " to " << dest << endl;
  TowerOfHanoi(n - 1, aux, src, dest);
}
int main() {
  TowerOfHanoi(3, 'A', 'B', 'C');
  return 0;
}
```
### Output
```
Move Disk No. 1 from A to C
Move Disk No. 2 from A to B
Move Disk No. 1 from C to B
Move Disk No. 3 from A to C
Move Disk No. 1 from B to A
Move Disk No. 2 from B to C
Move Disk No. 1 from A to C
```