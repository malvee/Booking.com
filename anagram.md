## Problem:
An anagram is a word that can be written as a permutation of the characters
of another word, like "dirty room" and "dormitory" (ignore spaces). However,
"the" and "thee" are not anagrams, since "the" only has a single "e" whereas
"thee" has two "e" characters (spaces can occur zero, or multiple times, however.)

Given a list of words as strings, you should return another list of strings,
each containing words that are mutual anagrams.

Each string of the output should be a single group of anagarms joined with commas.

Within an output string, the expression should be sorted lexicographically.
If a group contains only a single element, output that one-element group
as a single string. And the string should be also output in lexicographical
order.  Given e.g.:
```
pear
amleth
dormitory
tinsel
dirty room
hamlet
listen
silnet
```
... the output would be:
```
amleth,hamlet
dirty room,dormitory
listen,silnet,tinsel
pear
```

## Solution
```php
<?php

$input = file_get_contents("php://stdin");

$lines = explode("\n", $input);

function getAnagramValue($word) {
	$word = str_replace(' ', '', $word);
	$word = strtolower($word);
	return count_chars($word, 1);
}

function getAnagrams($word, array $wordlist) {
	$retval = array();
	foreach ($wordlist as $candidate) {
		if (getAnagramValue($word) == getAnagramValue($candidate)) {
			$retval[] = $candidate;
		}
	}
	return $retval;
}

$anagrams = array();
foreach ($lines as $word) {
    if (empty($word)) {
        continue;
    }
	$anagrams[] = getAnagrams($word, $lines);
}

$sorted_anagrams = array();
foreach ($anagrams as $word => $candidates) {
	sort($candidates);
	$sorted_anagrams[] = implode(",", $candidates);
}

$sorted_anagrams = array_unique($sorted_anagrams);
sort($sorted_anagrams);

foreach ($sorted_anagrams as $words) {
    fwrite(STDOUT, $words . "\n");    
}
```