---
layout: docpost
title: Validating a heron barcode
date_published: 2020-03-19 16:00:00 +0000
date_modified:  2020-03-20 12:00:00 +0000
author: rl15 sanger.ac.uk
maintainer: khelwood
---

The barcode is made up of a prefix, followed by a hyphen, followed by a hexadecimal string, all in capitals.
The prefix should be the one correct for the location the barcode is being used.
The last digit of the hexadecimal string is a checksum calculated based on the preceding characters.

## To validate the checksum

* Take the non-checksum part of the hex. This is all of it except the last digit.
* Starting from the end and working back towards the beginning, add up the value of the hex digits in even positions. (A)
* Separately, add up the values of the hex digits in odd positions, and multiply the total by 3. (B)
* Add up the two numbers A and B.
* Calculate the remainder when the total is divided by 16.
* If the result is nonzero, subtract it from 16.
* Convert the number to hexadecimal.
That should be the value of the checksum character.

### Example 1

`SANG-4A996`

The checksum is calculated from 4A99.

* The digits in even positions (counting from the end) are 9 and A.
* The digits in odd positions (counting from the end) are 9 and 4.

```
TOTAL = (9 + A) + (9 + 4) * 3 = 4A HEX (58 DEC)
```

* The remainder when divided by 16 is A HEX (10 DEC).
* Subtract that from 16 to give 6.
* 6 is the value of the checksum.

### Example 2

`NIRE-102B1B`

The checksum is calculated from 102B1.

* The digits in even positions (counting from the end) are 1, 2 and 1.
* The digits in odd positions (counting from the end) are B and 0.

```
TOTAL = (1 + 2 + 1) + (B + 0) * 3 = 25 HEX = 37 DEC
```

* The remainder when divided by 16 is 5.
* Subtract that from 16 to give B (11 DEC).
* B is the value of the checksum.

```
    // This Java code is equivalent to the description above, though
    // not following exactly the same steps.

    private static int hexCharToInt(char ch) {
        if (ch>='0' && ch<='9') return ch-'0';
        if (ch>='A' && ch<='F') return ch-'A'+10;
        throw new IllegalArgumentException("Illegal hex char: "+ch);
    }
    private static char intToHexChar(int n) {
        if ((n&0xf)!=n) {
            throw new IllegalArgumentException("Hex char out of range: "+n);
        }
        if (n<10) return (char) ('0'+n);
        return (char) ('A'+n-10);
    }

    // hex is the hex part of the barcode string (without the checksum)
    private static char calculateChecksum(String hex) {
        final int l = hex.length();
        int sum = 0;
        for (int i = 0; i < l; ++i) {
            int v = hexCharToInt(hex.charAt(l-1-i));
            if ((i&1)!=0) {
                v *= 3;
            }
            sum += v;
        }
        return intToHexChar((-sum)&0xf);
    }
```
