## Problem
Identify whether there exists a pair of numbers in an array such that
their sum is equal to **N**.

Input:
The first line contains one integer *N*, which is the sum we are trying to find.
The second line contains one integer *M*, which is the length of the array.
This is followed by M lines each containing one element of the array.

Output:
Output 1 if there exists a pair of numbers in the array such that their
sum equals N. If such a pair does not exist, output 0.

Sample Input:
```
66
10
18
11
21
28
31
38
40
55
60
62
```
Sample Output:
```
1
```

## Solution

```php
<?php
    
$input = file_get_contents("php://stdin");

$lines = explode("\n", $input);
$lines = array_map('intval', $lines);

$sum = array_shift($lines);
$len = array_shift($lines);

$found = false;
foreach ($lines as $num) {
    $diff = $sum - $num;
    if (in_array($diff, $lines)) {
        $found = true;
        break;
    }
}

fwrite(STDOUT, intval($found));
```