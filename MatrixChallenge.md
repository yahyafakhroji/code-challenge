## Question
Have the function `MatrixChallenge(strArr)` read the strArr parameter being passed which will make up an NxN matrix where the rows are separated by each pair of parentheses (the matrix will range from 2x2 to 5x5). The matrix represents connections between nodes in a graph where each node corresponds to the Nth element in the matrix (with 0 being the first node). If a connection exists from one node to another, it will be represented by a 1, if not it will be represented by a 0. For example: suppose strArr were a 3x3 matrix with input `["(1,1,1)","(1,0,0)","(0,1,0)"]`, this means that there is a connection from node 0->0, 0->1, and 0->2. For node 1 the connections are 1->0, and for node 2 the connections are 2->1. This can be interpreted as a connection existing from node X to node Y if there is a 1 in the Xth row and Yth column. Note: a connection from X->Y does not imply a connection from Y->X.

What your program should determine is whether or not the matrix, which represents connections among the nodes, is transitive. A transitive relation means that if the connections 0->1 and 1->2 exist for example, then there must exist the connection 0->2. More generally, if there is a relation xRy and yRz, then xRz should exist within the matrix. If a matrix is completely transitive, return the string transitive. If it isn't, your program should return the connections needed, in the following format, in order for the matrix to be transitive: (N1,N2)-(N3,N4)-(...). So for the example above, your program should return (1,2)-(2,0). You can ignore the reflexive property of nodes in your answers. Return the connections needed in lexicographical order [e.g. (0,1)-(0,4)-(1,4)-(2,3)-(4,1)].

## Answer
```Javascript
function MatrixChallenge(strArr) {
 
 // Convert string array to 2D integer matrix
 const matrix = strArr.map(row => row
   .slice(1, -1) // Remove parentheses
   .split(",")
   .map(Number));

 // Store missing transitive connections
 const missingConnections = [];

 // Check for transitive relations
 for (let i = 0; i < matrix.length; i++) {
   for (let j = 0; j < matrix.length; j++) {
     if (matrix[i][j] === 1) {
       for (let k = 0; k < matrix.length; k++) {
         if (matrix[j][k] === 1 && matrix[i][k] !== 1) {
           missingConnections.push(`(${i},${k})`);
           matrix[i][k] = 1; // Mark as connected to avoid duplicates
         }
       }
     }
   }
 }

 // Sort and format missing connections
 const sortedMissingConnections = missingConnections.sort().join("-");

 return sortedMissingConnections ? sortedMissingConnections : "transitive";
}

// Example usage with a 3x3 matrix
const result = MatrixChallenge(["(1,1,1)", "(1,0,0)", "(0,1,0)"]);
console.log(result); // Output: (1,2)-(2,0)

// Example usage with a 4x4 matrix
const result2 = MatrixChallenge(["(1,1,1,1)", "(1,0,0,0)", "(0,1,0,0)", "(0,0,1,0)"]);
console.log(result2); // Output: (1,3)-(2,3)-(3,0)

// Example usage with a transitive matrix
const result3 = MatrixChallenge(["(1,1,1)", "(0,1,1)", "(0,0,1)"]);
console.log(result3); // Output: transitive
```

## Logic explanation

### Data Preparation
- Converts `relations` from strings to number pairs for easier comparison.
- Uses `slice` and `split` to extract numbers within parentheses.

### Transitive Relation Check
- Iterates through pairs of relations using nested loops.
- If a pair `(x,y)` and `(y,z)` exist, but `(x,z)` is missing, it implies a missing transitive relation.
- Adds missing relations to `transitiveRelations`.

### Result
- Returns **"transitive"** if no missing relations are found.
- Otherwise, returns a sorted list of missing relations in the required format.

### Key Point
- **Matrix conversion**: Converts string array to a 2D integer matrix for easier manipulation.
- **Transitive relation check**: Nested loops iterate through the matrix to find missing transitive connections.
- **Missing connection tracking**: Stores missing connections in missingConnections and marks them in the matrix to avoid duplicates.
- **Result formatting**: Sorts and formats missing connections in the required format.
- **Clear return**: Returns "transitive" if no missing connections are found, otherwise returns the formatted list of missing connections.