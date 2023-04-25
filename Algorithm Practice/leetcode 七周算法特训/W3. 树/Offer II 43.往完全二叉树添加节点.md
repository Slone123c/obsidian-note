
```go
type CBTInserter struct {  
   root      *TreeNode  
   candidate []*TreeNode  
}  
  
func Constructor(root *TreeNode) CBTInserter {  
   q := []*TreeNode{root}  
   candidate := []*TreeNode{}  
   for len(q) > 0 {  
      node := q[0]  
      q = q[1:]  
      if node.Left != nil {  
         q = append(q, node.Left)  
      }  
      if node.Right != nil {  
         q = append(q, node.Right)  
      }  
      if node.Left == nil || node.Right == nil {  
         candidate = append(candidate, node)  
      }  
   }  
   return CBTInserter{root, candidate}  
}  
  
func (c *CBTInserter) Insert(val int) int {  
   child := &TreeNode{Val: val}  
   node := c.candidate[0]  
   if node.Left == nil {  
      node.Left = child  
   } else {  
      node.Right = child  
      c.candidate = c.candidate[1:]  
   }  
   c.candidate = append(c.candidate, child)  
   return node.Val  
}  
  
func (c *CBTInserter) Get_root() *TreeNode {  
   return c.root  
}
```