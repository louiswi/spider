#Built-in Functions

####_hasattr(object, name)_  
The arguments are an object and a string. The result is True if the string is the name of one of the object’s attributes, False if not. (This is implemented by calling getattr(object, name) and seeing whether it raises an AttributeError or not.)  
参数是一个对象与一个字符串. 如果字符串是对象属性的名字, 则返回值为真, 否则为假.(它通过执行`getattr(object, name)`来查看是否引发一个_AttributeError_, 据此完成该函数的功能)  

====
```
2015 11 2 晚
```
