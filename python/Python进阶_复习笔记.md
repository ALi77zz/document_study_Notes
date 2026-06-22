## 面向对象复习

* 必须掌握的内容

  1. 面向过程和面向对象的区别

     > 面向过程 = 自己写代码完成各种事儿,  例如: 用冒泡, 选择, 插入等排序算法对 列表元素排序. 
     >
     > 面向对象 = 找人(对象)帮我们做事儿,  例如:  Python内置的sort()函数就可以对列表元素排序.

  2. 如何定义类以及使用类中的内容

     ![1742542965063](assets/1742542965063.png)

     ```python
     """
     定义类的格式:
         class 类名(父类名):
             # 属性, 名词
             # 行为, 动词
     
     如何使用类中的成员:
         step1: 创建该类的对象
             对象名 = 类名(实参)
         step2: 通过 对象名. 的方式调用
             对象名.属性
             对象名.行为
     """
     
     # 需求: 定义学生类, 属性: 姓名, 年龄   行为: 学习, 吃饭
     # 1. 定义学生类
     class Student:
         # 属性, 名词    init是魔法方法, 当创建该类对象时, 会被自动调用.
         def __init__(self, name, age):     # 不要把 init(初始化) 写成 int(整型)
             # self.name   对象的属性, 即: 每个学生的 姓名.
             # name        就是传过来的值.
             self.name = name
             self.age = age
     
         # 行为, 动词
         def study(self):
             print(f'{self.name} 正在学习...')
     
         def eat(self):
             print(f'{self.name} 正在吃饭...')
     
     
     # 2. 测试
     if __name__ == '__main__':
         # 2.1 创建学生对象
         s1 = Student('乔峰', 38)
         # 2.2 打印属性值
         print(s1.name, s1.age)
         # 2.3 调用函数
         s1.study()
         s1.eat()
     ```

  3. 继承: 子类如何继承父类, 如何使用父类的成员

     ![1742543766695](assets/1742543766695.png)

     ```python
     """
     子类继承父类的格式:
         class 子类名(父类名):
             pass
     
     好处:
         子承父业, 父类中写一次, 子类中不需要写了, 就可以直接访问, 提高代码的 复用性.
     """
     
     # 需求: 定义父类(Person), 定义属性 和 行为.   定义子类(Student), 子类中继承父类的属性 和 行为.
     # 1. 定义父类
     class Person:
         # 父类的属性
         def __init__(self):
             self.class_name = 'AI23期'
     
         # 父类的行为
         def eat(self):
             print('人要吃饭')
     
     
     # 2. 定义子类
     class Student(Person):
         pass
     
     
     # 3.测试
     if __name__ == '__main__':
         # 3.1 创建子类对象.
         s1 = Student()
         # 3.2 打印该学生的属性 和 行为.
         print(s1.class_name)        # 从父类继承来的属性
         s1.eat()                    # 从父类继承来的行为
     ```

  4. 私有化

     ```python
     """
     私有化目的:
         提高代码的安全性.  因为私有成员, 外界无法直接访问.
     
     如何实现私有化:
         __属性名       一般用这个.
         __函数名
     
     如何访问私有内容:
         通过 类中提供的 公共的访问方式.
     """
     
     # 需求: 定义ATM机类, 私有化属性money, 外界尝试访问和修改.
     # 1. 定义ATM机类.
     class ATM:
         def __init__(self):
             # 2. 私有化属性money.
             self.__money = 10000
     
         # 3. 定义公共的访问方式.
         def get_money(self):        # 插卡, 取钱
             return self.__money
     
         def set_money(self, money):     # 插卡, 存钱
             self.__money = money
     
     
     # 4. 测试
     if __name__ == '__main__':
         # 4.1 创建ATM机对象.
         xm = ATM()
     
         # 4.2 访问私有属性money.
         # print(xm.__money)       # 报错.
     
         # 4.3 通过公共的访问方式, 访问私有属性money.
         xm.set_money(100)
         print(xm.get_money())
     ```

