`Given two strings, write a method to decide if one is a permutation of the other.`
#### Sol 1: Sort and compare
```
TC : O(nlogn)
SC : O(1)
```

#### Sol 2: Use Character count array
```
TC : O(n)
SC : O(1) - constant space comp
```

#### Sol 1
```
String sort(String s) {
	char[] content = s.toCharArray();
	java.util.Arrays.sort(content);
	return new String(content);
}

boolean permutation(String s, String t) {
	if (s.length() != t.length()) {
		return false;
	}
	return sort(s).equals(sort(t));
}
```

#### Sol 2
```
 boolean permutation(String s, String t) {
	if (s.length() != t.length()) {
		return false;
	}

	int[] letters = new int[128]; // Assumption
	char[] s_array = s.toCharArray();
	for (char c : s_array) {
		II count number of each char in s.
		letters[c]++;
	}
	for (int i = 0; i < t.length(); i++) {
		int c = (int) t.charAt(i);
		letters[c]--;
		if (letters[c] < 0) {
			return false;
		}
	}

	return true;
}
```
