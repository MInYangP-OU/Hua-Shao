C#中数组，ArrayList，List都能够存储**一组对象**

------

### 数组

​	最早出现，内存连续，索引速度非常快，而且赋值与修改元素简单。

```c#
int[] strList = new int[3]{1,2,3};
strList[2] = 5;

```

​	不足：

* 两个数据间插入麻烦
* 声明数组必须指定数组长度（过长浪费，过短溢出）（声明时不知道长度，麻烦）

### ArrayList(最先用来克服数组缺陷)

 命名空间System.Collections下（必须进行引用）

继承了IList接口，提供了数据存储和检索

ArrayList对象的大小是按照其中存储的数据来动态扩充与收缩的



```c#
ArrayList arrayList = new arrayList();

//新增数据
arrayList.Add("cds");
arrayList.Add(123);

//修改数据
arrayList[1] = "as";

//移除数据
arrayList.RemoveAt(0);

//插入数据
arrayList.Insert(0,"qw");
```

ArrayList好像是解决了数组中所有的缺点?

ArrayList中插入不同类型的数据 **==>**所有插入其中的数据当作为**object类型**来处理**==>**报类型不匹配的错误，也就是**ArrayList不是类型安全** **||**存储或检索值类型时通常发生装箱和拆箱箱操作，带来很大的**性能耗损**。



### 泛型List<T>

在声明List集合时，我们同时需要为其声明List集合内**数据的对象类型**。

```c#
List<int> list = new List<int>();
```

[参考]: https://blog.csdn.net/zhang_xinxiu/article/details/8657431

