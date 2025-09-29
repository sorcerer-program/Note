类这只是堆数据进行分组的方法
class 本质上是一种 type
```cpp
#include <iostream>
#define LOG(X) std::cout << X << std::endl;

class Player {
public:    // public 使得类的成员可以被外部访问
	int x, y;
	int speed;

	void Move(int xa, int ya) {
		x += xa * speed;
		y += ya * speed; 
	}
};

int main() {
	Player player;
	//player.x = 5;   这样写是不行的，存在可见性，默认情况下，类的可见度是私有的
	player.Move(1, -1);

	std::cin.get();
}
```
从本质上讲，类允许我们对变量进行分组，并为这些变量添加方法，
语法糖

## classes vs structs
类默认私有，而结构体默认公共

## static
在class或者struct里面，外面，一共两种情况

类外的static修饰的符号在link阶段是局部的，也就是它只对它的编译单元（.obj）可见

而类或结构体里面的static便士这部分内存是这个类的所有实例共享的，静态的变量只会有一个实例，静态方法没哟this

类外的
加上 extern 它会在另外的编译单元里找s_Variable的定义

类里面的
意味着这个类的所有实例中，这个变量只有一个实例

静态局部（local static）变量允许我们声明一个变量，它的生命周期是整个程序的生存期，但是作用域被限制。
```cpp
void Function() {
	static int i = 0;
	i++;
	std::cout << i << std::endl;
}

int main() {
	Function();
	Function();
	std::cin.get();
}
```
第一次调用这个函数的时候，i 被初始化为0，后续调用不会再创建一个新的变量。
这里很像全局变量的作用，不一样的是不是什么地方都能够访问到
## 虚函数
 虚函数可以让我们在子类中重写方法
 虚函数引入了一种要动态分派的东西，一般通过虚表来实现编译，虚表就是一个包含类中所有虚函数映射的列表，通过虚表，我们可以再运行时找到正确的被重写的函数
 如果想要重写一个函数，必须把基类中的原函数设置为虚函数
 `virtual string get_name() {return "Hello, world !";}`
 新标准允许给被重写的函数用 “override” 关键字标记（不是必须的，但是写上可读性更好）
 `string get_name() override {return "OVERRIDE";}`
 虚函数并不是没有成本的，有两种虚函数运行时的花费，一种是需要额外的内存来存储虚表，这样我们就可以分配到正确的函数，基类里还有一个指针成员指向虚表，还有就是每次调用虚函数的时候，我们必须遍历虚表去找到最终运行的函数。

有一种特殊的虚函数：纯虚函数
c++中的纯虚函数的本质上和其他语言中的抽象方法和接口相同