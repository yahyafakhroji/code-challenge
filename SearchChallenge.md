## Question
Have the function `SearchingChallenge(str)` take str which will be a string and return the longest pattern within the string. A pattern for this challenge will be defined as: if at least 2 or more adjacent characters within the string repeat at least twice. So for example "aabecaa" contains the pattern aa, on the other hand "abbbaac" doesn't contain any pattern. Your program should return yes/no pattern/null. So if str were "aabejiabkfabed" the output should be yes abe. If str were "123224" the output should return no null. The string may either contain all characters (a through z only), integers, or both. But the parameter will always be a string type. The maximum length for the string being passed in will be 20 characters. If a string for example is "aa2bbbaacbbb" the pattern is "bbb" and not "aa". You must always return the longest pattern possible.

```
Examples
Input: "da2kr32a2"
Output: yes a2
Input: "sskfssbbb9bbb"
Output: yes bbb
```

## Answer
```Javascript
// This is a special comment for a keyword requirement.

// Define a function that finds the longest repeating pattern in a given string.
function SearchingChallenge(str) {
    // Check if the input is number
    if (str.match(/^\d+$/)) {
        return "no null"; // no pattern
    }

    // Start with no known longest pattern.
    let longestPattern = null;

    // Loop through each character in the string.
    for (let i = 0; i < str.length; i++) {
        // Nested loop to form all possible substrings starting from the current character.
        for (let j = i + 1; j < str.length; j++) {
            // Extract the current substring.
            const substring = str.substring(i, j);

            // Count how many times this substring repeats in the string.
            const occurrences = (str.match(new RegExp(substring, 'g')) || []).length;

            // Check if the substring repeats at least twice and is longer than the current longest pattern.
            if (occurrences >= 2 && (!longestPattern || substring.length > longestPattern.length)) {
                // Update the longestPattern if conditions are met.
                longestPattern = substring;
            }
        }
    }

    // If a longest pattern is found, return "yes" followed by the pattern. Otherwise, return "no null".
    if (longestPattern) {
        return `yes ${longestPattern}`;
    } else {
        return 'no null';
    }
}

// Examples
// Call the function with example inputs and display the results in the console.
console.log(SearchingChallenge("da2kr32a2"));
console.log(SearchingChallenge("sskfssbbb9bbb"));

```