### Matlab笔记
数字计算，可视化编程，高级编程语言和交互环境
MathWorks


矩阵操作
绘制功能和数据
实现算法
和其他编程语言交互
创建用户界面
数据分析
开发算法
创建模型和应用程序
* % 注释
* %{ %} 连续注释
* save mymat
* load mymat
#### 在Matlab中，每个变量都是数组或矩阵
* who
* whos
* ...
* MATLAB默认显示四位小数，短格式 
* format long; format short; 
* format bank;
* format long e; format short e;
* format rat;
#### 创建向量
* r = [1 2 3 4 ]; 空格或者逗号
* r = [1; 2; 3; 4];
* r = [2 3 4; 4 5 6]; 二维数组
* shift + enter 换行
#### Matlab命令

#### .m 脚本 函数
* 脚本不接受输入，不返回任何输出，它们对工作空间中的数据进行操作
* 函数可以接受输入和返回的输出，内部变量是函数的局部变量
* 脚本 --- 包括多个连续的MATLAB命令行和函数调用。 可以通过在命令行中键入其名称来运行脚本

