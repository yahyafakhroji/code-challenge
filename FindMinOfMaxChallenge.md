## Question

Find out the minimum value of the maximum value of each nested array given the following structure.

```Typescript
// this is the input
const values: number[][] = [
	[1,2,3,4,5],
	[3,4,5,6,7],
	[6,7,8,9,10]
]
```

## Answer
```Typescript
// Function to find the minimum value of the maximum value in nested arrays
const findMinOfMax = (arr: number[][]): number => {
  const maxValues: number[] = arr.map(innerArr => Math.max(...innerArr));
  return Math.min(...maxValues);
};

// Call the function with the provided input
const result = findMinOfMax(values); // Output 5

console.log(`The minimum value of the maximum values is: ${result}`);
```

## Summary
This code defines a function `findMinOfMax` that takes a 2D array as input, calculates the maximum value for each inner array using `Math.max`, and then finds the minimum value of these maximum values using `Math.min`. The result is printed to the console. In this case, the output will be the minimum value of the maximum values of each nested array in the provided values array.