* 重难点

  1. 子类和父类成员重名了, 如何使用父类的成员

     ```python
     """
     子类继承父类的格式:
         class 子类名(父类名):
             pass
     
     好处:
         子承父业, 父类中写一次, 子类中不需要写了, 就可以直接访问, 提高代码的 复用性.
     
     进阶: 子类访问父类重名成员.
         方式1: 父类名.父类成员名(self)      # 适合于 多继承
         方式2: super().父类成员名()        # 适合于 单继承
     """
     
     # 需求: 定义父类(Person), 定义属性 和 行为.   定义子类(Student), 子类中继承父类的属性 和 行为.
     # 1. 定义父类
     class Person:
         # 父类的属性
         def __init__(self):
             self.class_name = 'AI23期'
     
         # 父类的行为
         def eat(self):
             print('人要吃饭')
     
     # 3. 定义学校类, 充当父类.
     class School:
         def __init__(self):
             self.class_name = 'AI学校'
     
         def study(self):
             print('学习')
     
         def eat(self):
             print('学生为了好好学习, 不吃饭!')
     
     # 2. 定义子类
     class Student(School, Person):      # 原则, 就近原则.
     
     
         # 实现, 访问父类的重名成员.  例如: Person#eat(), School#eat()
         def show(self):
             # super().eat()           # 最近的那个父类.
     
             # Person.eat(self)          # 精准访问
             School.eat(self)          # 精准访问
     
     # 3.测试
     if __name__ == '__main__':
         # 3.1 创建子类对象.
         s1 = Student()
         # 3.2 打印该学生的属性 和 行为.
         print(s1.class_name)        # 从父类继承来的属性
         s1.eat()                    # 从父类继承来的行为, 从Person类继承.
     
         # 3.3 打印从School类继承的方法.
         s1.study()
         print('-' * 23)
     
         # 3.4 访问父类的重名函数.
         s1.show()
     ```

* 案例

  1. 定义学生类, 属性: 姓名, 年龄, 行为: 吃饭, 学习, 创建对象, 并调用类中成员.
  2. 减肥案例
  3. 继承案例: 子类继承父类, 且子类可以访问父类的成员.
  4. 私有化案例, 如何访问类中私有的 money属性.



## 闭包和装饰器复习

* 必须掌握的内容

  1. 闭包的入门案例, 即: 你要会闭包的格式.

     ```python
     """
     闭包:
         作用:
             延长外部函数的 局部变量的生命周期.
         格式:
             def 外部函数名():
                 # 外部函数的 局部变量
     
                 def 内部函数名():                # 有嵌套
                     # 使用外部函数的 局部变量      # 有引用
     
                 return 内部函数名                # 有返回, 把内部函数对象 当做外部函数的 返回值 进行返回.
     """
     
     # 需求: 定义闭包入门案例.
     def fn_outer():     # 外部函数
         a = 100         # 外部函数的 局部变量
     
         def fn_inner():     # 内部函数
             print(a)        # 使用外部函数的 局部变量
     
     
         return fn_inner     # 有返回, 把内部函数对象 当做外部函数的 返回值 进行返回.
     
     
     
     # 测试:
     if __name__ == '__main__':
         my_fn = fn_outer()      # 等价于 def my_fn(): print(a)
     
         my_fn()                 # 100, 闭包(有嵌套, 有引用, 有返回)
     ```

  2. 装饰器的入门案例, 即: 你要会装饰器的格式.

     ```python
     """
     装饰器介绍:
         概述:
             闭包的一种特殊写法, 用于实现 在不改变目标函数的基础上, 对功能做增强.
         大白话:
             装饰器 = 装修队
             目标函数 = 你买的 毛坯房
         写法:
             传统方式:
                 装饰后的函数名 = 装饰器名(目标函数名)
                 装饰后的函数名()
     
             语法糖:
                 在目标函数上直接写 @装饰器名,  之后正常调用目标函数即可.
     
         前提条件:
             1. 有嵌套.
             2. 有引用.
             3. 有返回.
             4. 有额外功能.
     """
     
     # 需求: 定义目标函数, 表示: 发表评论.   在发表评论前, 需要先校验登陆.
     
     # 1. 定义装饰器.
     # def 装修队(房间号):
     #     def 装修后的内容():
     #         print('具体的装修动作')
     #         房间号()
     #
     #     return 装修后的内容
     
     # 装饰器
     def check_login(fn_name):
         def fn_inner():         # 有嵌套
             print('校验登陆')    # 有额外功能
             fn_name()          # 有引用
     
         return fn_inner         # 有返回
     
     # 2. 定义目标函数.
     @check_login
     def comment():
         print('发表评论')
     
     # 3. 测试
     if __name__ == '__main__':
         # 3.1 传统写法
         # comment = check_login(comment)
         # comment()
     
         # 3.2 装饰器写法.
         comment()
     ```

