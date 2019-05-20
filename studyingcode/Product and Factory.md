# c++[Classes and Objects]Product and Factory

### 在软件设计中，一个对象的创建可能没有它看上去那么容易。比如课程管理系统中，一个课程的创建依赖于许多业务逻辑。某些情况下，将对象的创建和使用分离开来，是一个不错的选择，这让我们可以更优雅地组织代码，降低各模块的耦合性。我们将使用Product和Factory的概念：

### * 当客户端需要某个Product时，并不直接拿到它，而是通过一个Factory拿到
### * 只有Factory关心如何创建这个Product，而客户端无需关心
### * 客户端拿到Product，即可使用它支持的各种方法

~~~
#include <iostream>
using namespace std;
class Laptop{
	public:
		Laptop(){}
		virtual ~Laptop(){}
		virtual void compileCppProgram()=0;
};
class MobilePhone{
	public:
		MobilePhone(){}
		virtual ~MobilePhone(){}
		virtual void sendShortMessage()=0;
};
class XiaomiLaptop:public Laptop{
	public:
		XiaomiLaptop(){}
		virtual~XiaomiLaptop(){}
		virtual void compileCppProgram();
};
void XiaomiLaptop::compileCppProgram(){
	cout << "Xiaomi Laptop compiles a cpp program."<<endl;;
}
class AppleLaptop:public Laptop{
	public:
		AppleLaptop(){}
		virtual~AppleLaptop(){}
		virtual void compileCppProgram();
};
void AppleLaptop::compileCppProgram(){
	cout << "Apple Laptop compiles a cpp program."<<endl;;
}
class XiaomiMobilePhone:public MobilePhone{
	public:
		XiaomiMobilePhone(){}
		virtual~XiaomiMobilePhone(){}
		virtual void sendShortMessage();
};
void XiaomiMobilePhone::sendShortMessage(){
	cout << "Xiaomi MobilePhone sends a short message."<<endl;
}
class AppleMobilePhone:public MobilePhone{
	public:
		AppleMobilePhone(){}
		virtual~AppleMobilePhone(){}
		virtual void sendShortMessage();
};
void AppleMobilePhone::sendShortMessage(){
	cout << "Apple MobilePhone sends a short message."<<endl;
}
//Product.hpp 使用纯虚函数



class Factory{
	public:
		Factory(){}
		virtual~Factory(){}
		virtual Laptop* produceLaptop() = 0;
		virtual MobilePhone* produceMobilePhone() = 0;
};
class AppleFactory:public Factory{
	public:
		AppleFactory() {}
		virtual~AppleFactory() {}
		virtual Laptop* produceLaptop();
		virtual AppleMobilePhone* produceMobilePhone();
};
Laptop* AppleFactory::produceLaptop(){
	Laptop* p = new AppleLaptop;
	return p;
}
AppleMobilePhone* AppleFactory::produceMobilePhone(){
	AppleMobilePhone* p = new AppleMobilePhone;
	return p;
}
class XiaomiFactory:public Factory{
	public:
		XiaomiFactory(){}
		virtual~XiaomiFactory(){}
		virtual Laptop* produceLaptop();
		virtual MobilePhone* produceMobilePhone();
};
Laptop* XiaomiFactory::produceLaptop(){
	Laptop* p = new XiaomiLaptop;
	return p;
}
MobilePhone* XiaomiFactory::produceMobilePhone(){
	MobilePhone* p = new XiaomiMobilePhone;
	return p;
}
//Factory.hpp 同样使用纯虚函数



void test() {
  Factory* factory = NULL;
  int choose;
  cin >> choose;

  switch (choose) {
    case 0:
      factory = new AppleFactory();
      break;
    case 1:
    default:
      factory = new XiaomiFactory();
      break;
  }

  Laptop* laptop = factory->produceLaptop();
  MobilePhone* phone = factory->produceMobilePhone();

  laptop->compileCppProgram();
  phone->sendShortMessage();

  delete laptop;
  delete phone;

  delete factory;
}

int main() {
  test();
  return 0;
}
~~~
### 标准测试
~~~
Input0:
0

Output0:
Apple Laptop compiles a cpp program.
Apple MobilePhone sends a short message.

/*======*/
Input1:
1

Output1:
Xiaomi Laptop compiles a cpp program.
Xiaomi MobilePhone sends a short message.
~