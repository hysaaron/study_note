# C++ 学习笔记
0. 注意不同类型变量之间的运算与赋值。运算g++会报错，但赋值不会。如float赋值给double的数值是错误的。
1. 模板类所有函数需放在一个.h中，不要分开（如定义在.h，实现在.cpp中）。[https://stackoverflow.com/questions/12772103/undefined-reference-to-function-c]
2. vector容器定点删除用erase()，容器长度会随之而变，当前iterator也会直接指向后面的数据。但当删除最后一个元素时，iterator无法指向后面的数据（因为是end()）。