* 重难点

  1. 多个装饰器的装饰顺序

     ```python
     """
     装饰器介绍:
         概述:
             闭包的一种特殊写法, 用于实现 在不改变目标函数的基础上, 对功能做增强.
         大白话:
             装饰器 = 装修队
             目标函数 = 你买的 毛坯房
         写法:
             传统方式:
                 装饰后的函数名 = 装饰器名(目标函数名)
                 装饰后的函数名()
     
             语法糖:
                 在目标函数上直接写 @装饰器名,  之后正常调用目标函数即可.
     
         前提条件:
             1. 有嵌套.
             2. 有引用.
             3. 有返回.
             4. 有额外功能.
     
     多个装饰器装饰顺序解释:
         传统写法 = 由内向外装饰
         语法糖写法 = 从上往下执行.
     """
     
     # 需求: 定义目标函数, 表示: 发表评论.   在发表评论前, 需要先校验登陆, 后校验验证码.
     
     # 1. 定义装饰器.
     # def 装修队(房间号):
     #     def 装修后的内容():
     #         print('具体的装修动作')
     #         房间号()
     #
     #     return 装修后的内容
     
     # 装饰器, 校验登陆
     def check_login(fn_name):
         def fn_inner():         # 有嵌套
             print('校验登陆')    # 有额外功能
             fn_name()          # 有引用
     
         return fn_inner         # 有返回
     
     
     # 装饰器, 校验验证码
     def check_code(fn_name):
         def fn_inner():         # 有嵌套
             print('校验验证码')   # 有额外功能
             fn_name()          # 有引用
         return fn_inner         # 有返回
     
     
     
     # 2. 定义目标函数.
     @check_login
     @check_code
     def comment():
         print('发表评论')
     
     # 3. 测试
     if __name__ == '__main__':
         # 3.1 传统写法
         # comment = check_login(comment)
         # comment()
     
         # 3.2 装饰器写法.
         comment()
     ```

## 网络编程

* 你要掌握的内容

  ![1742548401491](assets/1742548401491.png)

  * 客户端代码

    ```python
    """
    多线程案例, 一句话交情.
    
    
    客户端思路:
        1. 创建客户端Socket对象, 指定: ipv4, tcp协议
        2. 指定客户端 连接服务器端的 ip, 端口号
        3. 给服务器端发送消息.
        4. 接受服务器端的回执信息.
        5. 释放资源.
    """
    # 导包
    import socket
    
    # 1. 创建客户端Socket对象, 指定: ipv4, tcp协议
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # 2. 指定客户端 连接服务器端的 ip, 端口号
    client_socket.connect(("127.0.0.1", 12345))
    # 3.给服务器端发送消息
    client_socket.send('你好服务器端, 我是客户端!'.encode('utf-8'))
    # 4. 接受服务器端的回执信息.
    #                 1次接收1024个字节     解码
    data = client_socket.recv(1024).decode('utf-8')
    print(f"客户端收到: {data}")
    
    # 5. 释放资源.
    client_socket.close()
    ```

  * 服务器端代码

    ```python
    """
    多线程案例, 一句话交情.
    
    
    服务器端思路:
        1. 创建服务器端Socket对象, 指定: ipv4, tcp协议
        2. 绑定服务器端ip, 端口号
        3. 设置最大监听数量.
        4. 开启监听, 等待客户端申请建立连接.
        5. 接收客户端传输的消息.
        6. 给客户端回执信息.
        7. 释放资源.
    """
    # 导包
    import socket
    
    # 1. 创建服务器端Socket对象, 指定: ipv4, tcp协议
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # 2. 绑定服务器端ip, 端口号
    server_socket.bind(("127.0.0.1", 12345))
    # 3. 设置最大监听数量.
    server_socket.listen(5)
    # 4. 开启监听, 等待客户端申请建立连接.
    # 参1: 负责和客户端交互的socket对象.
    # 参2: 客户端信息.
    accept_socket, client_info = server_socket.accept()
    # 5. 接收客户端传输的消息.
    #                 1次接收1024个字节     解码
    data = accept_socket.recv(1024).decode('utf-8')
    print(f"服务器端收到: {data}")
    
    # 6. 给客户端回执信息.
    accept_socket.send('欢迎来到Scoket的世界'.encode('utf-8'))
    
    # 7. 释放资源.
    accept_socket.close()
    # server_socket.close()
    ```



