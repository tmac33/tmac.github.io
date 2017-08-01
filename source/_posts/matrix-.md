title: 逆矩阵(review)
date: 2017-07-03 03:25:24
categories: 基础
tags: [线性代数]
comments: true
---

![](http://osej1thz9.bkt.clouddn.com/static/images/matrix0.jpg)

<!-- more -->

# 内容
计算矩阵的逆矩阵意味着从矩阵首先得是一可逆矩阵（矩阵不一定是可逆的）。首先，为了可逆，矩阵必须是一个方形矩阵（它具有与列为例如2x2,3x3,4x4等一样多的行），并且矩阵的行列式必须不同于零。任何具有零行列式的矩阵都被称为是单数的（意味着它不是可逆的）。为了计算矩阵M的逆，我们将写入M，并且在其旁边写入单位矩阵（一个单位矩阵是一个方形矩阵，其中一个对角线和另一个零）。我们说，我们通过身份增加M。然后我们将减少这个增强（或相邻）的矩阵。

![](http://osej1thz9.bkt.clouddn.com/static/images/matrix1.png)

在开始之前，请记住矩阵可以被看作是可以使用所谓的行基本操作来解决的线性方程组。行基本操作具有保留由矩阵设置的解的属性。有三种这样的操作：您可以交换矩阵的行（操作1），将行的每个系数乘以非零常数（操作2），并将行自身与另一行的倍数替换为一行（操作3）。这些示例使用以下示例（行切换，行乘法和行相加）：

![](http://osej1thz9.bkt.clouddn.com/static/images/matrix2.png)

在第二个例子中，我们简单地将行1的所有系数乘以1/2，将行3的系数乘以2.在第三个例子中，我们将行1的系数加到行2的系数。 高斯法是使用这些基本行操作来将增强矩阵的左边内部的4×4矩阵变换为单位矩阵（我们说M是行减少）。通过对增强矩阵右侧的4x4单位矩阵执行相同的行操作，获得逆矩阵。

# 步骤1：设置行，使枢轴不同于零

使矩阵对角线的系数称为矩阵的枢轴。

如前所述，矩阵求逆过程的目标是使用行基本操作将每列的枢轴设置为1，将所有其他系数设置为0（在此过程结束时，我们将获得标识矩阵）。为了实现这一点，最好是从左边开始逐行排列。从左到右，保证当我们从列到列进行时，我们不会更改已经排列的列的值。

![](http://osej1thz9.bkt.clouddn.com/static/images/matrix3.png)

我们首先要检查当前列（正在处理的列）的枢轴系数的值。为了使我们的技术工作，这个值必须不等于零。如果它不同于零，那么我们可以直接转到第二步。如果它等于零，则我们需要在该列的矩阵中找到另一行，该列的值不等于零，并交换这两行（操作1）。但是，多于一行可能具有不同于零的值？那么我们应该选择哪一个？我们将拾取绝对值最高的行。

![](http://osej1thz9.bkt.clouddn.com/static/images/matrix4.gif)

在右边的例子中，我们来看第二列的枢轴系数。因为该系数的值为零，所以我们用第二列的绝对值最大的行（在本例中为第3行）交换第2行。

我们使用高斯 - 约旦消除方法将原始矩阵转换为单位矩阵，同时在另一个矩阵（mat）上执行相同的操作，在矩阵的开始（第3行）被设置为身份矩阵（Matrix类构造函数默认将矩阵设置为单位矩阵）。在这个过程结束时，我们的原始矩阵用第二个矩阵的系数（最后的代码中的第39行）设置。如果我们找不到另一个值，那么这个矩阵不能被反转并且是奇异的（第11行）。

![](http://osej1thz9.bkt.clouddn.com/static/images/matrix5.gif)

``` c++
Matrix<T, N> & invert() 
{ 
    Matrix<T, N> mat; 
    for (unsigned column = 0; column < N; ++column) { 
        // Swap row in case our pivot point is not working
        if (m[column][column] == 0) { 
            size_t big = column; 
            for (unsigned row = 0; row < N; ++row) 
                if (fabs(m[row][column]) > fabs(m[big][column])) big = row; 
            // Print this is a singular matrix, return identity ?
            if (big == column) fprintf(stderr, "Singular matrix\n"); 
            // Swap rows                               
            else for (unsigned j = 0; j < N; ++j) { 
                std::swap(m[column][j], m[big][j]); 
                std::swap(mat.m[column][j], mat.m[big][j]); 
            } 
        } 
        ... 
    } 
} 
```
# 步骤2：将列中的每一行设置为0

![](http://osej1thz9.bkt.clouddn.com/static/images/matrix6.png)

如果我们正在处理的当前列具有有效的枢轴系数，那么我们可以继续下一步。我们将减少列的每个系数（除了我们现在不会碰到的枢轴系数）为零。在英语中，这不会很有意义，但在这里。让我们调用'm'，我们要减少到零的当前有效（对于当前列/行）。我们将从当前行的每个系数（操作2和3）中减去与行的每个系数相关的索引与当前列的索引相同的m。如果m本身除以枢轴系数值（第4行），该技术将起作用。在下面的例子中说明了一个系数。第二列是当前列。我们要减少当前列的第一个系数（行0）（4.3）为零。对于第一行的每个系数（例如C0j），我们从第二行获取相应的系数（C1j）（因为我们正在处理第二列），将该系数乘以我们要减少的系数（C02）除以通过来自第二列（C12）的枢轴系数，并从C0j中减去结果数。

C++代码：

``` c++
// Set each row in the column to 0  
for (unsigned row = 0; row < N; ++row) { 
    if (row != column) { 
        T coeff = m[row][column] / m[column][column]; 
        if (coeff != 0) { 
            for (unsigned j = 0; j < N; ++j) { 
                m[row][j] -= coeff * m[column][j]; 
                mat.m[row][j] -=  coeff * mat.m[column][j]; 
            } 
            // Set the element to 0 for safety
            m[row][column] = 0; 
        } 
    } 
} 
```
注意我们如何将相同的操作应用到增强矩阵的右侧（第8行）。

# 步骤3：将所有枢轴系数缩放为1

在步骤2结束时，所有的矩阵系数应为0，除了我们需要设置为1的枢轴系数。为此，我们只需要通过自己的值来缩放系数。类似于我们在步骤2中做的，我们将循环遍历每一行，然后循环每一列，并将当前系数除以当前行的枢轴系数值：
``` c++

for（unsigned row = 0; row <N; ++ row）{ 
    for（unsigned column = 0; column <N; ++ column）{ 
        mat.m [row] [column] / = m [row] [row] ; 
    } 
}
```

最后，我们只是将矩阵的结果与我们右边的矩阵（mat在代码中）结合起来。我们使用高斯 - 约旦消除技术来反转矩阵。

# 以下是方法的完整代码：

``` c++

Matrix<T, N> & invert() 
{ 
    Matrix<T, N> mat; 
    for (unsigned column = 0; column < N; ++column) { 
        // Swap row in case our pivot point is not working
        if (m[column][column] == 0) { 
            unsigned big = column; 
            for (unsigned row = 0; row < N; ++row) 
                if (fabs(m[row][column]) > fabs(m[big][column])) big = row; 
            // Print this is a singular matrix, return identity ?
            if (big == column) fprintf(stderr, "Singular matrix\n"); 
            // Swap rows                               
            else for (unsigned j = 0; j < N; ++j) { 
                std::swap(m[column][j], m[big][j]); 
                std::swap(mat.m[column][j], mat.m[big][j]); 
            } 
        } 
        // Set each row in the column to 0  
        for (unsigned row = 0; row < N; ++row) { 
            if (row != column) { 
                T coeff = m[row][column] / m[column][column]; 
                if (coeff != 0) { 
                    for (unsigned j = 0; j < N; ++j) { 
                        m[row][j] -= coeff * m[column][j]; 
                        mat.m[row][j] -= coeff * mat.m[column][j]; 
                    } 
                    // Set the element to 0 for safety
                    m[row][column] = 0; 
                } 
            } 
        } 
    } 
    // Set each element of the diagonal to 1
    for (unsigned row = 0; row < N; ++row) { 
        for (unsigned column = 0; column < N; ++column) { 
            mat.m[row][column] /= m[row][row]; 
        } 
    } 
    *this = mat; 
    return *this; 
} 
```

