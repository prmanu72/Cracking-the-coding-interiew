```
There are three types of edits that can be performed on strings: insert a character,
remove a character, or replace a character. Given two strings, write a function to check if they are
one edit (or zero edits) away.
EXAMPLE
pale, ple -> true
pales, pale -> true
pale, bale -> true
pale, bae -> false
```

#### Sol 1
```java
boolean oneEditAway (String first, String second) {
	if (first.length() == second. length()) {
		return oneEditReplace(first, second);
	} else if (first.length() + 1 == second. length()) {
		return oneEdit Insert(first, second);
	} else if (first.length() - 1 == second. length()) {
		return oneEditInsert(second, first);
	}
	return false;
}
boolean oneEditReplace(String si, String s2) {
	boolean foundDifference = false;
	for (int i = 0; i < s1.length(); i++) {
		if (s1.charAt(i) != s2.charAt(i)) {
			if (foundDifference) {
				return false;
			}
			foundDifference = true;
		}
	}
	return true;

}


/* Check if you can insert a character into si to make s2. */
boolean oneEdit Insert(String s1, String s2) {
	int index1 = 0;
	int index2 = 0;
	while (index2 < 52. length() && index1 < s1. length()) {
		if ($1.charAt(index1) != 52.charAt(index2)) {
			if (index1 != index2) {
				return false;
			}
			index2++;
		} else {
			index1++;
			index2++;
		}
	}
	return true;
}
```

Merging two functions
```java
boolean oneEditAway(String first, String second) {
	/* Length checks. */
	if (Math.abs(first.length() - second.length()) > 1) {
		return false;
	}

	/* Get shorter and longer string.*/
	String s1 = first.length() < second.length() ? first : second;
	String s2 = first.length() < second.length() ? second : first;



	int index1 = 0;

	int index2 = 0;

	boolean foundDifference = false;

	while (index2 < s2.length() && index1 < s1.length()) {
		if (s1.charat(index1) != s2.charat(index2)) {

			/* Ensure that this is the first difference found.*/
			if (foundDifference) return false;
			foundDifference = true;

			if (s1.length() == s2.length()) { // On replace, move shorter pointer
				index1++;
			}
		} else {

			index1++; // If matching, move shorter pointer
		}

		index2++; // Always move pointer for longer string
	}

	return true;
}
```