## 进程和线程

* 你必须掌握的知识点

  1. 带参数的多进程

     ```python
     """
     进程解释:
         概述:
             无论是多进程, 还是多线程, 都是实现多任务的一种手段.
         目的:
             充分利用CPU资源, 提高开发效率.
         方式:
             并行: 多个任务同时执行.           前提: 需要多核CPU
                 大白话: 双车道, 四车道
             并发: 多个任务同时请求执行, 同一瞬间CPU只能执行1个任务, 于是安排它们交替执行.
                 大白话: 单车道              针对于: 单核CPU来讲的
     
         进程和线程的区别:
             1. 进程是CPU分配资源的基本单位, 线程是CPU调度资源的基本单位.
                 大白话:
                     CPU是以进程为单位分配资源的, 例如: 给QQ 2核3G内存,  给微信 3核5G内存...
                     QQ进程内部可以有很多线程(跟张三聊天, 看空间, 群聊, 偷菜, 抢车位...), 由CPU给这些线程分配资源.
             2. 进程之间数据是相互隔离的, (同一个进程)的多个线程间数据共享.
             3. 多进程相对更消耗资源, 相对更稳定.  例如: 10个班, 每个班5个人.
             4. 多线性相对更节省资源, 稳定性相对较弱.  例如: 1个班, 50个人.
     实现步骤:
         1. 导包
         2. 创建进程对象.
         3. 启动进程.
     """
     
     # 导包
     import multiprocessing
     import time
     
     
     # 1. 定义目标函数, 敲代码
     def code(name, num):
         for i in range(num):
             time.sleep(0.1)
             print(f'{name} 正在敲第{i}行代码...')
     
     
     # 2.定义目标函数, 听音乐
     def music(name, count):
         for i in range(count):
             time.sleep(0.1)
             print(f'{name} 正在听第{i}首歌**********')
     
     
     # 3. 测试
     if __name__ == '__main__':
         # 3.1 创建进程对象
         # 参1: 目标函数
         # args: 以元组的形式, 给目标函数传参.
         # kwargs: 以字典的形式, 给目标函数传参.
         p1 = multiprocessing.Process(target=code, args=('乔峰', 10))
         p2 = multiprocessing.Process(target=music, kwargs={'count': 10, 'name': '虚竹'})
     
         # 3.2 启动进程
         p1.start()
         p2.start()
     
     ```

  2. 带参数的多线程

     ```python
     """
     进程解释:
         概述:
             无论是多进程, 还是多线程, 都是实现多任务的一种手段.
         目的:
             充分利用CPU资源, 提高开发效率.
         方式:
             并行: 多个任务同时执行.           前提: 需要多核CPU
                 大白话: 双车道, 四车道
             并发: 多个任务同时请求执行, 同一瞬间CPU只能执行1个任务, 于是安排它们交替执行.
                 大白话: 单车道              针对于: 单核CPU来讲的
     
         进程和线程的区别:
             1. 进程是CPU分配资源的基本单位, 线程是CPU调度资源的基本单位.
                 大白话:
                     CPU是以进程为单位分配资源的, 例如: 给QQ 2核3G内存,  给微信 3核5G内存...
                     QQ进程内部可以有很多线程(跟张三聊天, 看空间, 群聊, 偷菜, 抢车位...), 由CPU给这些线程分配资源.
             2. 进程之间数据是相互隔离的, (同一个进程)的多个线程间数据共享.
             3. 多进程相对更消耗资源, 相对更稳定.  例如: 10个班, 每个班5个人.
             4. 多线性相对更节省资源, 稳定性相对较弱.  例如: 1个班, 50个人.
     实现步骤:
         1. 导包
         2. 创建线程对象.
         3. 启动线程.
     """
     
     # 导包
     import threading
     import time
     
     
     # 1. 定义目标函数, 敲代码
     def code(name, num):
         for i in range(num):
             time.sleep(0.1)
             print(f'{name} 正在敲第{i}行代码...')
     
     
     # 2.定义目标函数, 听音乐
     def music(name, count):
         for i in range(count):
             time.sleep(0.1)
             print(f'{name} 正在听第{i}首歌**********')
     
     
     # 3. 测试
     if __name__ == '__main__':
         # 3.1 创建进程对象
         # 参1: 目标函数
         # args: 以元组的形式, 给目标函数传参.
         # kwargs: 以字典的形式, 给目标函数传参.
         t1 = threading.Thread(target=code, args=('乔峰', 10))
         t2 = threading.Thread(target=music, kwargs={'count': 10, 'name': '虚竹'})
     
         # 3.2 启动进程
         t1.start()
         t2.start()
     
     ```

