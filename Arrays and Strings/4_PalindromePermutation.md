```
Given a string, write a function to check if it is a permutation of
a palindrome. A palindrome is a word or phrase that is the same forwards and backwards. A
permutation is a rearrangement of letters. The palindrome does not need to be limited to just
dictionary words.
EXAMPLE
Input: Tact Coa
Output: True (permutations: "taco cat'; "atco eta·; etc.)
```
1. Strings with even length (after removing all non-letter characters) must have all even counts of characters
2. Strings of an odd length must have exactly one character with an odd count.

#### Sol 1
We use a hash table to count how many times each character appears. Then, we iterate through the hash table and ensure that no more than one character has an odd count. 
```java
boolean isPermutationOfPalindrome(String phrase) {
	int[] table = buildCharFrequencyTable(phrase);
	return checkMaxOneOdd(table);
}

/* Check that no more than one character has an odd count. */
boolean checkMaxOneOdd(int[] table) {
	boolean foundOdd = false;
	for (int count : table) {
		if (count % 2 == 1) {
			if (foundOdd) {
				return false;
			}
			foundOdd = true;
		}
	}
	return true;
}

/* Map each character to a number. a -> 0, b -> 1, c -> 2, etc.
* This is case insensitive. Non-letter characters map to -1. */
int getCharNumber(Character c) {
	int a = Character.getNumericValue('a');
	int z = Character.getNumericValue('z');
	int val = Character.getNumericValue(c);
	if (a <= val && val <= z) {
		return val - a;
	}
	return -1;
}

/* Count how many times each character appears. */
int[] buildCharFrequencyTable(String phrase) {
	int[] table new int[Character.getNumericValue('z')
	                    Character.getNumericValue('a') + 1];
	for (char c phrase.toCharArray()) {
		int x = getCharNumber(c);
		if (x != -1) {
			table[x]++;
		}
	}
	return table;
}
```

#### Sol 2
Instead of checking the number of odd counts at the end, we can check as we go along.
```java
boolean isPermutationOfPalindrome(String phrase) {
	int countOdd = 0;
	int[] table new int[Character.getNumericValue('z') -
	                    Character.getNumericValue('a') + 1];
	for (char c phrase.toCharArray()) {
		int x = getCharNumber(c);
		if (x != -1) {
			table[x]++;
			if (table[x] % 2 1) {
				countOdd++;
			} else {
				countOdd--;
			}
		}
	}
	return countOdd <= 1;
}
```

#### Sol 3
1. we can use a single integer (as a bit vector). When we see a letter, we map it to an integer
between O and 26 (assuming an English alphabet). 
2. Then we toggle the bit at that value. At the end of the iteration, we check that at most one bit in the integer is set to 1.
3. We can easily check that no bits in the integer are 1: just compare the integer to 0. 
4. There is actually a very elegant way to check that an integer has exactly one bit set to 1.
`00010000 - 1 = 00001111
00010000 & 00001111 = 0 `

```java
boolean isPermutationOfPalindrome(String phrase) {
	int bitVector = createBitVector(phrase);
	return bitVector == 0 || checkExactlyOneBitSet(bitVector);
}

/* Create a bit vector for the string. For each letter with value i, toggle the
* ith bit. */
int createBitVector(String phrase) {
	int bitVector = 0;
	for (char c : phrase.toCharArray()) {
		int x = getCharNumber(c);
		bitVector = toggle(bitVector, x);
	}
	return bitVector;
}

/* Toggle the ith bit in the integer. */
int toggle(int bitVector, int index) {
	if (index < 0) return bitVector;
	int mask = 1 << index;
	if ((bitVector & mask) == 0) {
		bitVector  |= mask;
	} else {
		bitVector &= ~mask;
	}
	return bitVector;

}

/* Check that exactly one bit is set by subtracting one from the integer and
* ANDing it with the original integer. */
boolean checkExactlyOneBitSet(int bitVector) {
	return (bitVector & (bitVector - 1)) == 0;
}
```

