Intuition
- It is a matrix **block composition**: 
	- the rightmost element in the chain is the innermost block. 
	- the leftmost matrix are the block coefficients


### Distributive $(A + B)\bigotimes C = A\bigotimes C + B\bigotimes C$  
   - Apparent if you look at an element of the complete matrix $(A + B) \bigotimes C$ 
### Associative $(A \bigotimes B) \bigotimes C = A \bigotimes (B \bigotimes C)$ 
   - Think of how each innermost block is cloned and go from there.
### Mixed Product $(A \bigotimes B)(C \bigotimes D) = AC \bigotimes BD$ 
   - Write down each block structure in the lefthand side
   - Do a block matrix product to get the resultant righthand side 
### Vector product to create a matrix can be expressed as a Kronecker product
   $ba^T = b \bigotimes a^T$    

#math/matrix