* 重难点

  > **进程和线程的区别是什么?**
  >
  > ```
  > 1. 进程是CPU分配资源的基本单位, 线程是CPU调度资源的基本单位.
  >     大白话:
  >         CPU是以进程为单位分配资源的, 例如: 给QQ 2核3G内存,  给微信 3核5G内存...
  >         QQ进程内部可以有很多线程(跟张三聊天, 看空间, 群聊, 偷菜, 抢车位...), 由CPU给这些线程分配资源.
  > 2. 进程之间数据是相互隔离的, (同一个进程)的多个线程间数据共享.
  > 3. 多进程相对更消耗资源, 相对更稳定.  例如: 10个班, 每个班5个人.
  > 4. 多线性相对更节省资源, 稳定性相对较弱.  例如: 1个班, 50个人. 
  > ```

## 生成器和正则

* 你要掌握的内容

  1. 生成器的两种写法

     ```python
     """
     生成器介绍:
         概述:
             它是基于规则来生成数据, 并不是一下次生成所有的数据, 而是用一批生成一批.
         目的:
             节约内存(空间)
         大白话:
             家具城生产家具, 只有少量的样本, 当用户下单时才会现做, 发货...
         格式:
             1. 生成器对象 = (生成数据的规则)       类似于: 列表推导式
             2. yield关键字, 它有三重作用: 创建, 添加, 返回
     """
     # 导包
     import sys
     
     # 1. 生成 1 ~ 100000 之间的偶数列表.
     # 思路1: 回顾 列表推导式.
     my_list = [i for i in range(0, 100000, 2)]      # 一口气生成所有的数据.
     print(my_list)
     # 查看内存占用.
     print(sys.getsizeof(my_list))       # 444376字节
     print('-' * 23)
     
     
     # 思路2: "元组"推导式, 即: 生成器.
     my_generator = (i for i in range(0, 100000, 2))
     print(my_generator)     # 生成器对象.
     # 从生成器中获取数据.
     for i in my_generator:
         print(i)
     # 查看内存占用.
     print(sys.getsizeof(my_generator))       # 192字节
     print('*' * 23)
     
     
     # 需求2: yield关键字实现,生成 1 ~ 100000 之间的偶数列表.
     # 1. 定义函数, 获取生成器对象.
     def get_generator():
         for i in range(0, 100000, 2):
             yield i     # yield三件事: 创建(生成器对象), 添加数据到生成器, 返回生成器对象.
     
     my_generator = get_generator()
     ```

  2. 正则校验手机号

     ```python
     """
     正则表达式介绍:
         概述:
             正确的, 符合特定规则的字符串, 就是用来 校验, 查找, 匹配, 过滤, 替换数据的.
             全称Regular Expression, 简称: re
         用法:
             1. 导包
                 import re
             2. 正则校验.
                 result = re.match('正则表达式', 要被校验的字符串)
             3. 获取校验结果.
                 res = result.group()
     """
     # 导包
     import re
     
     # 需求1: 校验手机号.
     # 1. 定义手机号.
     phone = '13812345678'
     # 2. 校验手机号.
     # 正则规则: ^ 表示开头, $ 表示结尾.  1表示就是数字1,  [3-9] 表示3到9的任意1个数字, \d 表示任意1个数字, {9} 表示: 前边内容恰好出现9次.
     result = re.match(r'^1[3-9]\d{9}$', phone)
     # 3. 获取校验结果.
     if result:
         print(f'手机号正确, 匹配到: {result.group()}')
     else:
         print('手机号错误')
     print('-' * 23)
     ```

  3. 正则提取分组的信息

     ```python
     # 需求2: 提取分组信息.
     # 1. 定义字符串.
     s1 = 'qq:12345678'
     # 2. 校验字符串.
     # 正则规则: \d 表示任意1个数字, {6,11} 表示: 前边内容至少出现6次, 至少出现11次.
     #                          第1组 第2组
     result = re.match(r'(qq):(\d{6,11})', s1)
     # 3. 获取校验结果.
     if result:
         print(f'匹配成功, 匹配到: {result.group()}')
         print(f'匹配成功, 匹配到: {result.group(0)}')  # 效果同上
         print(f'匹配成功, 匹配到: {result.group(1)}')  # qq, 第1组
         print(f'匹配成功, 匹配到: {result.group(2)}')  # 12345678, 第2组
     else:
         print('匹配失败')
     
     ```

