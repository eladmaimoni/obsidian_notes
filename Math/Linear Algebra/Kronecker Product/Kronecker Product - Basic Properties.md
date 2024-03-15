Intuition
- It is a matrix **block composition**: 
	- the rightmost element in the chain is the innermost block. 
	- the leftmost matrix are the block coefficients

## [Kronecker](https://www.statlect.com/matrix-algebra/Kronecker-product-properties)
### 1. Distributive $(A + B)\bigotimes C = A\bigotimes C + B\bigotimes C$  
   - Apparent if you look at an element of the complete matrix $(A + B) \bigotimes C$ 
### 2. Associative $(A \bigotimes B) \bigotimes C = A \bigotimes (B \bigotimes C)$ 
   - Think of how each innermost block is cloned and go from there.
### 3. Mixed Product $(A \bigotimes B)(C \bigotimes D) = AC \bigotimes BD$ 
   - Write down each block structure in the lefthand side
   - Do a block matrix product to get the resultant righthand side 

## [Vec](https://www.statlect.com/matrix-algebra/vec-operator)
### 4. Vector product to create a matrix can be expressed as a Kronecker product
   $ba^T = b \bigotimes a^T$

### 5. $vec\,ab^T = b \bigotimes a$ 
### 5. $(vec\,A)^Tvec\,B = trace(A^TB)$ 
this is simply dot product of all the matching columns and summing them
### 5. $(A \bigotimes B) vec(C) = vec(BCA^T)$ 
- 


#math/matrix 