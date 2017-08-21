# Vim cheat sheet

[TOC]

# delete,copy, move

**command** | **Description**
:---:        | :---
**delete**  | 
`:3d`         | delete the 3rd line
`:2,5d`, `:2,5de`,`:2,5 d`, `:2,5 de`    | delete line 2-5
`10dd`       | delete 10 lines from the current line (current line included)
**copy** |
`2yy` | copy 2 lines from the current line (current line included)
`p` | paste the copied contents to 
`:6,9 co 12` | copy line 6-9 after line 12
`ma` + `mb` + `mc` then `'a, 'b co 'c`| copy contents from mark `a` to mark `b` after mark `c`.
**move/cut** |
`ma` + `mb` + `mc` then `'a, 'b m 'c`| move contents from mark `a` to mark `b` after mark `c`.



