```
Implement a method to perform basic string compression using the counts
of repeated characters. For example, the string aabcccccaaa would become a2blc5a3. If the
"compressed" string would not become smaller than the original string, your method should return
the original string. You can assume the string has only uppercase and lowercase letters (a - z). 
```

 If next character is different than current, append this char to result
```java
String compressBad(String str) {
	String compressedString = "";
	int countConsecutive = 0;
	for (int i = 0; i < str.length(); i++) {
		countConsecutive++;

		/* If next character is different than current, append this char to result.*/
		if (i + 1 >= str.length() || str.charAt(i) != str.charAt(i + 1)) {
			compressedString += "" + str. charAt ( i) + countConsecuti ve;
			countConsecutive = 0;
		}
	}
	return compressedString.length() < str.length() ? compressedString str;
}
```
Runtime is O(p + k^2 ), where p is the size of the original string and k is thel
number of character
sequences. For example, if the string is aabccdeeaa, then there are six characte sequences. It's slow
because string concatenation operates in O(n^2)

#### Fix this by using a StringBuilder
```java
String compress(String str) {
	StringBuilder compressed = new StringBuilder();
	int countConsecutive = 0;
	for (int i = 0; i < str.length(); i++) {
		countConsecutive++;

		/* If next character is different than current, append this char to result.*/
		if (i + 1 >= str.length() || str.charAt(i) != str.charAt(i + 1)) {
			compressed.append(str.charAt(i));
			compressed.append(countConsecutive);
			countConsecutive = 0;
		}
	}
	return compressed.length() < str.length() ? compressed.toString() : str;
}
```

Above solutions create the compressed string, then return shorter string. Below approach create cpmpressed string
only when it is shorter but adds duplicate code

Initialize StringBuilder to its necessary capacity up-front without the need of doubling size late
```java

String compress(String str) {
	/* Check final length and return input string if it would be longer. */
	int finallength = countCompression(str);
	if (finallength >= str.length()) return str;
	StringBuilder compressed = new StringBuilder(finalLength); // initial capacity
	int countConsecutive = 0;
	for (int i = 0; i < str.length(); i++) {
		countConsecutive++;

		/* If next character is different than current, append this char to result.*/
		if (i + 1 >= str.length() || str.charAt(i) != str.charAt(i + 1)) {
			compressed.append(str.charAt(i));
			compressed.append(countConsecutive);
			countConsecutive = 0;
		}
	}
	return compressed.toString();
}

int countCompression(String str) {
	int compressedlength = 0;
	int countConsecutive = 0;
	for (int i = 0; i < str.length(); i++) {
		countConsecutive++;

		/* If next character is different than current, increase the length.*/
		if (i + 1 >= str.length() I I str.charAt(i) != str.charAt(i + 1)) {
			compressedlength += 1 + String.valueOf(countConsecutive).length();
			countConsecutive = 0;
		}
	}
	return compressedlength;
}
```


