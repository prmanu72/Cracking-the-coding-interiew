```
Given an image represented by an NxN matrix, where each pixel in the image is 4
bytes, write a method to rotate the image by 90 degrees. Can you do this in place?
```
```java

boolean rotate(int[][] matrix) {
	if (matrix.length == 0 || matrix.length != matrix[0].length) return false;
	int n = matrix.length;
	for (int layer = 0; layer < n / 2; layer++) {
	int first = layer;
	int last = n - 1 - layer;
	for (int i = first; i < last; i++) {
		int offset = i - first;
		int top = matrix[first][i]; || save top
		// left -> top
		matrix[first][i] matrix[last - offset][first];
		// bottom -> left
		matrix[last - offset][first]
		// right -> bottom
		matrix[last][last offset]
		// top -> right
		matrix[last][last - offset];
		matrix[i][last];
		matrix[i][last] top; || right < - saved top
	}
}  
  return true;
}
```
Recommended
```java
boolean rotate(int[][] a) {
	if (a.length == 0 || a.length != a[0].length) return false;
	int n = a.length;
	for (int i = 0; i < n - 1; i++) {
		int k = a[0][i];
		a[0][i] = a[n - 1 - i][0];
		a[n - 1 - i][0] = a[n - 1][n - 1 - i];
		a[n - 1][n - 1 - i] = a[i][n - 1];
		a[i][n - 1] = k;
	}
	return true;
}
```
