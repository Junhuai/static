# Mockito教程

## 第一章 快速入门

### 1.引入jar包

![image-20230513195108716](images/image-20230513195108716.png)

### 2.入门实例代码

![image-20230513195005340](images/image-20230513195005340.png)

## 第二章 Mock

![img](images/91431c4745d06991d7cf692b7def4add0e46bf2b.jpg@1152w_!web-note-16839771476031.webp)



### 1.Use runner

@RunWith(MockitoJUnitRunnber.class)



![img](images/b7ab26b0b6512fa8cbae0d0b8404cab0daf1bf7d.jpg@1152w_!web-note-16839771476033.webp)

mock方法的第二个参数决定mock对象返回什么，默认使用defaultAnswer，某些类可以返回一个对象，其他返回null

Mockito.RETURN_SMART_NULLS会返回一个字符串

![img](images/f87a628ddf025a635fd00c7fc743777e5500641f.jpg@1152w_!web-note-16839771476045.webp)



### 2.Mock by Annotation

![img](images/a1e39b7ee88e1305f7b59e9f7dddf8614def9f0c.jpg@1152w_!web-note-16839771476047.webp)



### 3.Mock by rule

![img](images/a1b2a628f1f2ef88b5e32a28981951191489cb71.jpg@1152w_!web-note-16839771476049.webp)



### 4.Deep mock

针对链式编程，即连续点的情况

#### 4.1 基本方法

![img](images/59920eae6e33ac1d5e04b5e2cb3facc323802530.jpg@1152w_!web-note-168397714760411.webp)

#### 4.2 deep方法

![img](images/c60eac34d8d279a5d7775403701f6082bea930fa.jpg@1152w_!web-note-168397714760413.webp)

## 第三章 Stubbing

### 1. how to stubbing

例子：

![image-20230514113556296](images/image-20230514113556296.png)

![image-20230514113919450](images/image-20230514113919450.png)

### 2. stubbing无返回值的方法

![image-20230514114522683](images/image-20230514114522683.png)

### 3. doReturn方法做stubbing

等价于1小节中的写法

![image-20230514114851229](images/image-20230514114851229.png)

### 4. 一次stubbing返回多个值

![image-20230514115241193](images/image-20230514115241193.png)

等价于多次调用thenReturn（链式调用法）

### 5.  stubbing answer

自己写逻辑做返回值，可以对不同的入参返回不同的值

![image-20230514115804610](images/image-20230514115804610.png)

### 6. 调用真正的方法

mock返回的对象是cglib代理类，不会调用真正的方法,使用thenCallRealMethod调用自身method

![image-20230514122948624](images/image-20230514122948624.png)

## 第四章 Spying

属于部分mock，spy返回的对象上调用未stubing方法将调用真正的方法，和mock刚好相反

![image-20230514124519830](images/image-20230514124519830.png)

上面没有stubbing，只有spy，调用的是真正的方法

但是如果有stubbing,那么相应的方法会有mock行为，如下红框

![image-20230514124735615](images/image-20230514124735615.png)

spy对象可以使用annotation方式产生

![image-20230514125116542](images/image-20230514125116542.png)

## 第五章 Argument Matchers

### 1. 直接匹配

能匹配参数的stubbing返回相应的值，不能匹配则只能返回一些默认值。判断参数是不是匹配使用equals方法比较。

![image-20230514130617479](images/image-20230514130617479.png)



### 2. isA()

isA判断传入的参数是否某个类(及其子类)的实例(使用instanceof判断)，如下，Child1, Child2是Parent的子类，可以用isA匹配



![image-20230514131248319](images/image-20230514131248319.png)

![image-20230514131647996](images/image-20230514131647996.png)

或者类本身也匹配，匹配不上只能返回默认值。

![image-20230514132204499](images/image-20230514132204499.png)

### 3. any() 匹配

永远匹配成功，所以不论给的什么类型都认为匹配

![image-20230514132945211](images/image-20230514132945211.png)

### 4. any...()

anyInt,  anyString, anyCollection, anyObject等等

配测试类：

![image-20230514133420923](images/image-20230514133420923.png)

测试类：

![image-20230514134210159](images/image-20230514134210159.png)

>一旦使用了匹配函数，则不允许再使用直接匹配，这个时候可以使用eq方法达到相同的目的
>
>例如：
>
>![image-20230514134909824](images/image-20230514134909824.png)
>
>如果一个调用能匹配到多个stubbing,则最后一个将生效

### 5. doNothing()

不产生返回值,针对返回值为void的被测试方法

![image-20230514135411604](images/image-20230514135411604.png)

## 第六章 Hamcrest matcher

### 1.内置matcher做断言

![image-20230514155041725](images/image-20230514155041725.png)

可以使用either/both/anyOf/allOf将多个结果连起来

![image-20230514155721219](images/image-20230514155721219.png)



### 2.自定义matcher做断言

> 继承自BaseMatcher

实现：

![image-20230514161249163](images/image-20230514161249163.png)

![image-20230514161304982](images/image-20230514161304982.png)



使用：

![image-20230514161434219](images/image-20230514161434219.png)