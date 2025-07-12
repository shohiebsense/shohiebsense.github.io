[The problem](https://www.hackerrank.com/challenges/flipping-the-matrix/problem)


### 1. Find the length

```go
length := len(matrix)
```
### 2. Find the quadrant
```go
quadrantSize := length / 2
```
### 3. read and fully understand the behavior

### 4. Get the top-left, top-righht (its mirror / opposite), bottom left, and bottom-right (its opposite)

```go
	for i := 0; i < quadrantSize; i++ {

		for j:= 0; j < quadrantSize; j++ {
			topLeft := matrix[i][j]
			topRight := matrix[i][length - 1 - j]
			bottomLeft := matrix[length - 1 - i][j]
			bottomRight := matrix[length - 1 - i][length - 1 - j]

			sum += max(topLeft, topRight, bottomLeft, bottomRight)

		}
	}
```

### 5. return the sum.
