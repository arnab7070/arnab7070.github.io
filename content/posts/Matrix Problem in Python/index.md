---
title: Matrix Problems in Python
date: 2022-09-16
description: Various matrix problems using python
tags: ["python","matrix","numpy"]
image: python.jpg
---
# Questions
### 1. Write a python program to create an 3X3 Matrix randomly and calculate sum of the diagonal elements.
---
### Code
```py
import random
matrix = [[],[],[]]
sum1 = 0
for i in range (3):
    for j in range (3):
            matrix[i].append(random.randint(0,9))
            if i==j:
                sum1 += matrix[i][j]
print(f"The sum of the diagonal elements for the following matrix is = {sum1}")
for i in matrix:
    print(i)
```
### Output
```py
The sum of the diagonal elements for the following matrix is = 15
[5, 3, 3]
[9, 2, 1]
[6, 2, 8]
```

### 2. Write a python program to perform the addition of two 3X3 Matrixes.
---
### Code
```py
matrix1 = [[],[],[]]
print("Enter the elements of the first matrix: ")
for i in range (3):
    for j in range (3):
            var = int(input())
            matrix1[i].append(var)
matrix2 = [[],[],[]]
print("Enter the elements of the second matrix: ")
for i in range (3):
    for j in range (3):
            var = int(input())
            matrix2[i].append(var)
sum_matrix = [[],[],[]]
for i in range (3):
    for j in range (3):
        sum_matrix[i].append(matrix1[i][j]+matrix2[i][j])

print("Now the sum of the given matrix is: ")
for i in matrix1:
    print(i)
print()
for i in matrix2:
    print(i)
print()
for i in sum_matrix:
    print(i)
```
### Output
```py
Enter the elements of the first matrix: 
1    
2
3
4
5
6
7
8
9
Enter the elements of the second matrix: 
1
2
3
4
5
6
7
8
9
Now the sum of the given matrix is: 
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

[2, 4, 6]
[8, 10, 12]
[14, 16, 18]
```

### 3. Write a python program to perform the elements-wise multiplication of two 3X3 Matrixes.
---
### Code
```py
matrix1 = [[],[],[]]
print("Enter the elements of the first matrix: ")
for i in range (3):
    for j in range (3):
            var = int(input())
            matrix1[i].append(var)
matrix2 = [[],[],[]]
print("Enter the elements of the second matrix: ")
for i in range (3):
    for j in range (3):
            var = int(input())
            matrix2[i].append(var)
mul_matrix = [[],[],[]]
for i in  range (3):
    for j in range (3):
        mul_matrix[i].append(matrix1[i][j]*matrix2[i][j])
print("Now the elements-wise multiplication of the given matrix is: ")
for i in matrix1:
    print(i)
print()
for i in matrix2:
    print(i)
print()
for r in mul_matrix:
    print(r)
```
### Output
```py
Enter the elements of the first matrix: 
1 
2
3
4
5
6
7
8
9
Enter the elements of the second matrix: 
1
1
1
1
1
1
1
1
1
Now the elements-wise multiplication of the given matrix is: 
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

[1, 1, 1]
[1, 1, 1]
[1, 1, 1]

[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
```

### 4. Write a python program to perform the Matrix Multiplication of two 3X3 Matrixes.
---
### Code
```py
import numpy
matrix1 = [[],[],[]]
print("Enter the elements of the first matrix: ")
for i in range (3):
    for j in range (3):
            var = int(input())
            matrix1[i].append(var)
matrix2 = [[],[],[]]
print("Enter the elements of the second matrix: ")
for i in range (3):
    for j in range (3):
            var = int(input())
            matrix2[i].append(var)
mul_matrix = [[],[],[]]
print("Multiplication of these two matrix will be: ")
for i in matrix1:
    print(i)
print()
for i in matrix2:
    print(i)
print()

mul_matrix = numpy.dot(matrix1,matrix2)
 
for r in mul_matrix:
    print(r)
```
### Output
```py
Enter the elements of the first matrix: 
1
2
3
4
5
6
7
8
9
Enter the elements of the second matrix: 
1
2
3
4
5
6
7
8
9
Multiplication of these two matrix will be: 
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

[1, 2, 3]
[4, 5, 6]
[7, 8, 9]

[30 36 42]
[66 81 96]
[102 126 150]
```

### 5. Write a python program to find row wise maximum and column wise minimum element.
---
### Code
```py
matrix = [[],[],[]]
print("Enter the values of matrix: ")
for i in range (3):
    for j in range (3):
            var = int(input())
            matrix[i].append(var)
max_row = []
max_column = []
for i in range (3):
    temp = 0
    for j in range (3):
        if matrix[i][j]>temp:
            temp = matrix[i][j]
    max_row.append(temp)
for i in range (3):
    var = 0
    for j in range (3):
        if matrix[j][i]>var:
            var = matrix[j][i]
    max_column.append(var)
for i in matrix:
    print(i)
print()
print(f"Max row elements of the matrix {max_row}")
print(f"Max column elements of the matrix {max_column}")
```
### Output
```py
Enter the values of matrix: 
1
4
8
3
2
5
3
7
9
[1, 4, 8]
[3, 2, 5]
[3, 7, 9]

Max row elements of the matrix [8, 5, 9]
Max column elements of the matrix [3, 7, 9]
```
