```c#
using system;

namespace Hello
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello, World!");
        }
    }
}
```

```c#
// Main函数开始执行，必须声明为静态
// 根据返回类型和入口参数不同，Main函数分为以下几种形式

static void Main()
    
static void Main(string[] args)
    
static int Main()
    
static int Main(string[] args)
    
// Main函数有两种返回类型: void int。
// Main函数可以没有入口参数，也可以接受字符串数组作为参数。
```

```markdown
变量：分配一个真实的内存地址
常量： 不可改变 const
数据类型：定义了数据的性质、表示和存储空间的结构
    值类型：用来存储实际值。
    引用类型：指向它所引用的值的地址
    
    值类型分为：
    	简单类型：
    		整数类型：
    			有符号整数：sbyte(8), short(16), int(32), long(64);
             	 无符号整数：byte(8), ushort(16), uint(32), ulong(64);
             浮点类型：
             	 单精度浮点型：float(32), 7位小数精度;
             	 双精度浮点型: double(64), 15位小数精度;
             	 默认double, float f = 2.3f;
             十进制类型：
             	 decimal(128) 29位精度
             布尔类型：
             	 bool(8) true, false;
             字符类型：
             	 单个字符， 数字，英文，表达符号，中文等;
             	 采用Unicode标准字符集
             	 char(16) 0~65535范围内以双字节编码的任意符号
             	 
             	 ！ C#字符属于基本数据类型，字符串属于对象， char  a = 'a'; char a = ' \' ';
             	 \b 退格 \r回车 \f换页 
             
         
```

```c#
// 枚举类型
//仅限于整形
enum Season {Spring, Summar = 2, Autumn, Winter};
Season current = Season.Summar;

// Season current = (Season)2;

// 结构类型
//复合数据类型
//一个结构类型变量内所有数据可作为一个整体进行处理

struct Cube
{
    public int length;
    public int age;
    public double score;
    public string id;
}

Cube cb;
cb.length = 11;
cb.age = 21;
Console.WriteLine(cb.age);
```

```c#
// 隐含类型
//var 声明任何类型的局部变量
//仅限于本地变量

//！ error
var x; //没有赋值
var z = null; //不可为空
```

