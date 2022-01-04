```
Zero Matrix: Write an algorithm such that if an element in an MxN matrix is 0, its entire row and
column are set to 0. 
```
One way around this is to keep a second matrix which flags the zero locations. We would then do a second
pass through the matrix to set the zeros. This would take O(MN) space. 


We use two arrays to keep track of all the rows with zeros and all
the columns with zeros. We then nullify rows and columns based on the values in these arrays.
It would still be O(N) space
#### sol 1
```java
void setZeros(int[][] matrix) {
	boolean[] row = new boolean[matrix .length];
	boolean[] column = new boolean[matrix[0].length];

// Store the row and column index with value 0
	for (int i = 0; i < matrix.length; i++) {
		for (int j = 0; j < matrix[0].length; j++) {
			if (matrix[i][j] == 0) {
				row[i] = true;
				column[j] = true;
			}
		}
	}

	// Nullify rows
	for (inti = 0; i < row.length; i++) {
		if (row[i]) nullifyRow(matrix, i);
	}

// Nullify columns
	for (int j = 0; j < column.length; j++) {
		if (column[j]) nullifyColumn(matrix, j);
	}
}

void nullifyRow(int[][] matrix, int row) {
	for (int j = 0; j < matrix[0].length; j++) {
		matrix[row][j] = 0;
	}
}

void nullifyColumn(int[][] matrix, int col) {
	for (int i = 0; i < matrix.length; i++) {
		matrix[i][col] = 0;
	}
}
```

 Reduce the space to 0(1) by using the first row as a replacement for the row array and the first
column as a replacement for the column array
#### Sol 2
```java

void setzeros(int[][] matrix) {
	boolean rowHasZero = false;
	boolean colHasZero = false;
// Check if first row has a zero
	for (int j = 0; j < matrix[0].length; j++) {
		if (matrix[0][j] == 0) {
			rowHasZero = true;
			break;
		}
	}

// Check if first column has a zero
	for (int i = 0; i < matrix.length; i++) {
		if (matrix[i][0] == 0) {
			colHasZero = true;
			break;
		}
	}
// Check for zeros in the rest of the array
	for (int i = 1; i < matrix.length; i++) {
		for (int j = 1; j < matrix[0].length; j++) {
			if (matrix[i][j] == 0) {
				matrix[i][0] = 0;
				matrix[0][j] = 0;
			}
		}
	}
// Nullify rows based on values in first column
	for (int i = 1; i < matrix.length; i++) {
		if (matrix[i][0] == 0) {
			nullifyRow(matrix, i);
		}
	}
// Nullify columns based on values in first row
	for (int j = 1; j < matrix[0].length; j++) {
		if (matrix[0][j] == 0) {
			nullifyColumn(matrix, j);
		}
	}
// Nullify first row
	if (rowHasZero) {
		nullifyRow(matrix, 0);
	}
// Nullify first column
	if (colHasZero) {
		nullifyColumn(matrix, 0);
	}
}
```

