+++
title = '记录一次C++报错'
date = 2025-03-16T20:30:36+08:00
draft = false
author = 'Butterblock233'
tags = ['C++']
categories = ["计算机"]
+++

前段时间做C++的练习，遇到了一个**非常混乱**的报错，在此记录一下。
# 错误复现
出错的代码是关于`std::map`的练习。
```cpp
#include <string>
#include <map>

class PhoneBook {
   public:
	void addContact( const std::string& name, const std::string& phoneNumber ) {
		// 添加联系人
		contacts.insert(name,phoneNumber); 
	}

   private:
	std::map<std::string,std::string> contacts;
};
```
编译后g++报错：
```bash
In file included from D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/map:63,
                 from ./blog_code.cc:1:
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_map.h: In instantiation of 'void std::map<_Key, _Tp, _Compare, _Alloc>::insert(_InputIterator, _InputIterator) [with _InputIterator = std::__cxx11::basic_string<char>; _Key = std::__cxx11::basic_string<char>; _Tp = std::__cxx11::basic_string<char>; _Compare = std::less<std::__cxx11::basic_string<char> >; _Alloc = std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >]':
./blog_code.cc:8:18:   required from here
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_map.h:944:38: error: no matching function for call to 'std::_Rb_tree<std::__cxx11::basic_string<char>, std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> >, std::_Select1st<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >, std::less<std::__cxx11::basic_string<char> >, std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > > >::_M_insert_range_unique(std::__cxx11::basic_string<char>&, std::__cxx11::basic_string<char>&)'
  944 |         { _M_t._M_insert_range_unique(__first, __last); }
      |           ~~~~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~
In file included from D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/map:62:
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h:1100:9: note: candidate: 'template<class _InputIterator> std::__enable_if_t<std::is_same<_Val, typename std::iterator_traits<_Iter>::value_type>::value> std::_Rb_tree<_Key, _Val, _KeyOfValue, _Compare, _Alloc>::_M_insert_range_unique(_InputIterator, _InputIterator) [with _Key = std::__cxx11::basic_string<char>; _Val = std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> >; _KeyOfValue = std::_Select1st<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >; _Compare = std::less<std::__cxx11::basic_string<char> >; _Alloc = std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >]'
 1100 |         _M_insert_range_unique(_InputIterator __first, _InputIterator __last)
      |         ^~~~~~~~~~~~~~~~~~~~~~
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h:1100:9: note:   template argument deduction/substitution failed:
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h: In substitution of 'template<class _InputIterator> std::__enable_if_t<std::is_same<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> >, typename std::iterator_traits< <template-parameter-1-1> >::value_type>::value, void> std::_Rb_tree<std::__cxx11::basic_string<char>, std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> >, std::_Select1st<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >, std::less<std::__cxx11::basic_string<char> >, std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > > >::_M_insert_range_unique(_InputIterator, _InputIterator) [with _InputIterator = std::__cxx11::basic_string<char>]':
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_map.h:944:31:   required from 'void std::map<_Key, _Tp, _Compare, _Alloc>::insert(_InputIterator, _InputIterator) [with _InputIterator = std::__cxx11::basic_string<char>; _Key = std::__cxx11::basic_string<char>; _Tp = std::__cxx11::basic_string<char>; _Compare =
std::less<std::__cxx11::basic_string<char> >; _Alloc = std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >]'
./blog_code.cc:8:18:   required from here
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h:1100:9: error: no type named 'value_type' in 'struct std::iterator_traits<std::__cxx11::basic_string<char> >'
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_map.h: In instantiation of 'void std::map<_Key, _Tp, _Compare, _Alloc>::insert(_InputIterator, _InputIterator) [with _InputIterator = std::__cxx11::basic_string<char>; _Key = std::__cxx11::basic_string<char>; _Tp = std::__cxx11::basic_string<char>; _Compare = std::less<std::__cxx11::basic_string<char> >; _Alloc = std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >]':
./blog_code.cc:8:18:   required from here
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h:1109:9: note: candidate: 'template<class _InputIterator> std::__enable_if_t<(! std::is_same<_Val,
typename std::iterator_traits<_Iter>::value_type>::value)> std::_Rb_tree<_Key, _Val, _KeyOfValue, _Compare, _Alloc>::_M_insert_range_unique(_InputIterator, _InputIterator) [with _Key = std::__cxx11::basic_string<char>; _Val = std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> >; _KeyOfValue = std::_Select1st<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >; _Compare = std::less<std::__cxx11::basic_string<char> >; _Alloc = std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >]'
 1109 |         _M_insert_range_unique(_InputIterator __first, _InputIterator __last)
      |         ^~~~~~~~~~~~~~~~~~~~~~
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h:1109:9: note:   template argument deduction/substitution failed:
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h: In substitution of 'template<class _InputIterator> std::__enable_if_t<(! std::is_same<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> >, typename std::iterator_traits< <template-parameter-1-1> >::value_type>::value), void> std::_Rb_tree<std::__cxx11::basic_string<char>, std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> >, std::_Select1st<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >, std::less<std::__cxx11::basic_string<char> >, std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > > >::_M_insert_range_unique(_InputIterator, _InputIterator) [with _InputIterator = std::__cxx11::basic_string<char>]':
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_map.h:944:31:   required from 'void std::map<_Key, _Tp, _Compare, _Alloc>::insert(_InputIterator, _InputIterator) [with _InputIterator = std::__cxx11::basic_string<char>; _Key = std::__cxx11::basic_string<char>; _Tp = std::__cxx11::basic_string<char>; _Compare =
std::less<std::__cxx11::basic_string<char> >; _Alloc = std::allocator<std::pair<const std::__cxx11::basic_string<char>, std::__cxx11::basic_string<char> > >]'
./blog_code.cc:8:18:   required from here
D:/Scoop/apps/gcc/13.2.0/include/c++/13.2.0/bits/stl_tree.h:1108:59: error: no type named 'value_type' in 'struct std::iterator_traits<std::__cxx11::basic_string<char> >'
 1108 |         __enable_if_t<!__same_value_type<_InputIterator>::value>
      |
```