* 重难点

  1. 批量生成歌词数据. 

## 数据结构与算法

* 你必须掌握的

  1. 数据结构解释

     > 存储 和 组织数据的方式,  是算法解决实际业务问题时的 "数据载体"

  2. 算法解释

     > 就是解决实际业务问题的思路, 方式.

  3. 算法的衡量标准-> 大O标记法

     > **大O标记法**: 只考虑**主要条件(随着问题规模改变而改变的条件)**, 而忽略常数项, 次要条件等.
     >
     > ==常见的时间复杂度, 从优到劣分别是==
     >
     > O(1) -> O(logn) -> O(n) -> O(n logn) -> O(n²) -> O(n³)
     >
     > **如非必要, 我们一般只考虑: 最坏时间复杂度.**

  4. 数据结构的分类

     > **线性结构:**每个节点都只能有1个前驱, 1个后继节点.
     >
     > ​	**顺序表: 存储空间是连续的.**
     >
     > ​		例如:  栈, 队列
     >
     > ​		一体式存储: 信息区和数据区在一起.			my_list = [10, 20, 30]
     >
     > ​		分离式存储: 信息区和数据区分开存储.		my_list = ['a', 'abcdef', 10, False]
     >
     > ​	**链表:  存储空间是非连续的, 有地儿就行.**
     >
     > **非线性结构:**  每个节点可以有N个前驱, N个后继节点.
     >
     > ​	例如: 树, 图

  5. 自定义代码, 模拟链表

     ![1742553847583](assets/1742553847583.png)

     ![1742553854902](assets/1742553854902.png)

     ```python
     """
     案例: 模拟的是 单向链表.
     
     回顾:
         链表 是由 节点(数值域, 地址域) 组成的一条链子.
     
     分析:
         1. 定义节点类, 属性: 数值域, 地址域
     
         2. 定义链表类, 存储多个节点对象, 形成一条链子.
             属性:
                 head    指向链表的第1个节点, 也叫: 头结点
             行为:
                 is_empty()
                 length()
                 travel()
                 append()
     """
     # 1. 定义节点类.
     class SingleNode:
         # 初始化属性: 数值域, 地址域.
         def __init__(self, item):
             self.item = item    # 数值域.
             self.next = None    # 地址域.
     
     
     
     # 2. 定义链表类.
     class SingleLinkedList:
         # 2.1 初始化属性, 指向 链表的第1个节点(头结点)
         def __init__(self, node=None):
             self.head = node        # 头结点.
     
         # 2.2 判断链表是否为空
         def is_empty(self):
             return self.head == None        # 头结点为None, 链表为空.
     
         # 2.3 length()
         def length(self):
             # 1.定义计数器
             count = 0
             # 2. 定义变量cur记录当前节点.
             cur = self.head
             # 3. 判断当前节点不为空, 就一直遍历
             while cur is not None:
                 # 3.1 计数器 + 1
                 count += 1
                 # 3.2 cur后移.
                 cur = cur.next
             # 4.返回计数结果.
             return count
     
     # 3.测试
     if __name__ == '__main__':
         # 3.1 测试节点类.
         node1 = SingleNode('乔峰')
         # 3.2 打印节点类的数值域 和 地址域
         print(f'数值域: {node1.item}')
         print(f'地址域: {node1.next}')
     
         # 3.3 再次测试节点类.
         node2 = SingleNode('虚竹')
         print(f'数值域: {node2.item}')
         print(f'地址域: {node2.next}')
         print('-' * 23)
     
         # 3.4 测试链表.
         # my_linkedlist = SingleLinkedList()  # 空链表
         my_linkedlist = SingleLinkedList(node1)  # 乔峰作为头结点
         print(f'my_linkedlist: {my_linkedlist}')
         # print(f'头结点的数值域: {my_linkedlist.head.item}')    # 乔峰
         print('-' * 23)
     
         # 3.4 测试链表是否为空.
         print(my_linkedlist.is_empty())
         print('-' * 23)
     
         # 3.5 测试链表长度.
         print(my_linkedlist.length())
     ```
