方法(Methods)
===============

>> Methods are functions that are associated with a particular type. Classes, structures, and enumerations can all define instance methods, which encapsulate specific tasks and functionality for working with an instance of a given type. Classes, structures, and enumerations can also define type methods, which are associated with the type itself. Type methods are similar to class methods in Objective-C.

方法是与某些特定类型相关联的功能/函数。类、结构体、枚举都可以定义实例方法；实例方法为指定类型的实例封装了特定的任务与功能。类、结构体、枚举也可以定义类(型)方法(type itself)；类型方法与类型自身相关联。类型方法与Objective-C中的类方法(class methods)相似。

>> The fact that structures and enumerations can define methods in Swift is a major difference from C and Objective-C. In Objective-C, classes are the only types that can define methods. In Swift, you can choose whether to define a class, structure, or enumeration, and still have the flexibility to define methods on the type you create.

在Swift中,结构体和枚举能够定义方法；事实上这是Swift与C/Objective-C的主要区别之一。在Objective-C中,类是唯一能定义方法的类型。在Swift中，你能够选择是否定义一个类/结构体/枚举，并且你仍然享有在你创建的类型(类/结构体/枚举)上定义方法的灵活性。

### 实例方法(Instance Methods) ###
>> Instance methods are functions that belong to instances of a particular class, structure, or enumeration. They support the functionality of those instances, either by providing ways to access and modify instance properties, or by providing functionality related to the instance’s purpose. Instance methods have exactly the same syntax as functions, as described in Functions.

实例方法是某个特定类、结构体或者枚举类型的实例的方法。实例方法支撑实例的功能: 或者提供方法,以访问和修改实例属性;或者提供与实例的目的相关的功能。实例方法的语法与函数完全一致，参考函数说明(a link should be here)。

>> You write an instance method within the opening and closing braces of the type it belongs to. An instance method has implicit access to all other instance methods and properties of that type. An instance method can be called only on a specific instance of the type it belongs to. It cannot be called in isolation without an existing instance.

实例方法要写在它所属的类型的前后括号之间。实例方法能够访问他所属类型的所有的其他实例方法和属性。实例方法只能被它所属的类的特定实例调用。实例方法不能被孤立于现存的实例而被调用。

>> Here’s an example that defines a simple Counter class, which can be used to count the number of times an action occurs:

下面是定义一个很简单的类Counter的例子(Counter能被用来对一个动作发生的次数进行计数):

```
1|  class Counter {
2|   var count = 0
3|   func increment() {
4|     count++
5|   }
6|   func incrementBy(amount: Int) {
7|     count += amount
8|   }
9|   func reset() {
10|    count = 0
11|  }
12|}
```

>> The Counter class defines three instance methods:
>> • increment increments the counter by 1.
>> • incrementBy(amount: Int) increments the counter by an specified integer amount.
>> • reset resets the counter to zero.

Counter类定理了三个实例方法：
- increment让计数器按一递增；
- incrementBy(amount: Int)让计数器按一个指定的整数值递增；
- reset将计数器重置为0。

>> The Counter class also declares a variable property, count, to keep track of the current counter value.

Counter这个类还声明了一个可变属性count，用它来保持对当前计数器值的追踪。

>> You call instance methods with the same dot syntax as properties:

和调用属性一样，用点语法(dot syntax)调用实例方法:

```
1| let counter = Counter()
2| // the initial counter value is 0
3| counter.increment()
4| // the counter's value is now 1
5| counter.incrementBy(5)
6| // the counter's value is now 6
7| counter.reset()
8| // the counter's value is now 0
```

### 方法的局部和外部参数名称(Local and External Parameter Names for Methods) ###

>> Function parameters can have both a local name (for use within the function’s body) and an external name (for use when calling the function), as described in External Parameter Names. The same is true for method parameters, because methods are just functions that are associated with a type. However, the default behavior of local names and external names is different for functions and methods.

函数参数有一个局部名称(在函数体内部使用)和一个外部名称(在调用函数时使用),参考External Parameter Names一节。对于方法参数也是这样，因为方法就是函数(只是这个函数与某个类型相关联了)。但是，方法和函数的局部名称和外部名称的默认行为是不一样的。

>> Methods in Swift are very similar to their counterparts in Objective-C. As in Objective-C, the name of a method in Swift typically refers to the method’s first parameter using a preposition such as with , for , or by , as seen in the incrementBy method from the preceding Counter class example. The use of a preposition enables the method to be read as a sentence when it is called. Swift makes this established method naming convention easy to write by using a different default approach for method parameters than it uses for function parameters.

Swift中的方法和Objective-C中的方法极其相似。像在Objective-C中一样，Swift中方法的名称通常用一个介词指向方法的第一个参数，比如：with,for,by等等。前面的Counter类的例子中incrementBy方法就是这样的。介词的使用让方法在被调用时能像一个句子一样被解读。Swift这种方法命名约定很容易落实,因为它是用不同的默认处理方法参数的方式，而不是用函数参数(来实现的)。

>> Specifically, Swift gives the first parameter name in a method a local parameter name by default,
and gives the second and subsequent parameter names both local and external parameter names by default.
This convention matches the typical naming and calling convention you will be familiar with from writing Objective-C methods,
and makes for expressive method calls without the need to qualify your parameter names.

具体来说，Swift默认仅给方法的第一个参数名称一个局部参数名称;但是默认同时给第二个和后续的参数名称局部参数名称和外部参数名称。
这个约定与典型的命名和调用约定相匹配，这与你在写Objective-C的方法时很相似。这个约定还让expressive method调用不需要再检查/限定参数名。

>> Consider this alternative version of the Counter class, which defines a more complex form of the incrementBy method:

看看下面这个Counter的替换版本（它定义了一个更复杂的incrementBy方法）：

```
1| class Counter {
2|   var count: Int = 0
3|   func incrementBy(amount: Int, numberOfTimes: Int) {
4|     count += amount * numberOfTimes
5|   }
6| }
```

>> This incrementBy method has two parameters— amount and numberOfTimes.
By default, Swift treats amount as a local name only, but treats numberOfTimes as both a local and an external name.
You call the method as follows:

这个incrementBy方法有两个参数： amount和numberOfTimes。默认地，Swift只把amount当作一个局部名称，但是把numberOfTimes即看作本地名称又看作外部名称。下面调用这个方法：

```
1| let counter = Counter()
2| counter.incrementBy(5, numberOfTimes: 3)
3| // counter value is now 15
```

>> You don’t need to define an external parameter name for the first argument value, because its purpose is clear from the function name incrementBy. The second argument, however, is qualified by an external parameter name to make its purpose clear when the method is called.

你不必为第一个参数值再定义一个外部变量名：因为从函数名incrementBy已经能很清楚地看出它的目的/作用。但是第二个参数，就要被一个外部参数名称所限定,以便在方法被调用时让他目的/作用明确。

>> This default behavior effectively treats the method as if you had written a hash symbol ( # ) before the numberOfTimes parameter:

这种默认的行为能够有效的检查方法，比如你在参数numberOfTimes前写了个井号( # )时:

```
1| func incrementBy(amount: Int, #numberOfTimes: Int) {
2|  count += amount * numberOfTimes
3| }
```

>> The default behavior described above mean that method definitions in Swift are written with the same grammatical style as Objective-C,
and are called in a natural, expressive way.

这种默认行为使上面代码意味着：在Swift中定义方法使用了与Objective-C同样的语法风格，并且方法将以自然表达式的方式被调用。