clang++报错：
```bash
In file included from .\blog_code.cc:1:
In file included from D:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.43.34808\include\map:12:
D:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.43.34808\include\xtree:1265:33: error: cannot increment value of type
      'std::basic_string<char>'
 1265 |         for (; _First != _Last; ++_First) {
      |                                 ^ ~~~~~~
D:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.43.34808\include\xtree:1274:9: note: in instantiation of function template
      specialization 'std::_Tree<std::_Tmap_traits<std::basic_string<char>, std::basic_string<char>, std::less<std::basic_string<char>>,
      std::allocator<std::pair<const std::basic_string<char>, std::basic_string<char>>>, false>>::_Insert_range_unchecked<std::basic_string<char>,
      std::basic_string<char>>' requested here
 1274 |         _Insert_range_unchecked(_STD _Get_unwrapped(_First), _STD _Get_unwrapped(_Last));
      |         ^
.\blog_code.cc:8:12: note: in instantiation of function template specialization 'std::_Tree<std::_Tmap_traits<std::basic_string<char>,
      std::basic_string<char>, std::less<std::basic_string<char>>, std::allocator<std::pair<const std::basic_string<char>, std::basic_string<char>>>,
      false>>::insert<std::basic_string<char>>' requested here
    8 |                 contacts.insert( name, phoneNumber );
      |                          ^
1 error generated.
```


# 错误分析
我们先抛开编译器**莫名其妙**的报错，来看看代码出了什么问题。

我们可以发现问题出在这里：
```cpp
8		contacts.insert(name,phoneNumber); 
```
这里的`contacts`是一个`std::map`，而`insert()`方法期待接收参数`std::pair<std::string,std::string>`或两个迭代器`_Iter _First`,`_Iter _Last`，而实际传递的参数则是`std::string`和`std::string`，所以导致了**类型错误**


# 修复
这个问题的修复很简单，只需要wrap一层`std::pair`即可使其传递`std::pair<std::string,std::string>`。
```
8		contacts.insert(std::make_pair<std::string,std::string>(name,phoneNumber));
```
此外，还可以选择`emplace()`方法，这个方法可以接受一个pair作为参数，而不需要先创建一个pair再传递给insert方法。

```cpp
8		contacts.emplace(name,phoneNumber); 
```


# 为什么报错这么混乱？

不论是`g++`还是报错相对友好的`clang++`,都产生了非常冗长并且混乱的报错。并且`clangd`没有检查出错误。

我们先从相对简单的`clang++`报错进行解析。

## clang++报错

`clang++`的报错通常需要**自底向上**阅读。我们按照这个顺序开始。

