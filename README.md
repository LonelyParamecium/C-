#include<iostream>
using namespace std;


class MyInteger
{
public:
	friend ostream& operator<<(ostream& cout, MyInteger p);
	MyInteger();
	MyInteger& operator++();     //++前置，必须返回引用
	MyInteger operator++(int);   //后置+++ 必须返值，int占位参数，防止与++前置重定义；
	MyInteger& operator--();    //--前置，使用引用返回
	MyInteger operator--(int);  //后置--，返回值
	
private:
	int m_a;
	int m_b;
};
MyInteger::MyInteger()
{
	m_b = 0;
	m_a = 0;
}
MyInteger& MyInteger::operator++()  //++前置必须返回一个引用
{
	++m_a;
	++m_b;
	return *this;   //返回的是一个当前的指针，返回值的话，做++（++）无法操作
}
MyInteger MyInteger::operator++(int)
{
	MyInteger temp=*this;
	m_a++;
	m_b++;
	return temp;
}
MyInteger& MyInteger:: operator--()
{
	--m_a;
	--m_b;
	return *this;
}
MyInteger MyInteger::operator--(int)
{
	MyInteger temp = *this;
	m_a--;
	m_b--;
	return temp;
}

ostream& operator<<(ostream& cout, MyInteger p)   
{
	cout << "m_a=" << p.m_a << "  " << "m_b=" << p.m_b;
	return cout;
}
void test01()
{
	MyInteger p1;
	//cout << ++(++p1) << endl;
	MyInteger p2;
	//cout <<(p2++) << endl;  //没有写一个temp值，就不支持链式编程，就不能加了一次再加一次  
	//cout << p2 << endl;
	//cout << --(--p1) << endl;
	cout << (p2--) << endl;
	cout << p2;

}
int main()
{
	test01();
	system("pause");
	return 0;
}
