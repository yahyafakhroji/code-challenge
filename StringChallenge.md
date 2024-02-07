## Question
Have the function `StringChallenge(strArr)` read the array of strings stored in strArr, which will contain two elements, the first will be a positive decimal number and the second element will be a binary number. Your goal is to determine how many digits in the binary number need to be changed to represent the decimal number correctly (either 0 change to 1 or vice versa). For example: if strArr is `["56", "011000"]` then your program should return 1 because only 1 digit needs to change in the binary number (the first zero needs to become a 1) to correctly represent 56 in binary.

## Answer
```Javascript
function StringChallenge(strArr) {
  const [decimal, binary] = strArr;
  const decToBin = Number(decimal).toString(2);

  let count = 0;

  for (let i = 0; i < binary.length; i++) {
    if (binary[i] !== decToBin[i]) {
      count++;
    }
  }

  return count;
}

// Test cases
console.log(StringChallenge(["5624", "0010111111001"])) // Output 2

console.log(StringChallenge(["44", "111111"])) // Output 3
```

## Summary
This code defines a function called `StringChallenge` that takes an array of two strings as input. The first string is a decimal number and the second string is a binary number. The function returns the number of differences between the two representations of the number.

The function works by first converting the decimal number to a binary string. Then, it iterates over the binary string and compares each digit to the corresponding digit in the input binary string. If the digits are different, the function increments a counter. Finally, the function returns the counter value.

For example, if the input is `["5624", "0010111111001"]`, the function would convert the decimal number 5624 to the binary string `"101100110001"`. Then, it would iterate over the binary string and compare each digit to the corresponding digit in the input binary string. The digits would be different at positions 0, 3, 8, and 11, so the counter would be incremented 4 times. Finally, the function would return 4.