```
./blog_code.cc:8:12: note: in instantiation of function template specialization 'std::_Hash<std::_Umap_traits<std::basic_string<char>,
      std::basic_string<char>, std::_Uhash_compare<std::basic_string<char>, std::hash<std::basic_string<char>>, std::equal_to<std::basic_string<char>>>,
      std::allocator<std::pair<const std::basic_string<char>, std::basic_string<char>>>, false>>::insert<std::basic_string<char>>' requested here
   8 |                 contacts.insert(name,phoneNumber);
      |                          ^
1 error generated.
```
这里的错误信息是说在`contacts.insert(name,phoneNumber);`这个语句中，`clang++`在编译时发现`contacts`是一个`std::map`，而`insert`方法期待接收参数`std::pair<std::string,std::string>`或两个迭代器`_Iter _First`,`_Iter _Last`，而实际传递的参数则是`std::string`和`std::string`，所以导致了**类型错误**

随后，这个错误导致了STL一连串的报错：
```
D:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.43.34808/include/xhash:963:9: note: in instantiation of function template
      specialization 'std::_Hash<std::_Umap_traits<std::basic_string<char>, std::basic_string<char>, std::_Uhash_compare<std::basic_string<char>,
      std::hash<std::basic_string<char>>, std::equal_to<std::basic_string<char>>>, std::allocator<std::pair<const std::basic_string<char>,
      std::basic_string<char>>>, false>>::_Insert_range_unchecked<std::basic_string<char>, std::basic_string<char>>' requested here
  963 |         _Insert_range_unchecked(_STD _Get_unwrapped(_First), _STD _Get_unwrapped(_Last));
      |         ^
```
这里的错误信息是说在`_Insert_range_unchecked`这个函数中，`clang++`在编译时发现`_First`是一个`std::string`，而`_Insert_range_unchecked`方法期待接收参数`_Iter _First`,`_Iter _Last`，而实际传递的参数则是`std::string`，所以导致了**类型错误**


```
D:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.43.34808/include/xhash:954:33: error: cannot increment value of type
      'std::basic_string<char>'
  954 |         for (; _First != _Last; ++_First) {
      |                                 ^ ~~~~~~
```

这里的错误信息是说在`for (; _First != _Last; ++_First)`这个循环中，`clang++`在编译时发现`_First`是一个`std::string`，而`_First`期待接收参数`_Iter _First`,`_Iter _Last`，而实际传递的参数则是`std::string`，所以导致了**类型错误**

至此我们已经理清楚了`clang++`的报错内容。接下来看看`g++`的报错


## g++报错

`g++`的报错是从外到内逐层展开的，最外层的错误通常是问题的根源，而内层的错误是编译器在尝试解决问题时遇到的进一步问题。

在这个代码中：

- 最外层是`./blog_code.cc:8:18`。
- 中间层是`stl_map.h`和`stl_tree.h`，涉及STL的实现。
- 最内层是模板推导失败，比如`no type named 'value_type'`。

我们先从最外层开始：
### 外层

```
./blog_code.cc:8:12: note: in instantiation of function template specialization 'std::_Hash<std::_Umap_traits<std::basic_string<char>,
      std::basic_string<char>, std::_Uhash_compare<std::basic_string<char>, std::hash<std::basic_string<char>>, std::equal_to<std::basic_string<char>>>,
      std::allocator<std::pair<const std::basic_string<char>, std::basic_string<char>>>, false>>::insert<std::basic_string<char>>' requested here
   8 |                 contacts.insert(name,phoneNumber);
      |                          ^
```
编译器尝试实例化`std::map`的`insert`方法，但发现参数类型不匹配。

### 中层：`std::map::insert()`的期望参数

`std::map::insert()`有多个重载版本，但主要分为两类：

1. **插入单个键值对**：

   - 接受一个`std::pair<const Key, Value>`对象。

   - 例如：

     ```cpp
     contacts.insert(std::make_pair(name, phoneNumber));
     ```

2. **插入一个范围**：

   - 接受两个迭代器`_Iter _First`和`_Iter _Last`，表示一个范围。

   - 例如：

     ```cpp
     contacts.insert(otherMap.begin(), otherMap.end());
     ```

而在代码中：


```cpp
contacts.insert(name, phoneNumber); // 错误
```

- 这个代码传递了两个`std::string`参数，而`insert`方法没有接受两个独立参数的版本。
- 编译器将`name`和`phoneNumber`解释为迭代器范围，但`std::string`不是迭代器类型，因此导致类型错误。



### 内层：模板实例化失败

```
in instantiation of function template specialization 'std::_Hash<std::_Umap_traits<std::basic_string<char>, ...>>::insert<std::basic_string<char>>' requested here
```

- 编译器尝试实例化`std::map`的`insert`方法模板。但由于参数类型不匹配，模板实例化失败。
- 具体来说，编译器期望`insert`的参数是`std::pair`或迭代器，而实际传递的参数是`std::string`.



# 杂谈
C++的报错真的是史无前例的混乱啊…………


