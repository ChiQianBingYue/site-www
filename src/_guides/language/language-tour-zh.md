---
title: Dart语言之旅
description: A tour of all of the major Dart language features.
short-title: Language Tour
---
<?code-excerpt replace="/([A-Z]\w*)\d\b/$1/g"?>

本文将会向您展示如何使用Dart的主要特性，从最简单的变量到如何操作对象与类库。  
我们将假设您已有其他编程语言的基础。
<!-- This page shows you how to use each major Dart feature, from
variables and operators to classes and libraries, with the assumption
that you already know how to program in another language. -->


<div class="alert alert-info" markdown="1">
**Dart 2 提示:**
这段旅程的内容已经为[Dart 2 改变](/dart-2)更新过了，
比如可选的 `new` and `const`。
</div>
<!-- **Dart 2 note:**
This tour is being updated for [Dart 2 changes](/dart-2),
such as optional `new` and `const`. -->


想要学习更多的Dart核心类库，请参考 [Dart类库之旅](/guides/libraries/library-tour)。如果您想了解更多语言特性的细节，请参考[Dart语言细则](/guides/language/spec)。
<!-- To learn more about Dart's core libraries, see
[A Tour of the Dart Libraries](/guides/libraries/library-tour).
Whenever you want more details about a language feature,
consult the [Dart Language Specification](/guides/language/spec). -->

{% comment %}
update-for-dart-2
TODO: Uncomment when DartPad supports Dart 2 semantics.

<div class="alert alert-info" markdown="1">
**Tip:**
You can play with most of Dart's language features using DartPad
([learn more](/tools/dartpad)).

**<a href="{{ site.custom.dartpad.direct-link }}" target="_blank">Open DartPad</a>**
</div>
{% endcomment %}


## 一个基本的Dart程序
<!-- ## A basic Dart program -->

下面的代码使用了很多Dart的最基本特性：
<!-- The following code uses many of Dart’s most basic features: -->

<?code-excerpt "misc/test/language_tour/basic_test.dart"?>
{% prettify dart %}
// 定义一个方法
printInteger(int aNumber) {
  print('The number is $aNumber.'); // 打印到控制台
                                    
}

// 这里是app开始执行的地方
main() {
  var number = 42; // 声明并初始化一个变量
  printInteger(number); // 调用一个方法
}
{% endprettify %}

我们来看看这段程序里的那些可以使用在几乎所有Dart程序中的东西：
<!-- Here’s what this program uses that applies to all (or almost all) Dart apps: -->

<code>// <em>This is a comment.</em> </code>

:   单行注释。Dart同样支持多行和文本注释。更多的细节，请参考[《注释》](#comments)章节.
<!-- :   A single-line comment.Dart also supports multi-line and document comments.For details, see [Comments](#comments). -->

`int`

:   一种类型。其他的[内置类型](#built-in-types)有String, List,和 bool。
<!-- :   A type. Some of the other [built-in types](#built-in-types)
    are `String`, `List`, and `bool`. -->

`42`

:   一个数字字面量。数字字面量是一种编译时常量。
<!-- :   A number literal. Number literals are a kind of compile-time constant. -->

`print()`

:   一个方便的打印输出的办法。
<!-- :   A handy way to display output. -->

`'...'` (or `"..."`)

:   一个字符串字面量。
<!-- :   A string literal. -->

<code>$<em>variableName</em></code> (或者 <code>${<em>expression</em>}</code>)

:   解析型字符串：用来在字符串字面量中加入一个变量或者可转化为字符串的表达式。更多的内容，请参考[Strings](#strings)。
<!-- :   String interpolation: including a variable or expression’s string
    equivalent inside of a string literal. For more information, see
    [Strings](#strings). -->

`main()`

:   一个特别的、*必须的*、顶层的用来启动app的方法。更多的信息，请参考[The main() function](#the-main-function)章节。
<!-- :   The special, *required*, top-level function where app execution
    starts. For more information, see
    [The main() function](#the-main-function).-->

`var`

:   一个用来在不声明类型的情况下声明变量的办法。
<!-- :   A way to declare a variable without specifying its type. -->

<div class="alert alert-info" markdown="1">
**注意:**
本网站的代码内容遵循了[Dart style guide](/guides/language/effective-dart/style)中的格式规范.
<!-- **Note:**
This site's code follows the conventions in the
[Dart style guide](/guides/language/effective-dart/style). -->
</div>


## 重要的概念

在您学习Dart语言的过程中，请记住下列的事实和概念:
<!-- As you learn about the Dart language, keep these facts and concepts in
mind: -->
-   所有你能放置在变量「*variable*」中的都是一个对象「*object*」，
    而且每一个对象都是一个类「*class*」的实例。不论是数字「*numbers*」，
    方法「*functions*」，还是`null`，都是对象。所有的对象都继承了[*Object*](https://api.dartlang.org/dev/dart-core/Object-class.html) 类。
<!-- -   Everything you can place in a variable is an *object*, and every
    object is an instance of a *class*. Even numbers, functions, and
    `null` are objects. All objects inherit from the [Object][] class. -->

-   尽管Dart是强类型，但是在代码中并不一定要声明类型。换句话说，
    Dart的类型是可选的「*optional*」。因为Dart可以推断类型。在
    上面的代码中，`number`会被推断为`int`类型。如果您确定不需
    要类型，可以使用[特殊类型`dynamic`](https://www.dartlang.org/guides/language/effective-dart/design#do-annotate-with-object-instead-of-dynamic-to-indicate-any-object-is-allowed)。
<!-- -   Although Dart is strongly typed, type annotations are optional
    because Dart can infer types. In the code above, `number`
    is inferred to be of type `int`. When you want to explicitly say
    that no type is expected,
    [use the special type `dynamic`][ObjectVsDynamic]. -->

-   Dart支持泛型，比如`List<int>`（一个整数列表）或者`List<dynamic>`（一个可以是任意类型的列表）
<!-- -   Dart supports generic types, like `List<int>` (a list of integers)
    or `List<dynamic>` (a list of objects of any type). -->

-   Dart支持顶级-top-level函数（比如`main()`），类「*class*」函数
    （也叫做静态「*static*」方法）和对象「*object*」函数（也叫做实例「*instance*」方法）。
    您也可以在函数里创建函数（也叫做嵌套函数/本地函数）
<!-- -   Dart supports top-level functions (such as `main()`), as well as
    functions tied to a class or object (*static* and *instance
    methods*, respectively). You can also create functions within
    functions (*nested* or *local functions*). -->

-   类似的，Dart支持顶级-top-level变量，类「*class*」变量（也叫做静态「*static*」变量）
    和对象「*object*」变量（也叫做实例「*instance*」变量）。实例变量也被称为字段「*field*」或
    者属性「*properties*」。
<!-- -   Similarly, Dart supports top-level *variables*, as well as variables
    tied to a class or object (static and instance variables). Instance
    variables are sometimes known as fields or properties. -->

-   不同于Java，Dart没有`public`，`protected`和`private`关键词。
    如果一个标识符「*identifier*」以一个下划线（_）开始，那么这就是类库所
    私有的。更多的细节，参考[Libraries and visibility](https://www.dartlang.org/guides/language/language-tour#libraries-and-visibility)。
<!-- -   Unlike Java, Dart doesn’t have the keywords `public`, `protected`,
    and `private`. If an identifier starts with an underscore (\_), it’s
    private to its library. For details, see
    [Libraries and visibility](#libraries-and-visibility). -->

-   标识符「*identifier*」需要以一个字母或者下划线（\_）开头，其他的部分可以是任意的字母或数字的组合。
<!-- -   *Identifiers* can start with a letter or underscore (\_), followed by any
    combination of those characters plus digits.-->

-   我们需要分清一段代码是表达式「*expression*」还是声明「*statement*」，这很有帮助
<!-- -   Sometimes it matters whether something is an *expression* or a
    *statement*, so it helps to be precise about those two words. -->

-   Dart tools 可以提示两种问题：警告和错误。警告只是提示你的代码可能不会工作，
    但是他们不会阻止你的程序运行。错误可以是编译时或者运行时。一个编译时错误会让
    代码无法执行；一个运行时错误会在程序运行时抛出一个[异常「*exception*」](#exceptions)。

<!-- -   Dart tools can report two kinds of problems: warnings and errors.
    Warnings are just indications that your code might not work, but
    they don’t prevent your program from executing. Errors can be either
    compile-time or run-time. A compile-time error prevents the code
    from executing at all; a run-time error results in an
    [exception](#exceptions) being raised while the code executes. -->


## 关键词
<!-- ## Keywords -->

下面的表格列出了Dart语言中的特殊单词。
<!-- The following table lists the words that the Dart language treats specially. -->

{% assign bii = '&nbsp;<sup title="built-in-identifier" alt="built-in-identifier">1</sup>' %}
{% assign lrw = '&nbsp;<sup title="limited reserved word" alt="limited reserved word">2</sup>' %}

| abstract{{bii}}   | do                | import{{bii}}     | super             |
| as{{bii}}         | dynamic{{bii}}    | in                | switch            |
| assert            | else              | interface{{bii}}  | sync*{{lrw}}      |
| async{{lrw}}      | enum              | is                | this              |
| async*{{lrw}}     | export{{bii}}     | library{{bii}}    | throw             |
| await{{lrw}}      | external{{bii}}   | mixin{{bii}}      | true              |
| break             | extends           | new               | try               |
| case              | factory{{bii}}    | null              | typedef{{bii}}    |
| catch             | false             | operator{{bii}}   | var               |
| class             | final             | part{{bii}}       | void              |
| const             | finally           | rethrow           | while             |
| continue          | for               | return            | with              |
| covariant{{bii}}  | get{{bii}}        | set{{bii}}        | yield{{lrw}}      |
| default           | if                | static{{bii}}     | yield*{{lrw}}     |
| deferred{{bii}}   | implements{{bii}}
{:.table .table-striped .nowrap}

以<sup>1</sup>为后缀的单词是 **内置标识符「*built-in identifiers*」**。避免使用内置标识符作为标识符。如果你用内置标识符作为类名或者类型名，会产生一个编译时错误。
<!-- <sup>1</sup> Words with the superscript **1**
are **built-in identifiers**. Avoid using
built-in identifiers as identifiers.
A compile-time error happens if you try to
use a built-in identifier for a class or type name. -->

以<sup>2</sup>为后缀的是新加入的，在Dart 1.0之后为了 **异步(asynchrony)** 支持所部分限制的保留单词。你不能在标记为`async`, `async*`, 或者 `sync*`的函数中使用`async`, `await`, 或者`yield` 作为标识符。更多的信息，参考[异步支持「*Asynchrony support*」](https://www.dartlang.org/guides/language/language-tour#asynchrony-support)。
<!-- <sup>2</sup> Words with the superscript **2**
are newer, limited reserved words related to **asynchrony** support
added after Dart's 1.0 release.
You can't use `async`, `await`, or `yield` as
an identifier in any function body marked with `async`, `async*`, or `sync*`.
For more information, see
[Asynchrony support](#asynchrony-support). -->

所有其他在关键词表格中的单词都是 **保留单词**，你不能使用保留单词作为标识符。
<!-- All other words in the keyword table are **reserved words**.
You can't use reserved words as identifiers. -->

## 变量
<!-- ## Variables -->

下面是一个创建和初始化变量的例子：
<!-- Here’s an example of creating a variable and initializing it: -->

<?code-excerpt "misc/lib/language_tour/variables.dart (var-decl)"?>
{% prettify dart %}
var name = 'Bob';
{% endprettify %}

变量储存了引用「*references*」。这个叫做`name`的变量包含了一个引用，这个引用指向了一个值为“Bob”的`String`对象。 
<!-- Variables store references. The variable called `name` contains a
reference to a `String` object with a value of “Bob”. -->

变量`name`的类型`String`是被推导得到的，但是你也可以明确的指定它的类型。如果一个对象不想被限定为一个单一的类型，根据 [design guidelines](https://www.dartlang.org/guides/language/effective-dart/design#do-annotate-with-object-instead-of-dynamic-to-indicate-any-object-is-allowed)，可以指定它的类型为`Object` 或者 `dynamic`。
<!-- The type of the `name` variable is inferred to be `String`,
but you can change that type by specifying it.
If an object isn't restricted to a single type,
specify the `Object` or `dynamic` type, following
[design guidelines][ObjectVsDynamic]. -->

{% comment %}
**[PENDING: check on Object vs. dynamic guidance.]**
{% endcomment %}

<?code-excerpt "misc/lib/language_tour/variables.dart (type-decl)"?>
{% prettify dart %}
dynamic name = 'Bob';
{% endprettify %}

另外一种显式声明推导类型的方法：
<!-- Another option is to explicitly declare the type that would be inferred: -->

<?code-excerpt "misc/lib/language_tour/variables.dart (static-types)"?>
{% prettify dart %}
String name = 'Bob';
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**对于本地变量，本页遵循了[style guide recommendation](/guides/language/effective-dart/design#types)使用了`var`，而不是类型声明。
<!-- **Note:**
This page follows the
[style guide recommendation](/guides/language/effective-dart/design#types)
of using `var`, rather than type annotations, for local variables. -->
</div>


### 默认值
<!-- ### Default value -->

没有被初始化的变量有一个初始值`null`，即使是数字类型变量的初始值也是`null`（而不是`0`），因为数字，和其他所有Dart中的东西一样，都是对象（object）。
<!-- Uninitialized variables have an initial value of `null`. Even variables
with numeric types are initially null, because numbers—like everything
else in Dart—are objects. -->

<?code-excerpt "misc/test/language_tour/variables_test.dart (var-null-init)"?>
{% prettify dart %}
int lineCount;
assert(lineCount == null);
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**这里的`assert()`会在生产代码中忽视掉。在开发中，如果<code>assert(<em>condition</em>)</code>中的 *condition*是错的，那么程序会抛出一个错误。更多的信息，请参考[Assert](#assert)。
<!-- **Note:**
The `assert()` call is ignored in production code.
During development, <code>assert(<em>condition</em>)</code>
throws an exception unless *condition* is true. For details,
see [Assert](#assert). -->
</div>


### Final和const
<!-- ### Final and const -->

如果你确定永远不会改变一个变量的引用，请使用`final`或者`const`，而不是`var`或者一个类型。一个`final`变量只能被设置一次；一个`const`变量是一个编译时常数。（Const变量是隐式的final。）运行时，一个final的顶级或者类变量会在其第一次被使用时初始化。
<!-- If you never intend to change a variable, use `final` or `const`, either
instead of `var` or in addition to a type. A final variable can be set
only once; a const variable is a compile-time constant. (Const variables
are implicitly final.) A final top-level or class variable is initialized
the first time it's used. -->

<div class="alert alert-info" markdown="1">
**注意：**实例变量只能是`final`，而不能是`const`。（因为实例无法在编译时创建）
<!-- **Note:**
Instance variables can be `final` but not `const`. -->
</div>

这里有一个创建和设置final变量的例子
<!-- Here's an example of creating and setting a final variable: -->

<?code-excerpt "misc/lib/language_tour/variables.dart (final)"?>
{% prettify dart %}
final name = 'Bob'; // 没有类型声明
// name = 'Alice';  // 掉这行的注释会导致一个错误
final String nickname = 'Bobby';
{% endprettify %}

如果你想要编译时常数，请使用`const`。如果const变量在类中，标记为`static const`。在你声明变量的地方，请设置值为一个编译时常量，可以是一个数字字面量、字符串字面量、一个const变量、一个基于常量数字的数学表达式结果。
<!-- Use `const` for variables that you want to be compile-time constants. If
the const variable is at the class level, mark it `static const`.
Where you declare the variable, set the value to a compile-time constant
such as a number or string literal, a const
variable, or the result of an arithmetic operation on constant numbers: -->

<?code-excerpt "misc/lib/language_tour/variables.dart (const)"?>
{% prettify dart %}
const bar = 1000000; // 大气单位 (dynes/cm2)
const double atm = 1.01325 * bar; // 标准大气压
{% endprettify %}

`const`关键词不仅仅可以用来声明常数变量。您还可以使用它来创建常数值，以及用来声明创建常数值的constructors。任何变量都可以有一个常数值
<!-- The `const` keyword isn't just for declaring constant variables.
You can also use it to create constant _values_,
as well as to declare constructors that _create_ constant values.
Any variable can have a constant value. -->

<?code-excerpt "misc/lib/language_tour/variables.dart (const-vs-final)"?>
{% prettify dart %}
// 注意: [] 创建了一个空列表
// const [] 创建了一个空的，不变的列表（EIF）
var foo = const []; // foo 是一个EIL
final bar = const []; // bar 将只能是EIL
const baz = const []; // baz是一个编译时常量EIL

// 你可以改变一个不是fianl，且不是const的变量
// 即使他的值是一个常数值
foo = [];

// 你不能改变一个final或者const变量的值
// bar = []; // 未处理异常。
// baz = []; // 未处理异常。
{% endprettify %}

关于使用`const`来创建常数值的更多信息，请参考[Lists](#lists), [Maps](#maps), 和 [Classes](#classes).
<!-- For more information on using `const` to create constant values, see
[Lists](#lists), [Maps](#maps), and [Classes](#classes). -->


## 内置类型
<!-- ## Built-in types -->

Dart语言特别支持了下列的类型
<!-- The Dart language has special support for the following types: -->


- numbers 数字
- strings 字符串
- booleans 布尔值
- lists (also known as *arrays*) 列表（也叫做数组）
- maps 字典/地图
- runes (for expressing Unicode characters in a string) 字母（用来在string中表示Unicode字符, 类似char）
- symbols 符号

你可以用字面量来创建其中一个特殊类型的对象。比如，`'this is a string'`是一个字符串字面量，而`true`是一个布尔字面量。
<!-- You can initialize an object of any of these special types using a
literal. For example, `'this is a string'` is a string literal,
and `true` is a boolean literal. -->

{% comment %}
PENDING: add info about support for Iterable, Future, Stream?
Those can't be initialized using literals, but they do have special support.
{% endcomment %}

因为每个变量在Dart中都引用了一个对象（一个类的实例），你可以使用构造函数constructors来初始化变量。有一些内置类型有他们自己的构造函数。比如你可以使用`Map()`构造函数来创建一个map，代码如下`new Map()`。
<!-- Because every variable in Dart refers to an object—an instance of a
*class*—you can usually use *constructors* to initialize variables. Some
of the built-in types have their own constructors. For example, you can
use the `Map()` constructor to create a map, using code such as
`new Map()`. -->


### 数字-Numbers
<!-- ### Numbers -->

Dart有如下两种“风味”的数字
<!-- Dart numbers come in two flavors: -->

[int][]

:   根据所属的平台，整形值通常不能大于64个bit。在Dart Vm中，可以是从 -2<sup>63</sup> 到 2<sup>63</sup> - 1的值。编译到JS的Dart使用[JavaScript numbers，](https://stackoverflow.com/questions/2802957/number-of-bits-in-javascript-numbers/2803010#2803010)允许从-2<sup>53</sup> 到 2<sup>53</sup> - 1的值。
<!-- :   Integer values no larger than 64 bits,
    depending on the platform.
    On the Dart VM, values can be from
    -2<sup>63</sup> to 2<sup>63</sup> - 1.
    Dart that's compiled to JavaScript uses
    [JavaScript numbers,][js numbers]
    allowing values from -2<sup>53</sup> to 2<sup>53</sup> - 1. -->

{% comment %}
[PENDING: What about values on Android & iOS?
The informal spec is at
https://github.com/dart-lang/sdk/blob/master/docs/language/informal/int64.md.
{% endcomment %}

[double][]
:   64-bit（双精度）浮点数，基于IEEE 754标准。
<!-- :   64-bit (double-precision) floating-point numbers, as specified by
    the IEEE 754 standard. -->


`int`和`double`都是 [`num`](https://api.dartlang.org/dev/dart-core/num-class.html)类型的子类型。num类型包含了基本的+、-、/、*运算符，你也能找到`abs()`,` ceil()`，和`floor()`，以及其他的方法。（注意：bit级操作，比如>>，只定义在了`int`类中，`double`没有。）如果num和它的子类没有你需要的运算，[dart:math](https://api.dartlang.org/dev/dart-math)类库中应该会有。
<!-- Both `int` and `double` are subtypes of [`num`.][num]
The num type includes basic operators such as +, -, /, and \*,
and is also where you’ll find `abs()`,` ceil()`,
and `floor()`, among other methods.
(Bitwise operators, such as \>\>, are defined in the `int` class.)
If num and its subtypes don’t have what you’re looking for, the
[dart:math][] library might. -->


整数是没有小数的数字。如下是一些定义了整数字面量的例子
<!-- Integers are numbers without a decimal point. Here are some examples of
defining integer literals: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (integer-literals)"?>
{% prettify dart %}
int x = 1;
int hex = 0xDEADBEEF;
{% endprettify %}

如果数字包含了小数点，那它就是一个double。如下是一些定义了double字面量的例子
<!-- If a number includes a decimal, it is a double. Here are some examples
of defining double literals: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (double-literals)"?>
{% prettify dart %}
double y = 1.1;
double exponents = 1.42e5;
{% endprettify %}

下面的代码展示了如何相互转换字符串和数字
<!-- Here’s how you turn a string into a number, or vice versa: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (number-conversion)"?>
{% prettify dart %}
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
{% endprettify %}

int类型规定了传统的bit级别的位移（<<,>>）,于(&)，和非（|）操作。如下：
<!-- The int type specifies the traditional bitwise shift (\<\<, \>\>), AND
(&), and OR (|) operators. For example: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (bit-shifting)"?>
{% prettify dart %}
assert((3 << 1) == 6); // 0011 << 1 == 0110
assert((3 >> 1) == 1); // 0011 >> 1 == 0001
assert((3 | 4) == 7); // 0011 | 0100 == 0111
{% endprettify %}

字面量数字是编译时常量。许多数学操作也是编译时常量，只要它的运算值是编译时的数字常量值。
<!-- Literal numbers are compile-time constants.
Many arithmetic expressions are also compile-time constants,
as long as their operands are
compile-time constants that evaluate to numbers. -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (const-num)"?>
{% prettify dart %}
const msPerSecond = 1000;
const secondsUntilRetry = 5;
const msUntilRetry = secondsUntilRetry * msPerSecond;
{% endprettify %}


### 字符串-Strings
<!-- ### Strings -->

一个Dart string表示了一个UTF-16编码串。您可以使用单引号或者双引号来创建一个string。
<!-- A Dart string is a sequence of UTF-16 code units. You can use either
single or double quotes to create a string: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (quoting)"?>
{% prettify dart %}
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
{% endprettify %}

您可以在string中使用`${`*`表达式`*`}`来把表达式的值放入string中。如果表达式是一个标识符，您可以省去{}。Dart可以调用对象的`toString()`方法来得到对象对应的字符串。
<!-- You can put the value of an expression inside a string by using
`${`*`expression`*`}`. If the expression is an identifier, you can skip
the {}. To get the string corresponding to an object, Dart calls the
object’s `toString()` method. -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (string-interpolation)"?>
{% prettify dart %}
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, ' +
        'which is very handy.');
assert('That deserves all caps. ' +
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. ' +
        'STRING INTERPOLATION is very handy!');
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**`==`运算符测试了两个对象是否相等。两个string在他们包含相同顺序的编码时是相等的。
<!-- **Note:**
The `==` operator tests whether two objects are equivalent. Two
strings are equivalent if they contain the same sequence of code
units. -->
</div>

您可以直接把两个相邻的string字面量链接在一起，也可以用`+`运算符。
<!-- You can concatenate strings using adjacent string literals or the `+`
operator: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (adjacent-string-literals)"?>
{% prettify dart %}
var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
assert(s1 ==
    'String concatenation works even over '
    'line breaks.');

var s2 = 'The + operator ' + 'works, as well.';
assert(s2 == 'The + operator works, as well.');
{% endprettify %}

还有一种创建多行string的方式：使用三个双引号或者单引号。
<!-- Another way to create a multi-line string: use a triple quote with
either single or double quotation marks: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (triple-quotes)"?>
{% prettify dart %}
var s1 = '''
您可以像这样
生产多行字符串
''';

var s2 = """This is also a
multi-line string.""";
{% endprettify %}

您也可以用一个r开头来创建一个没有特殊字符的“生”string。但如果用三个双引号或者单引号是可以实现在生stirng中换行的。
<!-- You can create a “raw” string by prefixing it with `r`: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (raw-strings)"?>
{% prettify dart %}
var c = r"在生string中, 即使\n也不会换行.";
var s = r"""但是用三个双引号或者单引号, 
是可以\n换行的.""";
{% endprettify %}

想知道如何在字符串中表达Unicode字符，请查看[Runes](#runes)。
<!-- See [Runes](#runes) for details on how to express Unicode
characters in a string. -->

字面量string是编译时常量。而如果字符解析式中所有表达式的结果都为数字值、字符值、或者是布尔值的编译时常量，字符解析式也是编译时常量。
<!-- Literal strings are compile-time constants,
as long as any interpolated expression is a compile-time constant
that evaluates to null or a numeric, string, or boolean value. -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (string-literals)"?>
{% prettify dart %}
// 这些可以在const string中使用
const aConstNum = 0;
const aConstBool = true;
const aConstString = 'a constant string';

// 这些不能在const string中使用
var aNum = 0;
var aBool = true;
var aString = 'a string';
const aConstList = const [1, 2, 3];

const validConstString = '$aConstNum $aConstBool $aConstString';
// const invalidConstString = '$aNum $aBool $aString $aConstList';
{% endprettify %}

更多关于string的信息，参考 [Strings and regular expressions](https://www.dartlang.org/guides/libraries/library-tour#strings-and-regular-expressions)。
<!-- For more information on using strings, see
[Strings and regular expressions](/guides/libraries/library-tour#strings-and-regular-expressions). -->


### 布尔-Booleans

对于用来表示布尔值，Dart使用了`bool`类型名。只有两个对象是bool类型：就是布尔字面量`true`和`false`，它们都是编译时常量。
<!-- To represent boolean values, Dart has a type named `bool`. Only two
objects have type bool: the boolean literals `true` and `false`,
which are both compile-time constants. -->

Dart的类型安全意味着你不能使用<code>if (<em>nonbooleanValue</em>)</code>或者<code>assert (<em>nonbooleanValue</em>)</code>。反之，你必须显式地检查值，比如这样：
<!-- Dart's type safety means that you can't use code like
<code>if (<em>nonbooleanValue</em>)</code> or
<code>assert (<em>nonbooleanValue</em>)</code>.
Instead, explicitly check for values, like this: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (no-truthy)"?>
{% prettify dart %}
// 检查空字符串
var fullName = '';
assert(fullName.isEmpty);

// 检查0
var hitPoints = 0;
assert(hitPoints <= 0);

// 检查null
var unicorn;
assert(unicorn == null);

// 检查NaN
var iMeantToDoThis = 0 / 0;
assert(iMeantToDoThis.isNaN);
{% endprettify %}


### 列表-Lists

也许所有编程语言中最常见的集合就是*array*，或者是有序的对象组。在Dart中，arrays是[List][]对象，所以大部分人直接叫他们*lists*。
<!-- Perhaps the most common collection in nearly every programming language
is the *array*, or ordered group of objects. In Dart, arrays are
[List][] objects, so most people just call them *lists*. -->

Dart的list字面量看起来很像JavaScript的数组字面量。
<!-- Dart list literals look like JavaScript array literals. Here’s a simple
Dart list: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (list-literal)"?>
{% prettify dart %}
var list = [1, 2, 3];
{% endprettify %}

<aside class="alert alert-info" markdown="1">
**注意：**这会推断`list`有类`List<int>`。如果您试图添加不是整形的对象进入列表，运行时会产生一个错误。更多的信息，参考[type inference。](/guides/language/sound-dart#type-inference)
  <!-- **Note:**
  The analyzer infers that `list` has type `List<int>`.
  If you try to add non-integer objects to this list,
  the analyzer or runtime raises an error.
  For more information, read about
  [type inference.](/guides/language/sound-dart#type-inference) -->
</aside>

Lists使用0位开头的序列，所以0就是第一个元素的index，而`list.length - 1`就是最后一个元素的index。您可以像在JavaScript中一样拿到列表的长度或取到对应index的元素。
<!-- Lists use zero-based indexing, where 0 is the index of the first element
and `list.length - 1` is the index of the last element. You can get a
list’s length and refer to list elements just as you would in
JavaScript: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (list-indexing)"?>
{% prettify dart %}
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
{% endprettify %}

要创建一个编译时常量，在list字面量前添加`const`。
<!-- To create a list that's a compile-time constant,
add `const` before the list literal: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (const-list)"?>
{% prettify dart %}
var constantList = const [1, 2, 3];
// constantList[1] = 1; // Uncommenting this causes an error.
{% endprettify %}

List类型后很多实用的方法。更多的信息，参考[Generics](https://www.dartlang.org/guides/language/language-tour#generics) 和[Collections](/guides/libraries/library-tour#collections).
<!-- The List type has many handy methods for manipulating lists. For more
information about lists, see [Generics](#generics) and
[Collections](/guides/libraries/library-tour#collections). -->


### 字典-Maps

通常意义上来说，一个map对象就是键keys和值values的关联。key和value可以是任何类型的对象。每个*key*只会有一个，但你可以多次使用相同对的*value*。Dart对于Map的支持是由map字面量和[Map][]类型提供的。
<!-- In general, a map is an object that associates keys and values. Both
keys and values can be any type of object. Each *key* occurs only once,
but you can use the same *value* multiple times. Dart support for maps
is provided by map literals and the [Map][] type. -->

如下是一些简单的Dart maps，由map字面量创建：
<!-- Here are a couple of simple Dart maps, created using map literals: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (map-literal)"?>
{% prettify dart %}
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
{% endprettify %}

<aside class="alert alert-info" markdown="1">
**注意：**解析器推断`gifts`的类型是`Map<String, String>`，`nobleGases`的类型是`Map<int, String>`。如果你向任意map中添加了错误的类型，那么会产生一个解析时或运行时错误。更多的信息，参考[type inference.](/guides/language/sound-dart#type-inference)
  <!-- **Note:**
  The analyzer infers that `gifts` has the type
  `Map<String, String>` and `nobleGases` has the type
  `Map<int, String>`. If you try to add the wrong type of value
  to either map, the analyzer or runtime raises an error.
  For more information, read about
  [type inference.](/guides/language/sound-dart#type-inference) -->
</aside>

你可以用Map构造方法创建一样的对象：
<!-- You can create the same objects using a Map constructor: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (map-constructor)"?>
{% prettify dart %}
var gifts = new Map();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = new Map();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
{% endprettify %}

可以像在JavaScript中一样向一个已经存在的map添加新的键值对：
<!-- Add a new key-value pair to an existing map just as you would in
JavaScript: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (map-add-item)"?>
{% prettify dart %}
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
{% endprettify %}

也可以像在JavaScript中一样从已经存在的map中通过key来取值：
<!-- Retrieve a value from a map the same way you would in JavaScript: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (map-retrieve-item)"?>
{% prettify dart %}
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
{% endprettify %}

如果你查找的key不在map中，你会得到一个null返回值：
<!-- If you look for a key that isn’t in a map, you get a null in return: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (map-missing-key)"?>
{% prettify dart %}
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
{% endprettify %}

使用`.length`可以得到map中键值对的数量：
<!-- Use `.length` to get the number of key-value pairs in the map: -->

<?code-excerpt "misc/test/language_tour/built_in_types_test.dart (map-length)"?>
{% prettify dart %}
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
{% endprettify %}

要创建一个编译时常量的map，在map字面量前面添加`const`关键字：
<!-- To create a map that's a compile-time constant,
add `const` before the map literal: -->

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (const-map)"?>
{% prettify dart %}
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// constantMap[2] = 'Helium'; // Uncommenting this causes an error.
{% endprettify %}

关于map更多的信息，参考 [Generics](#generics) 和 [Maps](/guides/libraries/library-tour#maps).
<!-- For more information about maps, see
[Generics](#generics) and
[Maps](/guides/libraries/library-tour#maps). -->

### 字码-Runes

在Dart中，字runes是字符串中的UTF-32码位。
<!-- In Dart, runes are the UTF-32 code points of a string. -->

Unicode为每一个在世界上用于书写的字母，数字，符号定义了一个特殊的数字值。因为Dart的字符串是一串UTF-16单元，在字符串中表达32-bit的unicode需要特殊的语法。
<!-- Unicode defines a unique numeric value for each letter, digit,
and symbol used in all of the world's writing systems.
Because a Dart string is a sequence of UTF-16 code units,
expressing 32-bit Unicode values within a string requires
special syntax. -->

正常表示Unicode的方法是`\uXXXX`，XXXX是个4位16进制数字。举个例子，心符号（♥）是`\u2665`。要表示大于或者小于4位的符号，要在值外添加大括号。举个例子，大笑的emoji（😆) 是 `\u{1f600}`.
<!-- The usual way to express a Unicode code point is
`\uXXXX`, where XXXX is a 4-digit hexidecimal value.
For example, the heart character (♥) is `\u2665`.
To specify more or less than 4 hex digits,
place the value in curly brackets.
For example, the laughing emoji (😆) is `\u{1f600}`. -->

您可以使用[String][]类有一些属性来提取rune信息。`codeUnitAt`和`codeUnit`属性返回了16-bit单位。使用`runes`属性来提取string中的runes。
<!-- The [String][]
class has several properties you can use to extract rune information.
The `codeUnitAt` and `codeUnit` properties return 16-bit code
units. Use the `runes` property to get the runes of a string. -->

下面的这个例子描述了runes、16bit单位和32bit单位之间的关系，点击红色按钮( {% img 'red-run.png' %} )查看runes的结果。
<!-- The following example illustrates the relationship between runes,
16-bit code units, and 32-bit code points.
Click the run button ( {% img 'red-run.png' %} )
to see runes in action. -->

{% comment %}
https://gist.github.com/589bc5c95318696cefe5
https://dartpad.dartlang.org/589bc5c95318696cefe5
Unicode emoji: http://unicode.org/emoji/charts/full-emoji-list.html

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (runes)"?>
{% prettify dart %}
void main() {
  var clapping = '\u{1f44f}';
  print(clapping);
  print(clapping.codeUnits);
  print(clapping.runes.toList());

  Runes input = new Runes(
      '\u2665  \u{1f605}  \u{1f60e}  \u{1f47b}  \u{1f596}  \u{1f44d}');
  print(new String.fromCharCodes(input));
}
{% endprettify %}
{% endcomment %}

<iframe
src="{{site.custom.dartpad.embed-dart-prefix}}?id=589bc5c95318696cefe5&horizontalRatio=99&verticalRatio=65"
    width="100%"
    height="310px"
    style="border: 1px solid #ccc;">
</iframe>

<div class="alert alert-warning" markdown="1">
**注意：**要十分小心地在runes上使用list操作。基于特定的语言、字符集和操作，这很容易使代码崩溃。更多的信息，参考 Stack Overflow上的 [How do I reverse a String in Dart?](http://stackoverflow.com/questions/21521729/how-do-i-reverse-a-string-in-dart)
<!-- **Note:**
Be careful when manipulating runes using list operations.
This approach can easily break down,
depending on the particular language, character set, and operation.
For more information, see
[How do I reverse a String in Dart?](http://stackoverflow.com/questions/21521729/how-do-i-reverse-a-string-in-dart) on Stack Overflow. -->
</div>

### 符号 - Symbols

一个 [符号Symbol][]对象表示了一个Dart语言中的运算值或者标识符。您也许永远不会使用到symbols，但他们对于使用名称引用标识符的API十分宝贵，因为代码混淆压缩时只有标识符名称会改变，但是标识符符号不会。
<!-- A [Symbol][] object
represents an operator or identifier declared in a Dart program. You
might never need to use symbols, but they're invaluable for APIs that
refer to identifiers by name, because minification changes identifier
names but not identifier symbols. -->

要获取一个标识符的符号，使用符号字面量，即一个`#`跟着标识符。
<!-- To get the symbol for an identifier, use a symbol literal, which is just
`#` followed by the identifier: -->

```nocode
#radix
#bar
```

{% comment %}
The code from the following excerpt isn't actually what is being shown in the page

<?code-excerpt "misc/lib/language_tour/built_in_types.dart (symbols)"?>
{% prettify dart %}
// MOVE TO library tour?

void main() {
  print(Function.apply(int.parse, ['11']));
  print(Function.apply(int.parse, ['11'], {#radix: 16}));
  print(Function.apply(int.parse, ['11a'], {#onError: handleError}));
  print(Function
      .apply(int.parse, ['11a'], {#radix: 16, #onError: handleError}));
}

int handleError(String source) {
  return 0;
}
{% endprettify %}
{% endcomment %}

符号字面量是编译时常量。
<!-- Symbol literals are compile-time constants. -->


## 函数
<!-- ## Functions -->

Dart是一个纯正的面向对象语言，所以它的函数也是类型为 [Function][]的对象。这意味着函数可以被赋值给一个变量或者作为参数传入其他函数。你可以把一个dart类的实例当作函数调取。更多的细节，参考[Callable classes](#callable-classes)。
<!-- Dart is a true object-oriented language, so even functions are objects
and have a type, [Function][].
This means that functions can be assigned to variables or passed as arguments
to other functions. You can also call an instance of a Dart class as if
it were a function. For details, see [Callable classes](#callable-classes). -->

如下是一个实现方法的例子：
<!-- Here’s an example of implementing a function: -->

<?code-excerpt "misc/lib/language_tour/functions.dart (function)"?>
{% prettify dart %}
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
{% endprettify %}

尽管Effective Dart[type annotations for public APIs](/guides/language/effective-dart/design#prefer-type-annotating-public-fields-and-top-level-variables-if-the-type-isnt-obvious)推荐在公共API中标明类型，但是忽略类型的函数也是可以工作的。
<!-- Although Effective Dart recommends
[type annotations for public APIs](/guides/language/effective-dart/design#prefer-type-annotating-public-fields-and-top-level-variables-if-the-type-isnt-obvious),
the function still works if you omit the types: -->

<?code-excerpt "misc/lib/language_tour/functions.dart (function-omitting-types)"?>
{% prettify dart %}
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
{% endprettify %}

对于那些只有一行表达式的函数，您可以使用简化的语法：
<!-- For functions that contain just one expression, you can use a shorthand
syntax: -->

<?code-excerpt "misc/lib/language_tour/functions.dart (function-shorthand)"?>
{% prettify dart %}
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
{% endprettify %}

<code>=> <em>expr</em></code>的语法是<code>{ return <em>expr</em>; }</code>的简写。`=>`的写法被称为 _箭头_ 函数。
<!-- The <code>=> <em>expr</em></code> syntax is a shorthand for
<code>{ return <em>expr</em>; }</code>. The `=>` notation
is sometimes referred to as _fat arrow_ syntax. -->

<div class="alert alert-info" markdown="1">
**注意：**只有表达式可以出现在箭头(=>)和分号(;)之间，而声明不行。举个例子，你不能把[if 声明式（statement）](#if-and-else)放在他们之间，但你可以使用[条件表达式conditional expression](#conditional-expressions)。
<!-- **Note:**
Only an *expression*—not a *statement*—can appear between the arrow
(=\>) and the semicolon (;). For example, you can’t put an [if
statement](#if-and-else) there, but you can use a [conditional
expression](#conditional-expressions). -->
</div>

一个函数可以用两种参数：必填的和可选的。必填参数在前，可选参数在后。
<!-- A function can have two types of parameters: required and optional. The
required parameters are listed first, followed by any optional
parameters. -->

### 可选参数
<!-- ### Optional parameters -->

可选参数可以是定好位置的或者是被命名的，但不能两者都是。
<!-- Optional parameters can be either positional or named, but not both. -->

#### 可选命名参数
<!-- #### Optional named parameters -->

当调用一个函数的时候，你可以通过<code><em>paramName</em>: <em>value</em></code>来确定参数的名称：
<!-- When calling a function, you can specify named parameters using
<code><em>paramName</em>: <em>value</em></code>. For example: -->

<?code-excerpt "misc/lib/language_tour/functions.dart (use-named-parameters)"?>
{% prettify dart %}
enableFlags(bold: true, hidden: false);
{% endprettify %}

当定义一个函数的时候，你可以通过<code>{<em>param1</em>, <em>param2</em>, …}</code>来确定参数的名称：
<!-- When defining a function, use
<code>{<em>param1</em>, <em>param2</em>, …}</code>
to specify named parameters: -->

<?code-excerpt "misc/lib/language_tour/functions.dart (specify-named-parameters)"?>
{% prettify dart %}
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold, bool hidden}) {
  // ...
}
{% endprettify %}

#### 可选定位参数
<!-- #### Optional positional parameters -->

用`[]`标记来包含一些函数的参数会将他们定义为可选的定位参数：
<!-- Wrapping a set of function parameters in `[]` marks them as optional
positional parameters: -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (optional-positional-parameters)"?>
{% prettify dart %}
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
{% endprettify %}

这有个例子说明了如何不传入可选参数：
<!-- Here’s an example of calling this function without the optional
parameter: -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (call-without-optional-param)"?>
{% prettify dart %}
assert(say('Bob', 'Howdy') == 'Bob says Howdy');
{% endprettify %}

这是另外一个例子，说明了传入可选的第三个参数的情况：
<!-- And here’s an example of calling this function with the third parameter: -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (call-with-optional-param)"?>
{% prettify dart %}
assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');
{% endprettify %}

<a id="default-parameters"></a>
#### 默认参数值
<!-- #### Default parameter values -->

你的函数可以使用`=`来为命名参数或者定位参数定义默认值。默认值必须为编译时常量。如果没有提供，则默认值为`null`。
<!-- Your function can use `=` to define default values for both named and positional
parameters. The default values must be compile-time constants.
If no default value is provided, the default value is `null`. -->

如下是一个为命名参数设定默认值的例子：
<!-- Here's an example of setting default values for named parameters: -->

<?code-excerpt "misc/lib/language_tour/functions.dart (named-parameter-default-values)"?>
{% prettify dart %}
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {
  // ...
}

// bold will be true; hidden will be false.
enableFlags(bold: true);
{% endprettify %}

<div class="alert alert-info" markdown="1">
**废除通知：**
老的代码中也许有使用冒号`:`，而不是等号`=`用来设置默认命名参数值。原因是老版本只能用`:`来定义默认值。但冒号的支持后续可能会被废除，所以我们推荐您**[使用=来确定默认值。](/tools/pub/pubspec#sdk-constraints)**
<!-- **Deprecation note:**
Old code might use a colon (`:`) instead of `=`
to set default values of named parameters.
The reason is that originally, only `:` was supported for named parameters.
That support is likely to be deprecated,
so we recommend that you
**[use `=` to specify default values.](/tools/pub/pubspec#sdk-constraints)** -->
</div>

{% comment %}
PENDING: I don't see evidence that we've dropped support for `:`.
Update if/when we do. Issue #?
See `defaultNamedParameter` in the language spec.
{% endcomment %}

下面的例子说明了如何为定位参数设置默认值：
<!-- The next example shows how to set default values for positional parameters: -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (optional-positional-param-default)"?>
{% prettify dart %}
String say(String from, String msg,
    [String device = 'carrier pigeon', String mood]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  if (mood != null) {
    result = '$result (in a $mood mood)';
  }
  return result;
}

assert(say('Bob', 'Howdy') ==
    'Bob says Howdy with a carrier pigeon');
{% endprettify %}

您也可以说使用列表或者字典来作为默认值。如下展示了一个定义函数的例子，`doStuff()`函数为它的`list`参数定义了一个默认的列表，并为它的`gifts`参数定义了一个默认字典。
<!-- You can also pass lists or maps as default values.
The following example defines a function, `doStuff()`,
that specifies a default list for the `list`
parameter and a default map for the `gifts` parameter. -->
{% comment %}
The function is called three times with different values.
Click the run button ( {% img 'red-run.png' %} )
to see list and map default values in action.
{% endcomment %}

<?code-excerpt "misc/lib/language_tour/functions.dart (list-map-default-function-param)"?>
{% prettify dart %}
void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list:  $list');
  print('gifts: $gifts');
}
{% endprettify %}

{% comment %}
https://gist.github.com/d988cfce0a54c6853799
https://dartpad.dartlang.org/d988cfce0a54c6853799
(The gist needs updating: see https://github.com/dart-lang/site-www/issues/189)
<iframe
src="{{site.custom.dartpad.embed-dart-prefix}}?id=d988cfce0a54c6853799&horizontalRatio=99&verticalRatio=70"
    width="100%"
    height="450px"
    style="border: 1px solid #ccc;">
</iframe>
{% endcomment %}


### mian()函数
<!-- ### The main() function -->

每个app都必须有一个顶层的`mian()`函数作为程序的入口。`mian()`函数返回`void`并且有一个可选的`List<String>`参数用来调用。
<!-- Every app must have a top-level `main()` function, which serves as the
entrypoint to the app. The `main()` function returns `void` and has an
optional `List<String>` parameter for arguments. -->

如下是一个web应用的`main()`函数例子：
<!-- Here's an example of the `main()` function for a web app: -->

<?code-excerpt "misc/test/language_tour/browser_test.dart (simple-web-main-function)"?>
{% prettify dart %}
void main() {
  querySelector('#sample_text_id')
    ..text = 'Click me!'
    ..onClick.listen(reverseText);
}
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**`..`语法被称为[联级操作cascade](#cascade-notation-)。通过使用cascades，您可以对单个对象进行连续的多次操作。
<!-- **Note:**
The `..` syntax in the preceding code is called a [cascade](#cascade-notation-).
With cascades,
you can perform multiple operations on the members of a single object. -->
</div>

下面的例子是一个对main函数传参的命令行程序。
<!-- Here's an example of the `main()` function for a command-line app that
takes arguments: -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (main-args)"?>
{% prettify dart %}
// Run the app like this: dart args.dart 1 test
void main(List<String> arguments) {
  print(arguments);

  assert(arguments.length == 2);
  assert(int.parse(arguments[0]) == 1);
  assert(arguments[1] == 'test');
}
{% endprettify %}

您可以使用[args类库args library](https://pub.dartlang.org/packages/args)来定义和解析命令行参数。
<!-- You can use the [args library](https://pub.dartlang.org/packages/args) to
define and parse command-line arguments. -->

### 作为顶级对象的函数
<!-- ### Functions as first-class objects -->

您可以把函数作为参数传入其他函数。如下所示：
<!-- You can pass a function as a parameter to another function. For example: -->

<?code-excerpt "misc/lib/language_tour/functions.dart (function-as-param)"?>
{% prettify dart %}
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
{% endprettify %}

您也可以把一个函数赋值给一个变量，如下：
<!-- You can also assign a function to a variable, such as: -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (function-as-var)"?>
{% prettify dart %}
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
{% endprettify %}

这个例子使用了匿名函数。下个章节会详细说明匿名函数。
<!-- This example uses an anonymous function.
More about those in the next section. -->

### 匿名函数
<!-- ### Anonymous functions -->

大部分函数是有名字的，比如`main()`或者`printElement()`。但您可以创建一个没有名字的函数，这被称为*匿名函数*，有时也叫做*lambda表达式*或者*闭包*。您可以把一个匿名函赋值给一个变量，也可以把它加入或者移出一个集合。
<!-- Most functions are named, such as `main()` or `printElement()`.
You can also create a nameless function
called an _anonymous function_, or sometimes a _lambda_ or _closure_.
You might assign an anonymous function to a variable so that,
for example, you can add or remove it from a collection. -->

匿名函数看起来和普通（有名）函数很像。0个或者更多的被逗号分开的参数，可选的在括号之间的类型标识符。
<!-- An anonymous function looks similar to a named function&mdash;
zero or more parameters, separated by commas
and optional type annotations, between parentheses. -->

紧接着的代码块则包含了函数体：
<!-- The code block that follows contains the function's body: -->

<code>
([[<em>Type</em>] <em>param1</em>[, …]]) { <br>
&nbsp;&nbsp;<em>codeBlock</em>; <br>
}; <br>
</code>

下面的例子定义了一个没有类型的匿名函数。这个函数会被列表里的每个元素调用，打印出当前元素的string值。
<!-- The following example defines an anonymous function with an untyped parameter, `item`.
The function, invoked for each item in the list,
prints a string that includes the value at the specified index. -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (anonymous-function)"?>
{% prettify dart %}
var list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
{% endprettify %}

点击红色按钮( {% img 'red-run.png' %} )来执行代码。
<!-- Click the run button ( {% img 'red-run.png' %} ) to execute the code. -->

{% comment %}
https://gist.github.com/chalin/5d70bc1889d055c7a18d35d77874af88
https://dartpad.dartlang.org/5d70bc1889d055c7a18d35d77874af88
{% endcomment %}

<iframe
src="{{site.custom.dartpad.embed-dart-prefix}}?id=5d70bc1889d055c7a18d35d77874af88&horizontalRatio=99&verticalRatio=50"
    width="100%"
    height="250px"
    style="border: 1px solid #ccc;">
</iframe>

如果函数只有一行代码，你可以使用缩写的箭头函数表达式。复制下列的代码到PartPad然后点击运行来确认他的功能是一样的。
<!-- If the function contains only one statement, you can shorten it using
fat arrow notation. Paste the following line into DartPad
and click run to verify that it is functionally equivalent. -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (anon-func)"?>
{% prettify dart %}
list.forEach(
    (item) => print('${list.indexOf(item)}: $item'));
{% endprettify %}

### 词法域
<!-- ### Lexical scope -->

Dart是一个词法域语言，这意味着他的变量作用域是根据代码结构静态确定的。您可以“从内到外跟从大括号”来确认变量的作用域。
<!-- Dart is a lexically scoped language, which means that the scope of
variables is determined statically, simply by the layout of the code.
You can “follow the curly braces outwards” to see if a variable is in
scope. -->

如下展现了一个在各层域级都有变量的嵌套函数的例子。
<!-- Here is an example of nested functions with variables at each scope
level: -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (nested-functions)"?>
{% prettify dart %}
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      assert(topLevel);
      assert(insideMain);
      assert(insideFunction);
      assert(insideNestedFunction);
    }
  }
}
{% endprettify %}

注意`nestedFunction()`可以使用每个等级的变量，一直到`main()`函数外的最顶级。
<!-- Notice how `nestedFunction()` can use variables from every level, all
the way up to the top level. -->

### 词法闭包
<!-- ### Lexical closures -->

*闭包*是一个函数对象，它不是在它原来的作用域中，但仍然可以获取它的词法作用域里的所有变量。
<!-- A *closure* is a function object that has access to variables in its
lexical scope, even when the function is used outside of its original
scope. -->

函数可以包含所有围绕它的作用域中的变量。在下面的例子中，`makeAddr()`纳入了`addBy`变量。不论这个返回的函数在那里，他都记住了`addBy`。
<!-- Functions can close over variables defined in surrounding scopes. In the
following example, `makeAdder()` captures the variable `addBy`. Wherever the
returned function goes, it remembers `addBy`. -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (function-closure)"?>
{% prettify dart %}
/// Returns a function that adds [addBy] to the
/// function's argument.
Function makeAdder(num addBy) {
  return (num i) => addBy + i;
}

void main() {
  // Create a function that adds 2.
  var add2 = makeAdder(2);

  // Create a function that adds 4.
  var add4 = makeAdder(4);

  assert(add2(3) == 5);
  assert(add4(3) == 7);
}
{% endprettify %}


### 如何测试函数相等
<!-- ### Testing functions for equality -->

如下是一个展示了测试顶级函数，静态方法和实例方法相等的例子：
<!-- Here's an example of testing top-level functions, static methods, and
instance methods for equality: -->

<?code-excerpt "misc/lib/language_tour/function_equality.dart"?>
{% prettify dart %}
void foo() {} // 一个顶级函数

class A {
  static void bar() {} // 一个静态方法
  void baz() {} // 一个实例方法
}

void main() {
  var x;

  // 比较顶级函数
  x = foo;
  assert(foo == x);

  // 比较静态方法
  x = A.bar;
  assert(A.bar == x);

  // 比较实例方法
  var v = new A(); // A的第一个实例
  var w = new A(); // A的第二个实例
  var y = w;       // 引用第二个实例
  x = w.baz;

  // 这两个闭包都引用了相同对象，所以相等
  assert(y.baz == x);

  // 这两个闭包引用了不同的对象，所以不等
  assert(v.baz != w.baz);
}
{% endprettify %}


### 返回值
<!-- ### Return values -->

所有函数都有返回值。如果没有定义，`return null;`代码将会被添加到代码的最后。
<!-- All functions return a value. If no return value is specified, the
statement `return null;` is implicitly appended to the function body. -->

<?code-excerpt "misc/test/language_tour/functions_test.dart (implicit-return-null)"?>
{% prettify dart %}
foo() {}

assert(foo() == null);
{% endprettify %}

## 运算符
<!-- ## Operators -->

Dart定义了如下表的运算符。您可以重写覆盖其中很多的运算符，参考文章[Overridable operators](#overridable-operators)。
<!-- Dart defines the operators shown in the following table.
You can override many of these operators, as described in
[Overridable operators](#overridable-operators). -->

|--------------------------+------------------------------------------------|
|描述                       | 运算符                                          |
|--------------------------|------------------------------------------------|
| 一元后置运算               | <code><em>expr</em>++</code>    <code><em>expr</em>--</code>    `()`    `[]`    `.`    `?.` |
| 一元前置运算               | <code>-<em>expr</em></code>    <code>!<em>expr</em></code>    <code>~<em>expr</em></code>    <code>++<em>expr</em></code>    <code>--<em>expr</em></code>   |
| 倍数关系                   | `*`    `/`    `%`    `~/`                      |
| 增减                      | `+`    `-`                                     |
| 位移                      | `<<`    `>>`                                   |
| 比特与(AND)                | `&`                                            |
| 比特异或(XOR)              | `^`                                            |
| 比特或(OR)                 | `|`                                            |
| 关系和类型                 | `>=`    `>`    `<=`    `<`    `as`    `is`    `is!` |
| 相等                       | `==`    `!=`                                   |
| 逻辑与(AND)                | `&&`                                           |
| 逻辑或(OR)                 | `||`                                           |
| 如果null                  | `??`                                           |
| 条件                      | <code><em>expr1</em> ? <em>expr2</em> : <em>expr3</em></code> |
| 联级                      | `..`                                           |
| 赋值                       | `=`    `*=`    `/=`    `~/=`    `%=`    `+=`    `-=`    `<<=`    `>>=`    `&=`    `^=`    `|=`    `??=` |
{:.table .table-striped}

当你使用运算符时，你也是在创建表达式。如下是一些运算表达式的例子：
<!-- When you use operators, you create expressions. Here are some examples
of operator expressions: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (expressions)" replace="/,//g"?>
{% prettify dart %}
a++
a + b
a = b
a == b
c ? a : b
a is T
{% endprettify %}

在[运算符表格operator table](#operators)中,每行的运算符都比在它下面的运算符要有更高的优先级。比如说，倍数运算符`%`比相等运算符`==`有更高的优先级，这意味着前者比后者先执行。而`==`比逻辑与（AND）运算符`&&`也有更高的优先级。优先级意味着下面的两个例子会以相同的方式执行：
<!-- In the [operator table](#operators),
each operator has higher precedence than the operators in the rows
that follow it. For example, the multiplicative operator `%` has higher
precedence than (and thus executes before) the equality operator `==`,
which has higher precedence than the logical AND operator `&&`. That
precedence means that the following two lines of code execute the same
way: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (precedence)"?>
{% prettify dart %}
// 括号增加了可读性
if ((n % i == 0) && (d % i == 0)) ...

// 难理解，但是是一样的效果
if (n % i == 0 && d % i == 0) ...
{% endprettify %}

<div class="alert alert-warning" markdown="1">
**警告：**那些作用于两个运算值的运算符，左边的运算值决定了那种版本的运算符被使用。比如，如果你有一个向量(Vector)对象和一个点(Point)对象， `aVector + aPoint` 会使用Vector版本的+运算。
<!-- **Warning:**
For operators that work on two operands, the leftmost operand
determines which version of the operator is used. For example, if you
have a Vector object and a Point object, `aVector + aPoint` uses the
Vector version of +. -->
</div>

### 数学运算符
<!-- ### Arithmetic operators -->

Dart支持了一些常见的数学运算符，如下表所示。
<!-- Dart supports the usual arithmetic operators, as shown in the following table. -->

|-----------------------------+-------------------------------------------|
| Operator                    | Meaning                                   |
|-----------------------------+-------------------------------------------|
| `+`                         | 加
| `–`                         | 减
| <code>-<em>expr</em></code> | 一元减, 也被称为负运算 (改变表达式的正负符号)
| `*`                         | 乘
| `/`                         | 除
| `~/`                        | 除，返回整型结果
| `%`                         | 获取整除的余数 (模运算)
{:.table .table-striped}

例子：
<!-- Example: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (arithmetic)"?>
{% prettify dart %}
assert(2 + 3 == 5);
assert(2 - 3 == -1);
assert(2 * 3 == 6);
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
assert(5 % 2 == 1); // Remainder

assert('5/2 = ${5~/2} r ${5%2}' == '5/2 = 2 r 1');
{% endprettify %}

dart也支持前缀和后缀增减运算。
<!-- Dart also supports both prefix and postfix increment and decrement
operators. -->

|-----------------------------+-------------------------------------------|
| Operator                    | Meaning                                   |
|-----------------------------+-------------------------------------------|
| <code>++<em>var</em></code> | <code><em>var</em> = <em>var</em> + 1</code> (表达式值是 <code><em>var</em> + 1</code>)
| <code><em>var</em>++</code> | <code><em>var</em> = <em>var</em> + 1</code> (表达式值是 <code><em>var</em></code>)
| <code>--<em>var</em></code> | <code><em>var</em> = <em>var</em> – 1</code> (表达式值是 <code><em>var</em> – 1</code>)
| <code><em>var</em>--</code> | <code><em>var</em> = <em>var</em> – 1</code> (表达式值是 <code><em>var</em></code>)
{:.table .table-striped}

例子：
<!-- Example: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (increment-decrement)"?>
{% prettify dart %}
var a, b;

a = 0;
b = ++a; // 在b获取a的值之前给a + 1
assert(a == b); // 1 == 1

a = 0;
b = a++; // 在b获取a的值之后给a + 1
assert(a != b); // 1 != 0

a = 0;
b = --a; // 在b获取a的值之前给a = 1
assert(a == b); // -1 == -1

a = 0;
b = a--; // 在b获取a的值之后给a = 1
assert(a != b); // -1 != 0
{% endprettify %}


### 相等和关系运算符
<!-- ### Equality and relational operators -->

The following table lists the meanings of equality and relational operators.

|-----------+-------------------------------------------|
| Operator  | Meaning                                   |
|-----------+-------------------------------------------|
| `==`      |       Equal; see discussion below
| `!=`      |       Not equal
| `>`       |       Greater than
| `<`       |       Less than
| `>=`      |       Greater than or equal to
| `<=`      |       Less than or equal to
{:.table .table-striped}

如果要测试两个对象x和y是否表示了相同的东西，使用`==`运算符。（在少数的情况下如果想知道两个对象是否是同一个对象，使用[identical()][]函数）。`==`是这样工作的：
<!-- To test whether two objects x and y represent the same thing, use the
`==` operator. (In the rare case where you need to know whether two
objects are the exact same object, use the [identical()][]
function instead.) Here’s how the `==` operator works: -->

1.  如果x或者y是null，只在两个都是null的情况下返回true；如果只有一个是null，返回false。
<!-- 1.  If *x* or *y* is null, return true if both are null, and false if only
    one is null. -->

2.  返回调用`*x*.==(*y*)`方法的结果。（没错，
    像`==`这样的运算符其实就是对第一个对象调用的方法。
    您甚至可以重写很多运算符，包括`==`，就像你在 [Overridable operators](#overridable-operators)看到的。）
<!-- 2.  Return the result of the method invocation
    <code><em>x</em>.==(<em>y</em>)</code>. (That’s right,
    operators such as `==` are methods that are invoked on their first
    operand. You can even override many operators, including `==`, as
    you’ll see in
    [Overridable operators](#overridable-operators).) -->

如下是各个使用相等和关系运算符的例子：
<!-- Here’s an example of using each of the equality and relational
operators: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (relational)"?>
{% prettify dart %}
assert(2 == 2);
assert(2 != 3);
assert(3 > 2);
assert(2 < 3);
assert(3 >= 3);
assert(2 <= 3);
{% endprettify %}


### 类型测试运算符
<!-- ### Type test operators -->

`as`, `is`, 和 `is!` 是在运行时检查类型的实用方法。
<!-- The `as`, `is`, and `is!` operators are handy for checking types at
runtime. -->

|-----------+-------------------------------------------|
| Operator  | Meaning                                   |
|-----------+-------------------------------------------|
| `as`      | Typecast（类型转换）
| `is`      | 如果对象是指定类型返回True
| `is!`     | 如果对象是指定类型返回False
{:.table .table-striped}

如果`obj`实现了`T`接口，那么`obj is T`的值为True。比如来说，`obj is Object`的值总是True。
<!-- The result of `obj is T` is true if `obj` implements the interface
specified by `T`. For example, `obj is Object` is always true. -->

使用`as`操作符来将一个对象变为制定的类型。通常情况下，您可以把这种写法当成先用`is`测试对象和使用对象的简写。举个例子，考虑下面的代码：
<!-- Use the `as` operator to cast an object to a particular type. In
general, you should use it as a shorthand for an `is` test on an object
following by an expression using that object. For example, consider the
following code: -->

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (emp is Person)"?>
{% prettify dart %}
if (emp is Person) {
  // Type check
  emp.firstName = 'Bob';
}
{% endprettify %}

你可以是使用`as`操作符来使代码更短：
<!-- You can make the code shorter using the `as` operator: -->

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (emp as Person)"?>
{% prettify dart %}
(emp as Person).firstName = 'Bob';
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**这里的代码的效果是不相同的。如果`emp`是null或者不是Person类型，那么第一个使用`is`例子什么都不会做；而第二个使用`as`的例子会抛出一个异常。
<!-- **Note:**
The code isn’t equivalent. If `emp` is null or not a Person, the
first example (with `is`) does nothing; the second (with `as`) throws
an exception. -->
</div>


### Assignment operators
### 赋值运算符

如您之前所见，您可以使用`=`运算符来赋值。如果希望只赋值给null变量，使用`??=`。
<!-- As you’ve already seen, you can assign values using the `=` operator.
To assign only if the assigned-to variable is null,
use the `??=` operator. -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (assignment)"?>
{% prettify dart %}
// 赋值value给a
a = value;
// 当b是null时赋值value给b；不然的话，b不变
b ??= value;
{% endprettify %}

{% comment %}
<!-- embed a dartpad when we can hide code -->
https://gist.github.com/9de887c4daf76d39e524
https://dartpad.dartlang.org/9de887c4daf76d39e524

<?code-excerpt "misc/test/language_tour/operators_test.dart (assignment-gist-main-body)"?>
{% prettify dart %}
void assignValues(int a, int b, int value) {
  print('Initially: a == $a, b == $b');
  // Assign value to a
  a = value;
  // Assign value to b if b is null; otherwise, b stays the same
  b ??= value;
  print('After: a == $a, b == $b');
}

main() {
  assignValues(0, 0, 1);
  assignValues(null, null, 1);
}
{% endprettify %}
{% endcomment %}

复合赋值运算符，比如像`+=`结合了运算和赋值。
<!-- Compound assignment operators such as `+=` combine
an operation with an assignment. -->

| `=`  | `–=` | `/=`  | `%=`  | `>>=` | `^=`
| `+=` | `*=` | `~/=` | `<<=` | `&=`  | `|=`
{:.table}

如下是复合赋值运算符工作的方法：
<!-- Here’s how compound assignment operators work: -->

|-----------+----------------------+-----------------------|
|           | 复合赋值               | 等价的表达式 |
|-----------+----------------------+-----------------------|
|**For an operator <em>op</em>:** | <code>a <em>op</em>= b</code> | <code>a = a <em>op</em> b</code>
|**Example:**                     |`a += b`                       | `a = a + b`
{:.table}

如下的例子说明了如何使用赋值运算符和复合赋值运算符：
<!-- The following example uses assignment and compound assignment
operators: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (op-assign)"?>
{% prettify dart %}
var a = 2; // 使用 = 赋值
a *= 3; // 赋值并相乘: a = a * 3
assert(a == 6);
{% endprettify %}


### 逻辑运算符
<!-- ### Logical operators -->

您可以通过使用逻辑运算符来反转或者合并布尔表达式。
<!-- You can invert or combine boolean expressions using the logical
operators. -->


|-----------------------------+-------------------------------------------|
| Operator                    | Meaning                                   |
|-----------------------------+-------------------------------------------|
| <code>!<em>expr</em></code> | 反转表达式（把false变为true，以及相反）
| `||`                        | 逻辑或（logical OR）
| `&&`                        | 逻辑与（logical AND）
{:.table .table-striped}

如下是使用逻辑运算符的例子：
<!-- Here’s an example of using the logical operators: -->

<?code-excerpt "misc/lib/language_tour/operators.dart (op-logical)"?>
{% prettify dart %}
if (!done && (col == 0 || col == 3)) {
  // ...做点什么...
}
{% endprettify %}


### 比特和位移运算符
<!-- ### Bitwise and shift operators -->

您可以在Dart中操作数字里的单个比特。通常情况下，你只会对整数类型使用比特和位移操作。
<!-- You can manipulate the individual bits of numbers in Dart. Usually,
you’d use these bitwise and shift operators with integers. -->

|-----------------------------+-------------------------------------------|
| 运算符                       | 意义                                   |
|-----------------------------+-------------------------------------------|
| `&`                         | AND
| `|`                         | OR
| `^`                         | XOR
| <code>~<em>expr</em></code> | 一元逐位反转 (0s 变为 1s; 1s 变为 0s)
| `<<`                        | 左移
| `>>`                        | 右移
{:.table .table-striped}

下面的例子说明了如何使用比特运算和位运算。
<!-- Here’s an example of using bitwise and shift operators: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (op-bitwise)"?>
{% prettify dart %}
final value = 0x22;
final bitmask = 0x0f;

assert((value & bitmask) == 0x02); // AND
assert((value & ~bitmask) == 0x20); // AND NOT
assert((value | bitmask) == 0x2f); // OR
assert((value ^ bitmask) == 0x2d); // XOR
assert((value << 4) == 0x220); // 左移
assert((value >> 4) == 0x02); // 右移
{% endprettify %}


### 条件表达式
<!-- ### Conditional expressions -->

Dart有两种可以让您不需要 [if-else](https://www.dartlang.org/guides/language/language-tour#if-and-else)就能精确地进行条件选择的运算。
<!-- Dart has two operators that let you concisely evaluate expressions
that might otherwise require [if-else](#if-and-else) statements: -->

<code><em>condition</em> ? <em>expr1</em> : <em>expr2</em>
: 如果*condition*是true，那么处理*expr1*（返回它的值）；不然的话，处理并返回*expr2*的值。
<!-- : If _condition_ is true, evaluates _expr1_ (and returns its value);
  otherwise, evaluates and returns the value of _expr2_. -->

<code><em>expr1</em> ?? <em>expr2</em></code>
: 如果*expr1*是非null值，返回它；不然的话，处理并返回*expr2*的值。
<!-- If _expr1_ is non-null, returns its value;
  otherwise, evaluates and returns the value of _expr2_. -->

如果您想根据一个布尔值给一个变量赋值，考虑使用`?:`。
<!-- When you need to assign a value
based on a boolean expression,
consider using `?:`. -->

<?code-excerpt "misc/lib/language_tour/operators.dart (if-then-else-operator)"?>
{% prettify dart %}
var visibility = isPublic ? 'public' : 'private';
{% endprettify %}

如果想测试一个布尔表达式是否为null，考虑使用`??`。
<!-- If the boolean expression tests for null,
consider using `??`. -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (if-null)"?>
{% prettify dart %}
String playerName(String name) => name ?? 'Guest';
{% endprettify %}

之前的例子可以至少有两种其他的写法，但它们不会很简洁：
<!-- The previous example could have been written at least two other ways,
but not as succinctly: -->

<?code-excerpt "misc/test/language_tour/operators_test.dart (if-null-alt)"?>
{% prettify dart %}
// 使用 ?: 运算符的较长版本.
String playerName(String name) => name != null ? name : 'Guest';

// 使用if-else 声明的较长版本.
String playerName(String name) {
  if (name != null) {
    return name;
  } else {
    return 'Guest';
  }
}
{% endprettify %}

<a id="cascade"></a>

### 联级表达（..）
<!-- ### Cascade notation (..) -->

联级（`..`）允许您对同一个对象进行一系列的操作。除了调用函数，您还可以获取相同对象中的属性。通过使用联级，您就不需要创建临时变量，并写出更顺畅的代码。
<!-- Cascades (`..`) allow you to make a sequence of operations
on the same object. In addition to function calls,
you can also access fields on that same object.
This often saves you the step of creating a temporary variable and
allows you to write more fluid code. -->

考虑如下代码：
<!-- Consider the following code: -->

<?code-excerpt "misc/test/language_tour/browser_test.dart (cascade-operator)"?>
{% prettify dart %}
querySelector('#confirm') // 获取一个对象.
  ..text = 'Confirm' // 使用他的成员
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
{% endprettify %}

第一个函数调用，`querySelector()`，返回了一个选择对象。这个代码后面使用了联级来对这个选择对象操作，它可以忽略任何表达式的返回值。
<!-- The first method call, `querySelector()`, returns a selector object.
The code that follows the cascade notation operates
on this selector object, ignoring any subsequent values that
might be returned. -->

上面的例子和如下的代码等价：
<!-- The previous example is equivalent to: -->

<?code-excerpt "misc/test/language_tour/browser_test.dart (cascade-operator-example-expanded)"?>
{% prettify dart %}
var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
{% endprettify %}

您也可以嵌套您的联级操作。如下：
<!-- You can also nest your cascades. For example: -->

<?code-excerpt "misc/lib/language_tour/operators.dart (nested-cascades)"?>
{% prettify dart %}
final addressBook = (new AddressBookBuilder()
      ..name = 'jenny'
      ..email = 'jenny@example.com'
      ..phone = (new PhoneNumberBuilder()
            ..number = '415-555-0100'
            ..label = 'home')
          .build())
    .build();
{% endprettify %}

构造您的联级表达式的时候要小心函数是否返回了一个对象。举例来说，下面的代码会报错：
<!-- Be careful to construct your cascade on a function that returns
an actual object. For example, the following code fails: -->

<?code-excerpt "misc/lib/language_tour/operators.dart (cannot-cascade-on-void)"?>
{% prettify dart %}
var sb = new StringBuffer();
sb.write('foo')
  ..write('bar'); // Error: 'void'没有定义'write'方法.
{% endprettify %}

`sb.write()` 函数调用返回void，但是您不能对`void`使用联级。
<!-- The `sb.write()` call returns void,
and you can't construct a cascade on `void`. -->

<div class="alert alert-info" markdown="1">
**注意：**严格意义上来说，这个用来联级“两点”符号并不是运算符。它只是Dart语法的一部分。
<!-- **Note:**
Strictly speaking,
the "double dot" notation for cascades is not an operator.
It's just part of the Dart syntax. -->
</div>

### 其他运算符
<!-- ### Other operators -->

您应该已经在其他例子中看过了剩下的大部分运算符：
<!-- You've seen most of the remaining operators in other examples: -->

|----------+-------------------------------------------|
| 运算符    | 名称                 |          意义   |
|-----------+------------------------------------------|
| `()`     | 方法应用          | 表示了一个函数调用 
| `[]`     | 列表取值          | 引用了列表中指定位数的值
| `.`      | 成员获取          | 引用了表达式的一个属性；举例来说：`foo.bar`从`foo`表达式中选取了属性`bar`
| `?.`     | 条件性成员获取     | 和`.`相似，但是最左边的运算符可以是null；举例：`foo?.bar`会从表达式`foo`中选取`bar`，但如果`foo`是null，那么`foo?.bar`也是null。
{:.table .table-striped}

关于`.`、 `?.`和 `..` 运算符更多的信息，查看[Classes](#classes)。
<!-- For more information about the `.`, `?.`, and `..` operators, see
[Classes](#classes). -->


## 流程控制
<!-- ## Control flow statements -->

您可以使用下列的写法来控制Dart语言的运行流程
<!-- You can control the flow of your Dart code using any of the following: -->

-   `if` and `else`

-   `for` loops

-   `while` and `do`-`while` loops

-   `break` and `continue`

-   `switch` and `case`

-   `assert`

您也可以使用`try-catch`和`throw`来影响控制流程，详情请查看[异常Exceptions](#exceptions)。
<!-- You can also affect the control flow using `try-catch` and `throw`, as
explained in [Exceptions](#exceptions). -->


### If 和 else
<!-- ### If and else -->

如下例所示，Dart支持了`if` 语句和可选的`else`语句。具体可查看[条件表达式conditional-expressions](#conditional-expressions)
<!-- Dart supports `if` statements with optional `else` statements, as the
next sample shows. Also see [conditional expressions](#conditional-expressions). -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (if-else)"?>
{% prettify dart %}
if (isRaining()) {
  you.bringRainCoat();
} else if (isSnowing()) {
  you.wearJacket();
} else {
  car.putTopDown();
}
{% endprettify %}

和JavaScript不同，条件语句必须使用boolean类型的值，其他的都不行。具体请查看[Booleans](#booleans)。
<!-- Unlike JavaScript, conditions must use boolean values, nothing else. See
[Booleans](#booleans) for more information. -->


### for 循环
<!-- ### For loops -->

您可以使用常见的`for`语句来进行遍历。如下所示：
<!-- You can iterate with the standard `for` loop. For example: -->

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (for)"?>
{% prettify dart %}
var message = new StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
{% endprettify %}

在Dart`for`语句中的闭包是能够提取到_变量_的序号（index）的，这避免了javas中常见的一个纰漏。如下所示，考虑代码：
<!-- Closures inside of Dart’s `for` loops capture the _value_ of the index,
avoiding a common pitfall found in JavaScript. For example, consider: -->

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (for-and-closures)"?>
{% prettify dart %}
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}
callbacks.forEach((c) => c());
{% endprettify %}

它的输出代码首先是`0`，紧跟着`1`。与之相对的是在JavaScript中，两次的输出都是是`2`。
<!-- The output is `0` and then `1`, as expected. In contrast, the example
would print `2` and then `2` in JavaScript. -->

如果您遍历的对象是可遍历对象，那么您就可以使用[forEach()][]方法。如果您不需要当前遍历的序号和计数器，那使用`forEach()`是一个很好的选择：
<!-- If the object that you are iterating over is an Iterable, you can use the
[forEach()][] method. Using `forEach()` is a good option if you don’t need to
know the current iteration counter: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (forEach)"?>
{% prettify dart %}
candidates.forEach((candidate) => candidate.interview());
{% endprettify %}

可遍历(*Iterable*)类，比如像List和Set同样也支持了`for-in`的[遍历iteration](/guides/libraries/library-tour#iteration)表达式。
<!-- Iterable classes such as List and Set also support the `for-in` form of
[iteration](/guides/libraries/library-tour#iteration): -->

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (collection)"?>
{% prettify dart %}
var collection = [0, 1, 2];
for (var x in collection) {
  print(x); // 0 1 2
}
{% endprettify %}


### While 和 do-while
<!-- ### While and do-while -->

一个`while`循环会在每轮循环前查看条件(*condition*)：
<!-- A `while` loop evaluates the condition before the loop: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (while)"?>
{% prettify dart %}
while (!isDone()) {
  doSomething();
}
{% endprettify %}

一个`do`-`while`循环会在每次循环后查看条件：
<!-- A `do`-`while` loop evaluates the condition *after* the loop: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (do-while)"?>
{% prettify dart %}
do {
  printLine();
} while (!atEndOfPage());
{% endprettify %}


### Break 和 continue
<!-- ### Break and continue -->

使用`break`来终止循环：
<!-- Use `break` to stop looping: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (while-break)"?>
{% prettify dart %}
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
{% endprettify %}

使用`continue`来跳过当前循环，直接执行下一个循环：
<!-- Use `continue` to skip to the next loop iteration: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (for-continue)"?>
{% prettify dart %}
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}
{% endprettify %}

如果您遍历的对象是一个[可遍历Iterable][]对象，比如list或者set，那么还有另一种方式完成上面的代码：
<!-- You might write that example differently if you’re using an
[Iterable][] such as a list or set: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (where)"?>
{% prettify dart %}
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
{% endprettify %}


### Switch 和 case
<!-- ### Switch and case -->

Dart中的Switch声明会使用`==`比较整数、字符串和编译时常量。被比较的对象必须是相同类的实例（不可以是子类型），而且这个类不可以覆盖（*override*）原有的`==`运算符。
<!-- Switch statements in Dart compare integer, string, or compile-time
constants using `==`. The compared objects must all be instances of the
same class (and not of any of its subtypes), and the class must not
override `==`. -->
[枚举类型Enumerated types](#enumerated-types)与`switch`语句是绝配。
<!-- [Enumerated types](#enumerated-types) work well in `switch` statements. -->

<div class="alert alert-info" markdown="1">
**注意：**
Dart里的Switch语句是被设计用来处理有限的情况的，比如在解释器和扫描器。
<!-- **Note:**
Switch statements in Dart are intended for limited circumstances,
such as in interpreters or scanners. -->
</div>

根据规定，每一个非空`case`条件执行都是要以`break`语句结尾的。
其他用来结束一个非空`case`条件执行的方式有`continue`、`throw`或者`return`语句。
<!-- Each non-empty `case` clause ends with a `break` statement, as a rule.
Other valid ways to end a non-empty `case` clause are a `continue`,
`throw`, or `return` statement. -->

使用`default`来处理没有`case`匹配的条件的执行的情况：
<!-- Use a `default` clause to execute code when no `case` clause matches: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch)"?>
{% prettify dart %}
var command = 'OPEN';
switch (command) {
  case 'CLOSED':
    executeClosed();
    break;
  case 'PENDING':
    executePending();
    break;
  case 'APPROVED':
    executeApproved();
    break;
  case 'DENIED':
    executeDenied();
    break;
  case 'OPEN':
    executeOpen();
    break;
  default:
    executeUnknown();
}
{% endprettify %}

下面的代码忽略了`case`条件执行中的`break`语句，因此产生了报错：
<!-- The following example omits the `break` statement in a `case` clause,
thus generating an error: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch-break-omitted)"?>
{% prettify dart %}
var command = 'OPEN';
switch (command) {
  case 'OPEN':
    executeOpen();
    // ERROR: Missing break

  case 'CLOSED':
    executeClosed();
    break;
}
{% endprettify %}

话说回来，Dart还是支持了留空`case`条件执行的方式来运允许通过执行（fall-through）的形式：
<!-- However, Dart does support empty `case` clauses, allowing a form of
fall-through: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch-empty-case)"?>
{% prettify dart %}
var command = 'CLOSED';
switch (command) {
  case 'CLOSED': // Empty case falls through.空case执行下面的case
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    // 不论CLOSED还是NOW_CLOSED，都会执行。
    executeNowClosed();
    break;
}
{% endprettify %}


如果您想在非空的条件下进行通过执行(fall-through)，可以使用`continue`语句和一个符号（*label*）：
<!-- If you really want fall-through, you can use a `continue` statement and
a label: -->

<?code-excerpt "misc/lib/language_tour/control_flow.dart (switch-continue)"?>
{% prettify dart %}
var command = 'CLOSED';
switch (command) {
  case 'CLOSED':
    executeClosed();
    continue nowClosed;
  // Continues executing at the nowClosed label.
  // 在nowClosed符号处继续执行。
  nowClosed:
  case 'NOW_CLOSED':
    // Runs for both CLOSED and NOW_CLOSED.
    // CLOSED和NOW_CLOSED条件下都会执行。
    executeNowClosed();
    break;
}
{% endprettify %}

`case`的条件执行中可以有自己的本地变量，只有在大括号的作用域中可以获取。
A `case` clause can have local variables, which are visible only inside
the scope of that clause.


### Assert

使用`assert`语句来通过一个false的条件来扰乱程序的运行。您会常常在这篇文章中见到这个的例子。这里再给出一些：
<!-- Use an `assert` statement to disrupt normal execution if a boolean
condition is false. You can find examples of assert statements
throughout this tour. Here are some more: -->

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (assert)"?>
{% prettify dart %}
// Make sure the variable has a non-null value.
// 确保变量值不为null。
assert(text != null);

// Make sure the value is less than 100.
// 确保值小于100。
assert(number < 100);

// Make sure this is an https URL.
// 确保字符串是https的URL。
assert(urlString.startsWith('https'));
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**
Addert语句不会在生产模式（production）的代码中生效；
它们只为开发服务。
Flutter框架在[debug模式debug mode][flutter debug mode]中开启了assert。
开发用工具，比如[dartdevc][]默认支持asserts。
想在其他的一些工具中使用，比如[dart][]和[dart2js,][dart2js]需要在命令行中加入`--enable-asserts`flag。
<!-- **Note:**
Assert statements have no effect in production code;
they're for development only.
Flutter enables asserts in [debug mode.][flutter debug mode]
Development-only tools such as [dartdevc][]
typically support asserts by default.
Some tools, such as [dart][] and [dart2js,][dart2js]
support asserts through a command-line flag: `--enable-asserts`. -->
</div>

如果想给assert添加一个信息，在第二个参数中传入一个字符串。
<!-- To attach a message to an assert,
add a string as the second argument. -->

<?code-excerpt "misc/test/language_tour/control_flow_test.dart (assert-with-message)"?>
{% prettify dart %}
assert(urlString.startsWith('https'),
    'URL ($urlString) should start with "https".');
{% endprettify %}

`assert`语句的第一个参数可以是任何解析为布尔值的表达式。如果表达式为true，assertion会跳过，
程序会继续执行。如果是false，assertion会失败，一个异常([AssertionError][])会被抛出。
<!-- The first argument to `assert` can be any expression that
resolves to a boolean value. If the expression’s value
is true, the assertion succeeds and execution
continues. If it's false, the assertion fails and an exception (an
[AssertionError][]) is thrown. -->


## 异常
<!-- ## Exceptions -->

您的Dart代码可以抛出（*throw*）和抓住（*catch*）异常。异常是那些表明我们不希望发生的事情发生了的错误。如果
异常没有被catch，抛出错误的dart独立进程对象（[isolate](https://api.dartlang.org/stable/1.24.3/dart-isolate/Isolate-class.html)）会终止，
通常情况下，dart独立进程对象和他的程序会终止。
<!-- Your Dart code can throw and catch exceptions. Exceptions are errors
indicating that something unexpected happened. If the exception isn’t
caught, the isolate that raised the exception is suspended, and
typically the isolate and its program are terminated. -->

和Java相比，所以的Dart异常是unchecked exceptions。方法不需要声明它们可能
抛出的异常，而且您不一定要catch这些异常。
<!-- In contrast to Java, all of Dart’s exceptions are unchecked exceptions.
Methods do not declare which exceptions they might throw, and you are
not required to catch any exceptions. -->

Dart提供了[Exception][]和[Error][]类型，以及很多其他预定义好的子类型。当然，
您也可以定义您自己的异常。不过，Dart程序也可以抛出任何非空（non-null）对象作为
异常，而不仅仅是异常（*Exception*）和错误（*Error*）。
<!-- Dart provides [Exception][] and [Error][]
types, as well as numerous predefined subtypes. You can, of course,
define your own exceptions. However, Dart programs can throw any
non-null object—not just Exception and Error objects—as an exception. -->

### 抛出
<!-- ### Throw -->

如下是一个抛出异常的例子，也可以称为提出（*raising*）一个异常：
<!-- Here’s an example of throwing, or *raising*, an exception: -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (throw-FormatException)"?>
{% prettify dart %}
throw new FormatException('Expected at least 1 section');
{% endprettify %}

您也可以抛出任意的对象：
<!-- You can also throw arbitrary objects: -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (out-of-llamas)"?>
{% prettify dart %}
throw 'Out of llamas!';
{% endprettify %}

<div class="alert alert-info" markdown="1">
  **注意：**生产级的代码通常会抛出实现（*implement*）[Error][] 或者 [Exception][]
  接口的错误。
  <!-- **Note:** Production-quality code usually throws types that implement
  [Error][] or [Exception][]. -->
</div>

因为抛出对象是一个表达式，所以您也可以在箭头函数（=\>），以及任何允许表达式的地方抛出异常：
<!-- Because throwing an exception is an expression, you can throw exceptions
in =\> statements, as well as anywhere else that allows expressions: -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (throw-is-an-expression)"?>
{% prettify dart %}
void distanceTo(Point other) =>
    throw new UnimplementedError();
{% endprettify %}

### 捕获
<!-- ### Catch -->

捕获一个异常会停止会停止这个异常的传播（*propagating*），只要您不再抛出一个异常。
捕获异常可以使您有机会处理它：
<!-- Catching, or capturing, an exception stops the exception from
propagating (unless you rethrow the exception).
Catching an exception gives you a chance to handle it: -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try)"?>
{% prettify dart %}
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
{% endprettify %}

要处理抛出多个异常的代码，您可以简单地使用多个捕获大括号。第一个匹配到异常对象的捕获大括号语句
会处理异常。如果语句没有定义明确的类型，那个语句会处理任何异常对象：
<!-- To handle code that can throw more than one type of exception, you can
specify multiple catch clauses. The first catch clause that matches the
thrown object’s type handles the exception. If the catch clause does not
specify a type, that clause can handle any type of thrown object: -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try-catch)"?>
{% prettify dart %}
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  // 一个特殊异常
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  // 任何异常的东西
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  // 没有明确的类型，处理任何其他的情况
  print('Something really unknown: $e');
}
{% endprettify %}

就像之前的代码所显示的那样，您可以使用`on`或者`catch`，也可以一起用。
如果是指定的异常类型，使用`on`。如果您的异常处理需要异常对象，则使用`catch`。
<!-- As the preceding code shows, you can use either `on` or `catch` or both.
Use `on` when you need to specify the exception type. Use `catch` when
your exception handler needs the exception object. -->

您可以给`catch()`定义一个或者两个参数。第一个是被抛出的异常，
第二个是一个栈追踪（[StackTrace][]）对象。
<!-- You can specify one or two parameters to `catch()`.
The first is the exception that was thrown,
and the second is the stack trace (a [StackTrace][] object). -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try-catch-2)" replace="/\(e.*?\)/[!$&!]/g"?>
{% prettify dart %}
try {
  // ···
} on Exception catch [!(e)!] {
  print('Exception details:\n $e');
} catch [!(e, s)!] {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
{% endprettify %}

如果想部分地处理异常，并想让它继续传播，使用`rethrow`关键词。
<!-- To partially handle an exception,
while allowing it to propagate,
use the `rethrow` keyword. -->

<?code-excerpt "misc/test/language_tour/exceptions_test.dart (rethrow)" replace="/rethrow;/[!$&!]/g"?>
{% prettify dart %}
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error 运行时错误
  } catch (e) {
    print('misbehave() 部分的异常处理 ${e.runtimeType}.');
    [!rethrow;!] // Allow callers to see the exception.
                 // 使调用函数看见异常
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() 最终的异常处理 ${e.runtimeType}.');
  }
}
{% endprettify %}


### Finally

如果想保证一些代码在任何情况下执行，不论是抛出了异常还是没有，使用`finally`大括号语句块。
如果没有`catch`匹配到异常，那么异常会在`finally`大括号语句块执行后急需传播。
<!-- To ensure that some code runs whether or not an exception is thrown, use
a `finally` clause. If no `catch` clause matches the exception, the
exception is propagated after the `finally` clause runs: -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (finally)"?>
{% prettify dart %}
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  // 不论是否有异常，总是清理
  cleanLlamaStalls();
}
{% endprettify %}

`finally`里的代码会在所有`catch`代码后执行：
<!-- The `finally` clause runs after any matching `catch` clauses: -->

<?code-excerpt "misc/lib/language_tour/exceptions.dart (try-catch-finally)"?>
{% prettify dart %}
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
                      // 先处理异常
} finally {
  cleanLlamaStalls(); // Then clean up.
                      // 再清理
}
{% endprettify %}

更多内容，查看[Exceptions](/guides/libraries/library-tour#exceptions)章节。
<!-- Learn more by reading the
[Exceptions](/guides/libraries/library-tour#exceptions) section. -->

## 类
<!-- ## Classes -->

Dart是一个支持类和混入继承的面向对象语言。每个对象都是类的实例，而且所有类都是[Object][Object]类的子类。
*混入继承（Mixin-based inheritance）*的意思是：尽管每个类（除了Object）都只有一个超类，一个类体
可以在多个类树中复用。
<!-- Dart is an object-oriented language with classes and mixin-based
inheritance. Every object is an instance of a class, and all classes
descend from [Object.][Object]
*Mixin-based inheritance* means that although every class (except for
Object) has exactly one superclass, a class body can be reused in
multiple class hierarchies. -->

要创建一个对象，您可以使用`new`关键词和一个所需类的*构造函数constructor*。构造函数constructor
的名称可以是<code><em>ClassName</em></code> 或者<code><em>ClassName</em>.<em>identifier</em></code>。举个例子：
<!-- To create an object, you can use the `new` keyword with a *constructor*
for a class. Constructor names can be either <code><em>ClassName</em></code> or
<code><em>ClassName</em>.<em>identifier</em></code>. For example: -->

<?code-excerpt "misc/test/language_tour/classes_test.dart (object-creation)" replace="/ as .*?;/;/g"?>
{% prettify dart %}
// 使用Point()来创建一个Point类的对象。
var p1 = new Point(2, 2);

// 使用Point.fromJson()来创建一个Point类的对象。
var p2 = new Point.fromJson({'x': 1, 'y': 2});
{% endprettify %}

<aside class="alert alert-info" markdown="1">
**Dart 2 注意点：**
您可以省去构造函数之前的`new`。
比如：`p1 = Point(2, 2)`。
<!-- **Dart 2 note:**
You can omit the `new` before the constructor.
Example: `p1 = Point(2, 2)`. -->

{% comment %}
update-for-dart-2

TODO: Once dart-lang/pub#1807 is fixed, remove the note and put
`p3 = Point(2, 2)` into the code snippet.
{% endcomment %}
</aside>

对象是有*成员members*的，这包括*函数-functions*和*数据-data*，也被称为
*方法-methods* 和*实例变量-instance variables*。当您调用一个方法，您是在
一个对象中激活了它：这个方法可以获取这个对象中的函数和数据。

<!-- Objects have *members* consisting of functions and data (*methods* and
*instance variables*, respectively). When you call a method, you *invoke*
it on an object: the method has access to that object’s functions and
data. -->

使用一个点（`.`）来引用一个实例变量或者方法：
<!-- Use a dot (`.`) to refer to an instance variable or method: -->

<?code-excerpt "misc/test/language_tour/classes_test.dart (object-members)"?>
{% prettify dart %}
var p = new Point(2, 2);

// 设置这个对象的实例变量y的值。
p.y = 3;

// 获取y的值
assert(p.y == 3);

// 激活p对象上的distanceTo()方法。
num distance = p.distanceTo(new Point(4, 4));
{% endprettify %}

当最左边的运算对象是null时，使用`.`会抛出一个异常。可以使用`?.`来避免：
<!-- Use `?.` instead of `.` to avoid an exception
when the leftmost operand is null: -->

{% comment %}
https://dartpad.dartlang.org/0cb25997742ed5382e4a
https://gist.github.com/0cb25997742ed5382e4a
{% endcomment %}

<?code-excerpt "misc/test/language_tour/classes_test.dart (safe-member-access)"?>
{% prettify dart %}
// 如果p不是null，设置它的y值为4。
p?.y = 4;
{% endprettify %}

有些类提供了常数构造函数，这种构造函数可以用来创建一个编译时常量。但需要使用`const`，
而不是`new`：
<!-- Some classes provide constant constructors. To create a compile-time
constant using a constant constructor, use `const` instead of `new`: -->

<?code-excerpt "misc/test/language_tour/classes_test.dart (const)"?>
{% prettify dart %}
var p = const ImmutablePoint(2, 2);
{% endprettify %}

<aside class="alert alert-info" markdown="1">
**Dart 2 注意点：**
您有时其实可以省略构造函数前的`const`，但不是在这个例子中。
更多的信息，阅读[informal specification for implicit creation.](https://github.com/dart-lang/sdk/blob/master/docs/language/informal/implicit-creation.md)
中有关 _constant context_ 的内容。
<!-- **Dart 2 note:**
You can sometimes omit the `const` before the constructor,
but not in this example.
For more information, read about _constant context_ in the
[informal specification for implicit creation.](https://github.com/dart-lang/sdk/blob/master/docs/language/informal/implicit-creation.md) -->
{% comment %}
update-for-dart-2

To omit the `const` before a constructor,
you need to be in a `const` context,
which requires at least one other use of `const`.
[EXAMPLE OR LINK GOES HERE]

[TODO: Once https://github.com/dart-lang/pub/issues/1807 is fixed,
update code snippet and tests.]
{% endcomment %}
</aside>

构造两个一样的编译时常量只会得到一个唯一的实例：
<!-- Constructing two identical compile-time constants results in a single,
canonical instance: -->

<?code-excerpt "misc/test/language_tour/classes_test.dart (identical)"?>
{% prettify dart %}
var a = const ImmutablePoint(1, 1);
var b = const ImmutablePoint(1, 1);

assert(identical(a, b)); // 它们是同一个实例！
{% endprettify %}

如果想再运行时得到一个对象的类型，
您可以使用*对象类-Object*的`runtimeType`属性，这个属性会返回一个[Type][]类型的对象。
<!-- To get an object's type at runtime,
you can use Object's `runtimeType` property,
which returns a [Type][] object. -->

<?code-excerpt "misc/test/language_tour/classes_test.dart (runtimeType)"?>
{% prettify dart %}
print('The type of a is ${a.runtimeType}');
{% endprettify %}

下面的章节会讨论如何实现类。
<!-- The following sections discuss how to implement classes. -->


### 实例变量
<!-- ### Instance variables -->

如下是您声明实例变量的例子：
<!-- Here’s how you declare instance variables: -->

<?code-excerpt "misc/lib/language_tour/classes/point_with_main.dart (class)"?>
{% prettify dart %}
class Point {
  num x; // 声明实例变量x，初始值是null。
  num y; // 声明y，初始值是null。
  num z = 0; // 声明z，初始值是0。
}
{% endprettify %}

所有没有初始化的实例变量的值都是`null`。
<!-- All uninitialized instance variables have the value `null`. -->

所有实例变量都会生成一个隐性的*getter*方法。非final实例变量还会生产一个隐性的*setter*方法，
具体的细节，查看[Getters and setters](#getters-and-setters)章节。
<!-- All instance variables generate an implicit *getter* method. Non-final
instance variables also generate an implicit *setter* method. For details,
see [Getters and setters](#getters-and-setters). -->

<?code-excerpt "misc/lib/language_tour/classes/point_with_main.dart (class+main)" replace="/(num .*?;).*/$1/g"?>
{% prettify dart %}
class Point {
  num x;
  num y;
}

void main() {
  var point = new Point();
  point.x = 4; // 使用了x的setter方法。
  assert(point.x == 4); // 使用了x的getter方法。
  assert(point.y == null); // 默认值为null
}
{% endprettify %}

如果您在声明一个实例变量时就初始化了它的值，而不是在构造函数或者方法里，这个值会在实例
创建的时候就被赋予给这个实例变量，也就是说在实例的构造函数和初始化列表执行之前。
<!-- If you initialize an instance variable where it is declared (instead of
in a constructor or method), the value is set when the instance is
created, which is before the constructor and its initializer list
execute. -->


### 构造函数
<!-- ### Constructors -->

可以通过创建一个和类名相同的函数来声明一个构造函数（这个构造函数可以附加一个额外的，可选的标识符，具体参考[命名构造函数-Named constructors](#named-constructors)）。
这是最常见构造形式，它可以创建一个类的实例：
<!-- Declare a constructor by creating a function with the same name as its
class (plus, optionally, an additional identifier as described in
[Named constructors](#named-constructors)).
The most common form of constructor, the generative constructor, creates
a new instance of a class: -->

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (constructor-long-way)"?>
{% prettify dart %}
class Point {
  num x, y;

  Point(num x, num y) {
    // 还有一个更好的方法，先别“换台”。
    this.x = x;
    this.y = y;
  }
}
{% endprettify %}

`this`关键词引用了当前实例。
<!-- The `this` keyword refers to the current instance. -->

<div class="alert alert-info" markdown="1">
**注意：**
只在会出现多个相同名称冲突的时候再使用`this`。不然的话，Dart格式会省略`this`。
<!-- **Note:**
Use `this` only when there is a name conflict. Otherwise, Dart style
omits the `this`. -->
</div>

因为通过传入实参来指派实例变量的模式太常见了，所有Dart提供了一个方便的语法糖：
<!-- The pattern of assigning a constructor argument to an instance variable
is so common, Dart has syntactic sugar to make it easy: -->

<?code-excerpt "misc/lib/language_tour/classes/point.dart (constructor-initializer)"?>
{% prettify dart %}
class Point {
  num x, y;

  // 在运行构造函数之前，这个语法糖会设置x和y的值
  Point(this.x, this.y);
}
{% endprettify %}

#### 默认构造函数
<!-- #### Default constructors -->

如果您没有声明一个构造函数，Dart会提供一个默认的构造函数给您。这个默认的构造函数不会接受
实参数，它还会触发父类的没有参数的构造函数。
If you don’t declare a constructor, a default constructor is provided
for you. The default constructor has no arguments and invokes the
no-argument constructor in the superclass.

#### 构造函数是不会继承的
<!-- #### Constructors aren’t inherited -->

父类不会基础它自己父类的构造函数。一个没有声明构造函数的子类只会有一个默认的，没有参数，
没有名称的构造函数。
<!-- Subclasses don’t inherit constructors from their superclass. A subclass
that declares no constructors has only the default (no argument, no
name) constructor. -->

#### 命名构造函数
<!-- #### Named constructors -->

使用命名构造函数功能来为一个类实现多个构造方式，也可以来增强程序的可读性。
<!-- Use a named constructor to implement multiple constructors for a class
or to provide extra clarity: -->

<?code-excerpt "misc/lib/language_tour/classes/point.dart (named-constructor)" replace="/Point\.\S*/[!$&!]/g"?>
{% prettify dart %}
class Point {
  num x, y;

  Point(this.x, this.y);

  // 命名构造函数
  [!Point.origin()!] {
    x = 0;
    y = 0;
  }
}
{% endprettify %}

记住构造函数是不会继承的，这意味着一个父类的命名构造函数是不会被子类继承的。如果您
希望用一个子类的父类所定义的命名构造函数创建一个实例，那么您必须在这个子类中实现这
个构造函数。
<!-- Remember that constructors are not inherited, which means that a
superclass’s named constructor is not inherited by a subclass. If you
want a subclass to be created with a named constructor defined in the
superclass, you must implement that constructor in the subclass. -->

#### 触发一个非默认父类的构造函数
<!-- #### Invoking a non-default superclass constructor -->

在默认的情况下，一个子类的构造函数会调用父类的非命名，无参数的构造函数。
这个父类的构造函数会在子类的的构造函数的函数逻辑之前被调用。如果一个
[初始化列表- initializer list](#initializer-list)也被使用了，那么这个
初始化列表会在父类的构造函数之前被调用。
总结一下，执行的顺序如下：
<!-- 
By default, a constructor in a subclass calls the superclass’s unnamed,
no-argument constructor.
The superclass's constructor is called at the beginning of the
constructor body. If an [initializer list](#initializer-list)
is also being used, it executes before the superclass is called.
In summary, the order of execution is as follows: -->

1. 初始化列表
1. 父类的无参构造函数
1. 当前类的无参构造函数
<!-- 1. initializer list
1. superclass's no-arg constructor
1. main class's no-arg constructor -->

如果一个父类没有一个未命名的，没有参数的构造函数，那么您必须手动地去调用这个父类中
的某一个构造函数。方法是在构造逻辑之前，在一个冒号（`:`）之后，定义需要的父类构造函数。
<!-- If the superclass doesn’t have an unnamed, no-argument constructor,
then you must manually call one of the constructors in the
superclass. Specify the superclass constructor after a colon (`:`), just
before the constructor body (if any). -->

如下的代码就是这样的一个例子，Employee类的构造函数调用了它父类，Person，的命名构造函数。
点击运行按钮 ( {% img 'red-run.png' %} ) 来执行代码。
<!-- In the following example, the constructor for the Employee class
calls the named constructor for its superclass, Person.
Click the run button ( {% img 'red-run.png' %} ) to execute the code. -->

{% comment %}
https://gist.github.com/Sfshaza/e57aa06401e6618d4eb8
https://dartpad.dartlang.org/e57aa06401e6618d4eb8

<?code-excerpt "misc/lib/language_tour/classes/employee.dart"?>
{% prettify dart %}
class Person {
  String firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

void main() {
  var emp = new Employee.fromJson({});
  // Prints:
  // in Person
  // in Employee

  if (emp is Person) {
    // Type check
    emp.firstName = 'Bob';
  }
  (emp as Person).firstName = 'Bob';
}
{% endprettify %}
{% endcomment %}

<iframe
src="{{site.custom.dartpad.embed-dart-prefix}}?id=e57aa06401e6618d4eb8&horizontalRatio=99&verticalRatio=80"
    width="100%"
    height="500px"
    style="border: 1px solid #ccc;">
</iframe>

因为传入父类构造函数的参数会在调用之前先求值，所以参数可以是一个表达式，比如函数调用：
<!-- Because the arguments to the superclass constructor are evaluated before
invoking the constructor, an argument can be an expression such as a
function call: -->

<?code-excerpt "misc/lib/language_tour/classes/employee.dart (method-then-constructor)"?>
{% prettify dart %}
class Employee extends Person {
  Employee() : super.fromJson(getDefaultData());
  // ···
}
{% endprettify %}

<div class="alert alert-warning" markdown="1">
**警告：**
传入父类构造函数的参数是没有获取`this`的能力的。举个例子，参数可以调用静态方法，但不能
调用实例方法。
<!-- **Warning:**
Arguments to the superclass constructor do not have access to `this`.
For example, arguments can call static methods but not instance methods. -->
</div>

#### 初始化列表 - Initializer list
<!-- #### Initializer list -->

除了调用一个父类的构造函数，你还可以在构造逻辑之前初始化实例变量。要有逗号来分割
这样的初始化操作。
<!-- Besides invoking a superclass constructor, you can also initialize
instance variables before the constructor body runs. Separate
initializers with commas. -->

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (initializer-list)"?>
{% prettify dart %}
// 使用初始化列表，在构造逻辑之前初始化实例变量
Point.fromJson(Map<String, num> json)
    : x = json['x'],
      y = json['y'] {
  print('In Point.fromJson(): ($x, $y)');
}
{% endprettify %}

<div class="alert alert-warning" markdown="1">
**警告：**
初始化操作的右边是没有获取`this`的能力的。
<!-- **Warning:**
The right-hand side of an initializer does not have access to `this`. -->
</div>

在开发时，您可以在初始化列表中使用`assert`来验证输入。
<!-- During development, you can validate inputs by using `assert` in the
initializer list. -->

<?code-excerpt "misc/lib/language_tour/classes/point_alt.dart (initializer-list-with-assert)" replace="/assert\(.*?\)/[!$&!]/g"?>
{% prettify dart %}
Point.withAssert(this.x, this.y) : [!assert(x >= 0)!] {
  print('In Point.withAssert(): ($x, $y)');
}
{% endprettify %}

{% comment %}
[PENDING: the example could be better.
Note that DartPad doesn't support this yet?

https://github.com/dart-lang/sdk/issues/30968
https://github.com/dart-lang/sdk/blob/master/docs/language/informal/assert-in-initializer-list.md]
{% endcomment %}

初始化列表是很合适的用来设置final变量的地方。
如下的例子在一个初始化列表中初始化了3个final变量。
点击运行按钮 ( {% img 'red-run.png' %} ) 来执行代码
<!-- Initializer lists are handy when setting up final fields.
The following example initializes three final fields in an initializer list.
Click the run button ( {% img 'red-run.png' %} ) to execute the code. -->

{% comment %}
https://gist.github.com/Sfshaza/7a9764702c0608711e08
https://dartpad.dartlang.org/7a9764702c0608711e08

<?code-excerpt "misc/lib/language_tour/classes/point_with_distance_field.dart"?>
{% prettify dart %}
import 'dart:math';

class Point {
  final num x;
  final num y;
  final num distanceFromOrigin;

  Point(num x, num y)
      : x = x,
        y = y,
        distanceFromOrigin = sqrt(x * x + y * y);
}

void main() {
  var p = new Point(2, 3);
  print(p.distanceFromOrigin);
}
{% endprettify %}
{% endcomment %}

<iframe
src="{{site.custom.dartpad.embed-dart-prefix}}?id=7a9764702c0608711e08&horizontalRatio=99&verticalRatio=85"
    width="100%"
    height="420px"
    style="border: 1px solid #ccc;">
</iframe>


#### 重定向构造函数
<!-- #### Redirecting constructors -->

有时候一个构造函数的唯一目的是重定向到同个类中的其他构造函数。这种构造函数的逻辑可以是
空的，只需要在冒号（:）后面调用希望的构造函数。
<!-- Sometimes a constructor’s only purpose is to redirect to another
constructor in the same class. A redirecting constructor’s body is
empty, with the constructor call appearing after a colon (:). -->

<?code-excerpt "misc/lib/language_tour/classes/point_redirecting.dart"?>
{% prettify dart %}
class Point {
  num x, y;

  // 当前类的主构造函数。
  Point(this.x, this.y);

  // 对主构造函数的代理。
  Point.alongXAxis(num x) : this(x, 0);
}
{% endprettify %}

#### 常量构造函数
<!-- #### Constant constructors -->

如果你的类产出的对象用于不会变，你可以使这些对象成为编译时常量。要做到这个，定义一个`const`构造函数，
并且确保所有的实例变量都是`final`。
<!-- If your class produces objects that never change, you can make these
objects compile-time constants. To do this, define a `const` constructor
and make sure that all instance variables are `final`. -->

<?code-excerpt "misc/lib/language_tour/classes/immutable_point.dart"?>
{% prettify dart %}
class ImmutablePoint {
  static final ImmutablePoint origin =
      const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
{% endprettify %}

#### 工厂构造函数
<!-- #### Factory constructors -->

使用`factory`关键词来实现一个不总是创建它的新实例的构造函数。比如说，一个工厂构造函数
也许会从缓存中取出一个实例，也可能返回一个子类型的实例。
<!-- Use the `factory` keyword when implementing a constructor that doesn’t
always create a new instance of its class. For example, a factory
constructor might return an instance from a cache, or it might return an
instance of a subtype. -->

如下的例子说明了一个从缓存中返回对象的工厂构造函数：
<!-- The following example demonstrates a factory constructor returning
objects from a cache: -->

<?code-excerpt "misc/lib/language_tour/classes/logger.dart"?>
{% prettify dart %}
class Logger {
  final String name;
  bool mute = false;

  // _cache 是类库中的私有属性，因为它名字前的 _。
  static final Map<String, Logger> _cache =
      <String, Logger>{};

  factory Logger(String name) {
    if (_cache.containsKey(name)) {
      return _cache[name];
    } else {
      final logger = new Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
{% endprettify %}

<div class="alert alert-info" markdown="1">
##注意：##
工厂构造函数是不能获取`this`的。
<!-- **Note:**
Factory constructors have no access to `this`. -->
</div>

要调用一个工厂构造函数，您需要使用`new`关键词：
<!-- To invoke a factory constructor, you use the `new` keyword: -->

<?code-excerpt "misc/lib/language_tour/classes/logger.dart (logger)"?>
{% prettify dart %}
var logger = new Logger('UI');
logger.log('Button clicked');
{% endprettify %}


### 方法
<!-- ### Methods -->

方法就是为一个对象描述行为的函数。
<!-- Methods are functions that provide behavior for an object. -->

#### 实例方法
<!-- #### Instance methods -->

对象的实例方法可以获取实例的变量和实例的`this`。如下例子中的`distanceTo()`方法就是
这样的一个实例方法。
<!-- Instance methods on objects can access instance variables and `this`.
The `distanceTo()` method in the following sample is an example of an
instance method: -->

<?code-excerpt "misc/lib/language_tour/classes/point.dart (class-with-distanceTo)"?>
{% prettify dart %}
import 'dart:math';

class Point {
  num x, y;

  Point(this.x, this.y);

  num distanceTo(Point other) {
    var dx = x - other.x;
    var dy = y - other.y;
    return sqrt(dx * dx + dy * dy);
  }
}
{% endprettify %}

#### Getters 和 setters
<!-- #### Getters and setters -->

Getters和setters是为对象的属性提供读、写功能的特殊方法。回忆一下每个实例变量都有一个
隐性的getter，如果合适的话，还会有一个setter。您可以使用getters和setters来实现额外
的属性，通过使用`get`和`set`关键词：
<!-- Getters and setters are special methods that provide read and write
access to an object’s properties. Recall that each instance variable has
an implicit getter, plus a setter if appropriate. You can create
additional properties by implementing getters and setters, using the
`get` and `set` keywords: -->

<?code-excerpt "misc/lib/language_tour/classes/rectangle.dart"?>
{% prettify dart %}
class Rectangle {
  num left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  // 定义两个计算得来的属性，right和bottom
  num get right => left + width;
  set right(num value) => left = value - width;
  num get bottom => top + height;
  set bottom(num value) => top = value - height;
}

void main() {
  var rect = new Rectangle(3, 4, 20, 15);
  assert(rect.left == 3);
  rect.right = 12;
  assert(rect.left == -8);
}
{% endprettify %}

通过使用getters和setters，您可以以实例变量为起点，之后把他们装进方法里，而完全不需要
改变类外部的代码。
<!-- With getters and setters, you can start with instance variables, later
wrapping them with methods, all without changing client code. -->

<div class="alert alert-info" markdown="1">
**注意：**
运算符，比如增加（++），是以一种意料之中的方式运作的，是不管getter是否显示地定义过的。
要避免意料之外的效果，这种运算符只会明确地调用getter一次，把塔的值存在一个零时变量中。
<!-- **Note:**
Operators such as increment (++) work in the expected way, whether or
not a getter is explicitly defined. To avoid any unexpected side
effects, the operator calls the getter exactly once, saving its value
in a temporary variable. -->
</div>

#### 抽象方法 - Abstract
<!-- #### Abstract methods -->

实例，getter，和setter方法可以是抽象（*abstract*）的。抽象的意思是定义一个接口，但把
具体实现的任务交给其他类。抽象方法只会在[抽象类 abstract classes](#abstract-classes)中出现。
<!-- Instance, getter, and setter methods can be abstract, defining an
interface but leaving its implementation up to other classes.
Abstract methods can only exist in [abstract classes](#abstract-classes). -->

想让一个方法变成抽象方法，使用一个分号（；），不要写方法逻辑：
<!-- To make a method abstract, use a semicolon (;) instead of a method body: -->

<?code-excerpt "misc/lib/language_tour/classes/doer.dart"?>
{% prettify dart %}
abstract class Doer {
  // Define instance variables and methods...

  void doSomething(); // 定义一个抽象方法。
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // 提供一个实现，所有这里的方法并不是抽象的
  }
}
{% endprettify %}

调用一个抽象方法会产生运行时错误。
<!-- Calling an abstract method results in a runtime error. -->

#### 可覆盖运算符 - Overridable operators
<!-- #### Overridable operators -->

您可以覆盖在下面表格中的运算符。比如说，如果您定义了一个向量（*Vector*）类，你
可以把`+`方法定义成两个向量的相加。
<!-- You can override the operators shown in the following table.
For example, if you define a
Vector class, you might define a `+` method to add two vectors. -->

`<`  | `+`  | `|`  | `[]`
`>`  | `/`  | `^`  | `[]=`
`<=` | `~/` | `&`  | `~`
`>=` | `*`  | `<<` | `==`
`–`  | `%`  | `>>`
{:.table}

如下是个覆盖`+`和`-`运算符的例子：
<!-- Here’s an example of a class that overrides the `+` and `-` operators: -->

<?code-excerpt "misc/lib/language_tour/classes/vector.dart"?>
{% prettify dart %}
class Vector {
  final int x, y;

  const Vector(this.x, this.y);

  /// 覆盖 + (a + b).
  Vector operator +(Vector v) {
    return new Vector(x + v.x, y + v.y);
  }

  /// 覆盖 - (a - b).
  Vector operator -(Vector v) {
    return new Vector(x - v.x, y - v.y);
  }
}

void main() {
  final v = new Vector(2, 3);
  final w = new Vector(2, 2);

  // v == (2, 3)
  assert(v.x == 2 && v.y == 3);

  // v + w == (4, 5)
  assert((v + w).x == 4 && (v + w).y == 5);

  // v - w == (0, 1)
  assert((v - w).x == 0 && (v - w).y == 1);
}
{% endprettify %}

如果您覆盖了`==`，您必须同时覆盖对象的`hashCode`getter。在[Implementing map keys](/guides/libraries/library-tour#implementing-map-keys)查看这样的一个例子。
<!-- If you override `==`, you should also override Object's `hashCode` getter.
For an example of overriding `==` and `hashCode`, see
[Implementing map keys](/guides/libraries/library-tour#implementing-map-keys). -->

更多的关于覆盖的信息，查看[Extending a class](#extending-a-class)。
<!-- For more information on overriding, in general, see
[Extending a class](#extending-a-class). -->

### 抽象类 Abstract classes
<!-- ### Abstract classes -->

使用`abstact`修饰符来定义一个*抽象类-abstact class*，抽象类是一种不能被实例化的类，
它也是一种非常好的定义接口的方法，同时也可以实现一部分的功能。如果您希望您的抽象类可以
实例化，那么就定义一个[工厂构造函数](#factory-constructors)。
<!-- Use the `abstract` modifier to define an *abstract class*—a class that
can’t be instantiated. Abstract classes are useful for defining
interfaces, often with some implementation. If you want your abstract
class to appear to be instantiable, define a [factory
constructor](#factory-constructors). -->

抽象类通常都有[抽象方法-abstract methods](#abstract-methods)。如下是一个定义了
抽象方法的抽象类的例子：
<!-- Abstract classes often have [abstract methods](#abstract-methods).
Here’s an example of declaring an abstract class that has an abstract
method: -->

<?code-excerpt "misc/lib/language_tour/classes/misc.dart (abstract)"?>
{% prettify dart %}
// 这个类被声明为抽象类，因此不能被实例化
abstract class AbstractContainer {
  // 定义构造函数，字段，方法

  void updateChildren(); // 抽象方法
}
{% endprettify %}


### 隐式接口
<!-- ### Implicit interfaces -->

每个类都隐式地定义了一个接口，此接口包含这个类的所有实例成员和其所实现的所有接口。如果你
希望创建一个类，A。你还希望A提供另一个类B的API，但不去具体基础B类的实现，那么A类必须实
现B的接口。
<!-- Every class implicitly defines an interface containing all the instance
members of the class and of any interfaces it implements. If you want to
create a class A that supports class B’s API without inheriting B’s
implementation, class A should implement the B interface. -->

一个类可以实现一个或者多个接口，方法是在`implements`代码段中声明需要实现的接口并且提供
接口所需要的API。如下所示：
<!-- A class implements one or more interfaces by declaring them in an
`implements` clause and then providing the APIs required by the
interfaces. For example: -->

<?code-excerpt "misc/lib/language_tour/classes/impostor.dart"?>
{% prettify dart %}
// 一个Person类。它的隐式接口包含了greet()方法。
class Person {
  // 也在接口中，但只在当前函数库汇可见。
  final _name;

  // 不在接口中，因为是个构造函数。
  Person(this._name);

  // 在接口中。
  String greet(String who) => 'Hello, $who. I am $_name.';
}

// 一个对于Person接口的现实。
class Impostor implements Person {
  get _name => '';

  String greet(String who) => 'Hi $who. Do you know who I am?';
}

String greetBob(Person person) => person.greet('Bob');

void main() {
  print(greetBob(new Person('Kathy')));
  print(greetBob(new Impostor()));
}
{% endprettify %}

如下是一个实现了多个接口的类的例子：
<!-- Here’s an example of specifying that a class implements multiple
interfaces: -->

<?code-excerpt "misc/lib/language_tour/classes/misc.dart (point_interfaces)"?>
{% prettify dart %}
class Point implements Comparable, Location {
  // ···
}
{% endprettify %}


### 扩展一个类
<!-- ### Extending a class -->

使用`extends`来创建一个子类，并且用`super`来指代父类：
<!-- Use `extends` to create a subclass, and `super` to refer to the
superclass: -->

<?code-excerpt "misc/lib/language_tour/classes/extends.dart" replace="/extends|super/[!$&!]/g"?>
{% prettify dart %}
class Television {
  void turnOn() {
    _illuminateDisplay();
    _activateIrSensor();
  }
  // ···
}

class SmartTelevision [!extends!] Television {
  void turnOn() {
    [!super!].turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }
  // ···
}
{% endprettify %}

#### 覆盖类成员
<!-- #### Overriding members -->

子类可以覆盖父类的实例方法，getters和setters。您可以使用`@override` 
描述（*annotation*）来告诉Dart您希望覆盖一个成员：
<!-- Subclasses can override instance methods, getters, and setters.
You can use the `@override` annotation to indicate that you are
intentionally overriding a member: -->

<?code-excerpt "misc/lib/language_tour/metadata/television.dart (override)" replace="/@override/[!$&!]/g"?>
{% prettify dart %}
class SmartTelevision extends Television {
  [!@override!]
  void turnOn() {
    // ···
  }
  // ···
}
{% endprettify %}

要缩小代码中[类型安全-type safe](/guides/language/sound-dart)的方法或者实例变量的参数类型，
您可以使用[`covariant` 关键词](/guides/language/sound-problems#the-covariant-keyword).
<!-- To narrow the type of a method parameter or instance variable in code that is
[type safe](/guides/language/sound-dart),
you can use the [`covariant` keyword](/guides/language/sound-problems#the-covariant-keyword). -->


#### noSuchMethod()

如果想检测并且应对代码尝试使用不存在的方法或者实例变量的情况，您可以覆盖`noSuchMethod()`方法:
<!-- To detect or react whenever code attempts to use a non-existent method or
instance variable, you can override `noSuchMethod()`: -->

<?code-excerpt "misc/lib/language_tour/classes/no_such_method.dart" replace="/noSuchMethod(?!,)/[!$&!]/g"?>
{% prettify dart %}
class A {
  // 除非您覆盖了noSuchMethod，使用一个不存在的成员会导致一个
  // NoSuchMethodError错误
  @override
  void [!noSuchMethod!](Invocation invocation) {
    print('You tried to use a non-existent member: ' +
        '${invocation.memberName}');
  }
}
{% endprettify %}

您**不能触发**一个未被实现的方法，除非下列的**一种**情况为真:
<!-- You **can't invoke** an unimplemented method unless
**one** of the following is true: -->

* 接收者有一个静态的`dynamic`类型。
<!-- * The receiver has the static type `dynamic`. -->

* 接收者有一个静态类型，并且定义了这个未被实现的方法（abstact也行），
同时，这个dynamic类型的接受者有一个`noSuchMethod()`的实现，而且
这个实现和`Object`类中的不同。
<!-- * The receiver has a static type that
defines the unimplemented method (abstract is OK),
and the dynamic type of the receiver has an implemention of `noSuchMethod()`
that's different from the one in class `Object`. -->

更多的信息，查看[nosuchMethod forwarding specification。](https://github.com/dart-lang/sdk/blob/master/docs/language/informal/nosuchmethod-forwarding.md)
<!-- For more information, see the informal
[nosuchMethod forwarding specification.](https://github.com/dart-lang/sdk/blob/master/docs/language/informal/nosuchmethod-forwarding.md) -->


<a id="enums"></a>
### 枚举类型 Enumerated types
<!-- ### Enumerated types -->

枚举类型，经常被称为 _enumerations_ 或者 _enums_，是一种用来
表示固定数量的常量的特殊类。
<!-- Enumerated types, often called _enumerations_ or _enums_,
are a special kind of class used to represent
a fixed number of constant values. -->


#### 使用 enums
<!-- #### Using enums -->

使用`enum`关键词来声明枚举类型：
<!-- Declare an enumerated type using the `enum` keyword: -->

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (enum)"?>
{% prettify dart %}
enum Color { red, green, blue }
{% endprettify %}

一个enum中的每个值都有一个`index`getter，这个getter回返回一个在enum声明中的
以0开始的位置值。举例来说，第一个值有index 0，第二个值有index 1.
<!-- Each value in an enum has an `index` getter,
which returns the zero-based position of the value in the enum declaration.
For example, the first value has index 0,
and the second value has index 1. -->

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (index)"?>
{% prettify dart %}
assert(Color.red.index == 0);
assert(Color.green.index == 1);
assert(Color.blue.index == 2);
{% endprettify %}

如果想获取enum中所有值的列表，使用enum的`values`常量。
<!-- To get a list of all of the values in the enum,
use the enum's `values` constant. -->

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (values)"?>
{% prettify dart %}
List<Color> colors = Color.values;
assert(colors[2] == Color.blue);
{% endprettify %}

您可以在[switch statements](#switch-and-case)使用enums，而且如果您没有
处理enum所有值的情况，程序回产生一个警告：
<!-- You can use enums in [switch statements](#switch-and-case), and
you'll get a warning if you don't handle all of the enum's values: -->

<?code-excerpt "misc/lib/language_tour/classes/enum.dart (switch)"?>
{% prettify dart %}
var aColor = Color.blue;

switch (aColor) {
  case Color.red:
    print('Red as roses!');
    break;
  case Color.green:
    print('Green as grass!');
    break;
  default: // 如果没有defaul，您会看见一个WARNING。
    print(aColor); // 'Color.blue'
}
{% endprettify %}

枚举类型有如下限制：
<!-- Enumerated types have the following limits: -->

* 您不可以在enum中使用子类（subclass），混入（mix in,）或者实现（implement）一个接口。
<!-- * You can't subclass, mix in, or implement an enum. -->
* 您不可以显式地初始化一个enum。
<!-- * You can't explicitly instantiate an enum. -->

更多的信息，查看[Dart Language Specification](/guides/language/spec)。
<!-- For more information, see the
[Dart Language Specification](/guides/language/spec). -->


### 为类增加功能：混入 - mixins
<!-- ### Adding features to a class: mixins -->

混入（Mixins）是一种在多个类结构中复用一个类的代码的方法。
<!-- Mixins are a way of reusing a class's code in multiple class
hierarchies. -->

要使用mixin，需要使用`with`关键词，并在关键词后跟上一个或多个mixin的名称。如下
的代码展示了两个使用minxins的类的例子：
<!-- To use a mixin, use the `with` keyword followed by one or more mixin
names. The following example shows two classes that use mixins: -->

<?code-excerpt "misc/lib/language_tour/classes/orchestra.dart (Musician and Maestro)" replace="/(with.*) \{/[!$1!] {/g"?>
{% prettify dart %}
class Musician extends Performer [!with Musical!] {
  // ···
}

class Maestro extends Person
    [!with Musical, Aggressive, Demented!] {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
{% endprettify %}

要实现一个mixin，创建一个继承了Ojbect类的类，不要声明构造函数，并且不要调用`super`。
举个例子：
<!-- To implement a mixin, create a class that extends Object,
declares no constructors, and has no calls to `super`. For example: -->

<?code-excerpt "misc/lib/language_tour/classes/orchestra.dart (Musical)"?>
{% prettify dart %}
abstract class Musical {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;

  void entertainMe() {
    if (canPlayPiano) {
      print('Playing piano');
    } else if (canConduct) {
      print('Waving hands');
    } else {
      print('Humming to self');
    }
  }
}
{% endprettify %}

<div class="alert alert-info" markdown="1">
**Note：**
从Dart 1.13开始，有两个关于mixins的限制被移除了：

* Mixins可以运行从一个不是Object的类拓展。
* Mixins可以调用`super()`。

这种“超级mixins”没有被[dart2js 支持](https://github.com/dart-lang/sdk/issues/23773)，
并且需要在dartanalyzer使用`--supermixin` flag。
<!-- **Note:**
As of 1.13, two restrictions on mixins have been lifted
from the Dart VM:

* Mixins allow extending from a class other than Object.
* Mixins can call `super()`.

These "super mixins" are
[not yet supported in dart2js](https://github.com/dart-lang/sdk/issues/23773)
and require the `--supermixin` flag in dartanalyzer. -->
</div>

更多的信息，查看这个文章：[Mixins in
Dart。](/articles/language/mixins)


### 类变量和类方法
<!-- ### Class variables and methods -->

使用`static`关键词来实现类范围内的变量和方法。
<!-- Use the `static` keyword to implement class-wide variables and methods. -->

#### 静态变量
<!-- #### Static variables -->

静态变量（类变量）在定义类范围内的状态和常量是十分有用的：
<!-- Static variables (class variables) are useful for class-wide state and
constants: -->

<?code-excerpt "misc/lib/language_tour/classes/misc.dart (static-field)"?>
{% prettify dart %}
class Queue {
  static const int initialCapacity = 16;
  // ···
}

void main() {
  assert(Queue.initialCapacity == 16);
}
{% endprettify %}

静态变量在他们被使用之前是不会被初始化的。
<!-- Static variables aren’t initialized until they’re used. -->

<div class="alert alert-info" markdown="1">
**注意：**
这个页面的内容遵从了[style guide
recommendation](/guides/language/effective-dart/style#identifiers)，它推荐使用
`小写驼峰法 - lowerCamelCase`来给常量命名。
<!-- **Note:**
This page follows the [style guide
recommendation](/guides/language/effective-dart/style#identifiers)
of preferring `lowerCamelCase` for constant names. -->
</div>

#### 静态方法
<!-- #### Static methods -->

静态方法（类方法）是不会作用在实例伤的，因此没发获取`this`。如下所示：
<!-- Static methods (class methods) do not operate on an instance, and thus
do not have access to `this`. For example: -->

<?code-excerpt "misc/lib/language_tour/classes/point_with_distance_method.dart"?>
{% prettify dart %}
import 'dart:math';

class Point {
  num x, y;
  Point(this.x, this.y);

  static num distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}

void main() {
  var a = new Point(2, 2);
  var b = new Point(4, 4);
  var distance = Point.distanceBetween(a, b);
  assert(2.8 < distance && distance < 2.9);
  print(distance);
}
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**
在定义常见的或者广泛使用的工具函数时，考虑使用顶级top-level函数，而不是静态方法。
<!-- **Note:**
Consider using top-level functions, instead of static methods, for
common or widely used utilities and functionality. -->
</div>

您可以使用静态方法作为编译时常量。举个例子，您可以把静态方法作为参数传入常量构造函数中。
<!-- You can use static methods as compile-time constants. For example, you
can pass a static method as a parameter to a constant constructor. -->


## 泛型 Generics

如果您看过了最基本的[列表（数组）类型 List][List]的API文档，您应该看到了实际上的类型是`List<E>`。
这个\<...\>符号标记了一个被称为*泛型（generic）*的，也被称为*参数化（parameterized）*的类型，
这种类型有正式的参数类型。根据规范，类型变量有个单字母的名称，比如 E，T，S，K和V。
<!-- If you look at the API documentation for the basic array type,
[List,][List] you’ll see that the
type is actually `List<E>`. The \<...\> notation marks List as a
*generic* (or *parameterized*) type—a type that has formal type
parameters. By convention, type variables have single-letter names, such
as E, T, S, K, and V. -->


### 为什么要用泛型？
<!-- ### Why use generics? -->

泛型通常被用来确保类型安全，但他们除了使您的代码可以运行之外，其实还有其他的好处：
<!-- Generics are often required for type safety, but they have more benefits
than just allowing your code to run: -->

* 定义合适的泛型会生成出更好的代码
<!-- * Properly specifying generic types results in better generated code. -->
* 您可以使用泛型来减少重复的代码
<!-- * You can use generics to reduce code duplication. -->

如果您有意使一个列表只可包含string，那么您可以声明它为`List<String>`（被读作“字符串列表”）。
通过这种方法，您、您的程序员同伴、还有您的工具就可以在您给这个列表传入非string值时意识到有错
误发生。如下是这样的一个例子：
<!-- If you intend for a list to contain only strings, you can
declare it as `List<String>` (read that as “list of string”). That way
you, your fellow programmers, and your tools can detect that assigning a non-string to
the list is probably a mistake. Here’s an example: -->

{:.fails-sa}
<?code-excerpt "misc/lib/language_tour/generics/misc.dart (why-generics)"?>
{% prettify dart %}
var names = new List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
names.add(42); // 报错
{% endprettify %}

另外一个理由是减少重复的代码。泛型是您可以分享一个接口，并在多个类型中实现它，而且还是在
不影响有利的静态分析的情况下。举个例子，比如说您新建了一个用来缓存某个对象的接口：
<!-- Another reason for using generics is to reduce code duplication.
Generics let you share a single interface and implementation between
many types, while still taking advantage of static
analysis. For example, say you create an interface for
caching an object: -->

<?code-excerpt "misc/lib/language_tour/generics/cache.dart (ObjectCache)"?>
{% prettify dart %}
abstract class ObjectCache {
  Object getByKey(String key);
  void setByKey(String key, Object value);
}
{% endprettify %}

您发现您需要一个string类型的此接口，于是您创建了另一个接口：
<!-- You discover that you want a string-specific version of this interface,
so you create another interface: -->

<?code-excerpt "misc/lib/language_tour/generics/cache.dart (StringCache)"?>
{% prettify dart %}
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);
}
{% endprettify %}

再然后您发现您需要一个number类型的此接口。。。您应该明白这里的意思了。
<!-- Later, you decide you want a number-specific version of this
interface... You get the idea. -->

泛型可以使您避免这样的要创建多个接口的麻烦。使用泛型，您只需要创建一个有类型参数的接口：
<!-- Generic types can save you the trouble of creating all these interfaces.
Instead, you can create a single interface that takes a type parameter: -->

<?code-excerpt "misc/lib/language_tour/generics/cache.dart (Cache)"?>
{% prettify dart %}
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
{% endprettify %}

在这个代码中，T是一个占位类型。您可以把它想成开发者会在之后定义的类型。
<!-- In this code, T is the stand-in type. It’s a placeholder that you can
think of as a type that a developer will define later. -->


### 使用集合-collection字面量
<!-- ### Using collection literals -->

列表（List）和字典（map）是可以被参数化的。参数化字面量和您之前看到的字面量是一样的，
除了您需要在括号前给List增加<code>&lt;<em>type</em>></code>和给map增加<code>&lt;<em>keyType</em>, <em>valueType</em>></code>。这是一些例子：
<!-- List and map literals can be parameterized. Parameterized literals are
just like the literals you’ve already seen, except that you add
<code>&lt;<em>type</em>></code> (for lists) or
<code>&lt;<em>keyType</em>, <em>valueType</em>></code> (for maps)
before the opening bracket. Here
is example of using typed literals: -->

<?code-excerpt "misc/lib/language_tour/generics/misc.dart (collection-literals)"?>
{% prettify dart %}
var names = <String>['Seth', 'Kathy', 'Lars'];
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
{% endprettify %}

### 和构造函数配合使用泛型
<!-- ### Using parameterized types with constructors -->

要在构造函数中确定一个或者多个类型，在类名后的`<...>`中放入需要的类型。如下所示：
<!-- To specify one or more types when using a constructor, put the types in
angle brackets (`<...>`) just after the class name. For example: -->

<?code-excerpt "misc/test/language_tour/generics_test.dart (constructor-1)"?>
{% prettify dart %}
var names = new List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
var nameSet = new Set<String>.from(names);
{% endprettify %}

下面的代码创建了一个有integer作为key，View作为值的map：
<!-- The following code creates a map that has integer keys and values of
type View: -->

<?code-excerpt "misc/test/language_tour/generics_test.dart (constructor-2)"?>
{% prettify dart %}
var views = new Map<int, View>();
{% endprettify %}


### 泛型集合和他们所包含的类型
<!-- ### Generic collections and the types they contain -->

Dart的泛型是*真实的 reified*，这意味着在运行时，泛型是包含它们的类型信息的。举个例子，您可以
在一个集合中测试它的类型：
<!-- Dart generic types are *reified*, which means that they carry their type
information around at runtime. For example, you can test the type of a
collection: -->

<?code-excerpt "misc/test/language_tour/generics_test.dart (generic-collections)"?>
{% prettify dart %}
var names = new List<String>();
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**
与之相反，Java中的泛型是*擦除的erasure*，这意味着泛型参数在运行时是被移除的。在Java中，
您可以测试一个对象是否是List，但你不能知道它是否是`List<String>`。
<!-- **Note:**
In contrast, generics in Java use *erasure*, which means that generic
type parameters are removed at runtime. In Java, you can test whether
an object is a List, but you can’t test whether it’s a `List<String>`. -->
</div>


### 限定泛型的类型参数
<!-- ### Restricting the parameterized type -->

当实现一个泛型时，您也许希望限定它可用的类型。您可以使用`extends`关键词：
<!-- When implementing a generic type,
you might want to limit the types of its parameters.
You can do this using `extends`. -->

<?code-excerpt "misc/lib/language_tour/generics/base_class.dart" replace="/extends SomeBaseClass(?=. \{)/[!$&!]/g"?>
{% prettify dart %}
class Foo<T [!extends SomeBaseClass!]> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'";
}

class Extender extends SomeBaseClass {...}
{% endprettify %}

如此一来，您就只能使用`SomeBaseClass`类或者它的子类作为泛型的类型参数：
<!-- It's OK to use `SomeBaseClass` or any of its subclasses as generic argument: -->

<?code-excerpt "misc/test/language_tour/generics_test.dart (SomeBaseClass-ok)" replace="/Foo.\w+./[!$&!]/g"?>
{% prettify dart %}
var someBaseClassFoo = new [!Foo<SomeBaseClass>!]();
var extenderFoo = new [!Foo<Extender>!]();
{% endprettify %}

您可以不填入泛型的类型参数：
<!-- It's also OK to specify no generic argument: -->

<?code-excerpt "misc/test/language_tour/generics_test.dart (no-generic-arg-ok)" replace="/expect\((.*?).toString\(\), .(.*?).\);/print($1); \/\/ $2/g"?>
{% prettify dart %}
var foo = new Foo();
print(foo); // Instance of 'Foo<SomeBaseClass>'
{% endprettify %}

但是填入一个不是`SomeBaseClass`类的类型会导致一个错误：
<!-- Specifying any non-`SomeBaseClass` type results in an error: -->

{:.fails-sa}
<?code-excerpt "misc/lib/language_tour/generics/misc.dart (Foo-Object-error)" replace="/Foo.\w+./[!$&!]/g"?>
{% prettify dart %}
var foo = new [!Foo<Object>!]();
{% endprettify %}


### 使用泛型方法
<!-- ### Using generic methods -->

在一开始，Dart对类的泛型支持是有限的。但现在，一个新的语法，_generic methods_,允许在方法和函数
中使用类型参数：
<!-- Initially, Dart's generic support was limited to classes.
A newer syntax, called _generic methods_, allows type arguments on methods and functions: -->

<!-- https://dartpad.dartlang.org/a02c53b001977efa4d803109900f21bb -->
<!-- https://gist.github.com/a02c53b001977efa4d803109900f21bb -->
<?code-excerpt "misc/test/language_tour/generics_test.dart (method)" replace="/<T.(?=\()|T/[!$&!]/g"?>
{% prettify dart %}
[!T!] first[!<T>!](List<[!T!]> ts) {
  // 做一些初始化构造或者错误检查，然后。。。
  [!T!] tmp = ts[0];
  // 做一些额外的检查或者处理
  return tmp;
}
{% endprettify %}

这里在`first` (`<T>`)上的泛型类型参数运行您在如下的地方使用`T`: 
<!-- Here the generic type parameter on `first` (`<T>`)
allows you to use the type argument `T` in several places: -->

* 方法的返回类型(`T`)
* 方法参数的类型(`List<T>`)
* 方法本地变量的类型(`T tmp`)
<!-- * In the function's return type (`T`).
* In the type of an argument (`List<T>`).
* In the type of a local variable (`T tmp`). -->

更多关于泛型的信息，查看[Using Generic Methods。](https://github.com/dart-lang/sdk/blob/master/pkg/dev_compiler/doc/GENERIC_METHODS.md)
<!-- For more information about generics, see
[Using Generic Methods.](https://github.com/dart-lang/sdk/blob/master/pkg/dev_compiler/doc/GENERIC_METHODS.md) -->


## 类库和可访问性
<!-- ## Libraries and visibility -->

`import`和`library`指令可以帮助你创建模块和可复用代码。类库不仅仅提供了API，而且还时
一个隐私单元：以下划线（\_）起头的标识符是只在类库内部可见的。不管有没有使用`library`
指令，*Dart程序的每个部分都是一个类库*。。
<!-- The `import` and `library` directives can help you create a
modular and shareable code base. Libraries not only provide APIs, but
are a unit of privacy: identifiers that start with an underscore (\_)
are visible only inside the library. *Every Dart app is a library*, even
if it doesn’t use a `library` directive. -->

类库可以被打包发布。查看[Pub Package and Asset Manager](/tools/pub)来了解pub，一
个Dart SDK自带的包管理器。
<!-- Libraries can be distributed using packages. See
[Pub Package and Asset Manager](/tools/pub)
for information about
pub, a package manager included in the SDK. -->


### 使用类库
<!-- ### Using libraries -->

使用`import`来确定一个类库在其他类库域中的命名空间（*namespace*）。
<!-- Use `import` to specify how a namespace from one library is used in the
scope of another library. -->

举个例子，Dart web 应用基本都会使用[dart:html][]类库，它们会这样引入：
<!-- For example, Dart web apps generally use the [dart:html][]
library, which they can import like this: -->

<?code-excerpt "misc/test/language_tour/browser_test.dart (dart-html-import)"?>
{% prettify dart %}
import 'dart:html';
{% endprettify %}

`import`唯一需要的参数就是一个用来确定类库的URI（Universal Resource Identifier）。
对于内置类库，URI会有`dart:`这样的一种语法准则。对于其他的类库，您可以使用文件系统的路径，或者
`package:`这样的语法准则。`package`语法准则确定了由像pub这样的包管理器所提供的类库。举个例子：
<!-- The only required argument to `import` is a URI specifying the
library.
For built-in libraries, the URI has the special `dart:` scheme.
For other libraries, you can use a file system path or the `package:`
scheme. The `package:` scheme specifies libraries provided by a package
manager such as the pub tool. For example: -->

<?code-excerpt "misc/test/language_tour/browser_test.dart (package-import)"?>
{% prettify dart %}
import 'package:test/test.dart';
{% endprettify %}

<div class="alert alert-info" markdown="1">
**注意：**
*URI* 是指uniform resource identifier。
*URL* 是指uniform resource locators，是一种常见的URI。
<!-- **Note:**
*URI* stands for uniform resource identifier.
*URLs* (uniform resource locators) are a common kind of URI. -->
</div>


#### 确定一个类库的前缀
<!-- #### Specifying a library prefix -->

如果您引入了两个有相互冲突的标识符的类库，那么您需要为其中一个，或者全部的两个类库确定前缀。
举例来说，如果library1和library2都有一个Element类，那么您的代码需要和下面的代码一样：
<!-- If you import two libraries that have conflicting identifiers, then you
can specify a prefix for one or both libraries. For example, if library1
and library2 both have an Element class, then you might have code like
this: -->

<?code-excerpt "misc/lib/language_tour/libraries/import_as.dart" replace="/(lib\d)\.dart/package:$1\/$&/g"?>
{% prettify dart %}
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = new Element();

// Uses Element from lib2.
lib2.Element element2 = new lib2.Element();
{% endprettify %}

#### 引用类库中的部分代码
<!-- #### Importing only part of a library -->

如果您只想使用类库中的部分代码，您可以选择性地引入类库，如下例：
<!-- If you want to use only part of a library, you can selectively import
the library. For example: -->

<?code-excerpt "misc/lib/language_tour/libraries/show_hide.dart" replace="/(lib\d)\.dart/package:$1\/$&/g"?>
{% prettify dart %}
// 只引入foo
import 'package:lib1/lib1.dart' show foo;

// 引入除了foo的其他代码
import 'package:lib2/lib2.dart' hide foo;
{% endprettify %}

<a id="deferred-loading"></a>
#### 懒加载类库
<!-- #### Lazily loading a library -->

_延迟加载_(也被叫做 _懒加载_)允许应用只在需要的时候再引入一个类库。
您可以在下列的情况下使用这个功能：
<!-- _Deferred loading_ (also called _lazy loading_)
allows an application to load a library on demand,
if and when it's needed.
Here are some cases when you might use deferred loading: -->

* 减少app首次加载的时间。
* 进行A/B测试的时候，比如尝试不同的替代算法。
* 引入很少用到的函数功能，比如一些可选的界面和对话框。
<!-- * To reduce an app's initial startup time.
* To perform A/B testing—trying out
  alternative implementations of an algorithm, for example.
* To load rarely used functionality, such as optional screens and dialogs. -->

您必须使用`deferred as`来引用懒加载的类库。
<!-- To lazily load a library, you must first
import it using `deferred as`. -->

<?code-excerpt "misc/lib/language_tour/libraries/greeter.dart (import)" replace="/hello\.dart/package:greetings\/$&/g"?>
{% prettify dart %}
import 'package:greetings/hello.dart' deferred as hello;
{% endprettify %}

然后在需要使用类库的时候，使用类库的标识符来调用`loadLibrary()`方法。
<!-- When you need the library, invoke
`loadLibrary()` using the library's identifier. -->

<?code-excerpt "misc/lib/language_tour/libraries/greeter.dart (loadLibrary)"?>
{% prettify dart %}
Future greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
{% endprettify %}

在上面的代码中，`await`关键词会使当前进程在类库加载完成前暂停运行。更多的信息，
查看[异步支持 - asynchrony support](#asynchrony-support)。
<!-- In the preceding code,
the `await` keyword pauses execution until the library is loaded.
For more information about `async` and `await`,
see [asynchrony support](#asynchrony-support). -->

您可以对同一个类库多次执行`loadLibrary()`方法。这不会有任何问题，因为类库只会被加载一次。
<!-- You can invoke `loadLibrary()` multiple times on a library without problems.
The library is loaded only once. -->

在使用延时加载时请注意：
<!-- Keep in mind the following when you use deferred loading: -->

* 一个延时加载的类库中的常量不是常量。在延时加载类库加载完成前，这些常量时不存在的。
<!-- * A deferred library's constants aren't constants in the importing file.
  Remember, these constants don't exist until the deferred library is loaded. -->
* 您不可以在引入类库的文件中使用异步类库的类型。如果一定要这样，您可以单独创建一个
接口，并在引入异步类库的文件和异步类库中都另外引入这个接口。
<!-- * You can't use types from a deferred library in the importing file.
  Instead, consider moving interface types to a library imported by
  both the deferred library and the importing file. -->
* 当您使用<code>deferred as <em>namespace</em></code>，时，Dart会自动在命名空间内
引入`loadLibrary()`方法。`loadLibrary()`会返回一个[Future](/guides/libraries/library-tour#future)。
<!-- * Dart implicitly inserts `loadLibrary()` into the namespace that you define
  using <code>deferred as <em>namespace</em></code>.
  The `loadLibrary()` function returns a [Future](/guides/libraries/library-tour#future). -->

### 实现类库
<!-- ### Implementing libraries -->

查看[Create Library Packages](/guides/libraries/create-library-packages)来
了解有关如何实现自己的类库包，本文包含了如下内容：
<!-- See
[Create Library Packages](/guides/libraries/create-library-packages)
for advice on how to implement a library package, including: -->

* 如何组织类库的源代码。
* 如何使用`export`指令。
* 在什么时候使用`part`指令。
<!-- * How to organize library source code.
* How to use the `export` directive.
* When to use the `part` directive. -->


<a id="asynchrony"></a>
## Asynchrony support

Dart libraries are full of functions that
return [Future][] or [Stream][] objects.
These functions are _asynchronous_:
they return after setting up
a possibly time-consuming operation
(such as I/O),
without waiting for that operation to complete.

The `async` and `await` keywords support asynchronous programming,
letting you write asynchronous code that
looks similar to synchronous code.


<a id="await"></a>
### Handling Futures

When you need the result of a completed Future,
you have two options:

* Use `async` and `await`.
* Use the Future API, as described
  [in the library tour](/guides/libraries/library-tour#future).

Code that uses `async` and `await` is asynchronous,
but it looks a lot like synchronous code.
For example, here's some code that uses `await`
to wait for the result of an asynchronous function:

<?code-excerpt "misc/lib/language_tour/async.dart (await-lookUpVersion)"?>
{% prettify dart %}
await lookUpVersion();
{% endprettify %}

To use `await`, code must be in an _async function_—a
function marked as `async`:

<?code-excerpt "misc/lib/language_tour/async.dart (checkVersion)" replace="/async|await/[!$&!]/g"?>
{% prettify dart %}
Future checkVersion() [!async!] {
  var version = [!await!] lookUpVersion();
  // Do something with version
}
{% endprettify %}

<aside class="alert alert-info" markdown="1">
**Note:**
Although an async function might perform time-consuming operations,
it doesn't wait for those operations.
Instead, the async function executes only until it encounters
its first `await` expression
([details][synchronous-async-start]).
Then it returns a Future object,
resuming execution only after the `await` expression completes.
</aside>

Use `try`, `catch`, and `finally`
to handle errors and cleanup in code that uses `await`:

<?code-excerpt "misc/lib/language_tour/async.dart (try-catch)"?>
{% prettify dart %}
try {
  version = await lookUpVersion();
} catch (e) {
  // React to inability to look up the version
}
{% endprettify %}

You can use `await` multiple times in an async function.
For example, the following code waits three times
for the results of functions:

<?code-excerpt "misc/lib/language_tour/async.dart (repeated-await)"?>
{% prettify dart %}
var entrypoint = await findEntrypoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
{% endprettify %}

In <code>await <em>expression</em></code>,
the value of <code><em>expression</em></code> is usually a Future;
if it isn't, then the value is automatically wrapped in a Future.
This Future object indicates a promise to return an object.
The value of <code>await <em>expression</em></code> is that returned object.
The await expression makes execution pause until that object is available.

**If you get a compile-time error when using `await`,
make sure `await` is in an async function.**
For example, to use `await` in your app's `main()` function,
the body of `main()` must be marked as `async`:

<?code-excerpt "misc/lib/language_tour/async.dart (main)" replace="/async|await/[!$&!]/g"?>
{% prettify dart %}
Future main() [!async!] {
  checkVersion();
  print('In main: version is ${[!await!] lookUpVersion()}');
}
{% endprettify %}


<a id="async"></a>
### Declaring async functions

An _async function_ is a function whose body is marked with
the `async` modifier.

Adding the `async` keyword to a function makes it return a Future.
For example, consider this synchronous function,
which returns a String:

<?code-excerpt "misc/lib/language_tour/async.dart (sync-lookUpVersion)"?>
{% prettify dart %}
String lookUpVersion() => '1.0.0';
{% endprettify %}

If you change it to be an async function—for example,
because a future implementation will be time consuming—the
returned value is a Future:

<?code-excerpt "misc/lib/language_tour/async.dart (async-lookUpVersion)"?>
{% prettify dart %}
Future<String> lookUpVersion() async => '1.0.0';
{% endprettify %}

Note that the function's body doesn't need to use the Future API.
Dart creates the Future object if necessary.

If your function doesn't return a useful value,
make its return type `Future<void>`.

{% comment %}
PENDING: add example here

Where else should we cover generalized void?
{% endcomment %}


<a id="await-for"></a>
### Handling Streams

When you need to get values from a Stream,
you have two options:

* Use `async` and an _asynchronous for loop_ (`await for`).
* Use the Stream API, as described
  [in the library tour](/guides/libraries/library-tour#stream).

<aside class="alert alert-warning" markdown="1">
**Note:**
Before using `await for`, be sure that it makes the code clearer
and that you really do want to wait for all of the stream's results.
For example, you usually should **not** use `await for` for UI event listeners,
because UI frameworks send endless streams of events.
</aside>

An asynchronous for loop has the following form:

<?code-excerpt "misc/lib/language_tour/async.dart (await-for)"?>
{% prettify dart %}
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
{% endprettify %}

The value of <code><em>expression</em></code> must have type Stream.
Execution proceeds as follows:

1. Wait until the stream emits a value.
2. Execute the body of the for loop,
   with the variable set to that emitted value.
3. Repeat 1 and 2 until the stream is closed.

To stop listening to the stream,
you can use a `break` or `return` statement,
which breaks out of the for loop
and unsubscribes from the stream.

**If you get a compile-time error when implementing an asynchronous for loop,
make sure the `await for` is in an async function.**
For example, to use an asynchronous for loop in your app's `main()` function,
the body of `main()` must be marked as `async`:

<?code-excerpt "misc/lib/language_tour/async.dart (number_thinker)" replace="/async|await for/[!$&!]/g"?>
{% prettify dart %}
Future main() [!async!] {
  // ...
  [!await for!] (var request in requestServer) {
    handleRequest(request);
  }
  // ...
}
{% endprettify %}

For more information about asynchronous programming, in general, see the
[dart:async](/guides/libraries/library-tour#dartasync---asynchronous-programming)
section of the library tour.
Also see the articles
[Dart Language Asynchrony Support: Phase 1](/articles/language/await-async)
and
[Dart Language Asynchrony Support: Phase 2](/articles/language/beyond-async),
and the [Dart language specification](/guides/language/spec).


<a id="generator"></a>
## Generators

When you need to lazily produce a sequence of values,
consider using a _generator function_.
Dart has built-in support for two kinds of generator functions:

* **Synchronous** generator: Returns an **[Iterable]** object.
* **Asynchronous** generator: Returns a **[Stream]** object.

To implement a **synchronous** generator function,
mark the function body as `sync*`,
and use `yield` statements to deliver values:

<?code-excerpt "misc/test/language_tour/async_test.dart (sync-generator)"?>
{% prettify dart %}
Iterable<int> naturalsTo(int n) sync* {
  int k = 0;
  while (k < n) yield k++;
}
{% endprettify %}

To implement an **asynchronous** generator function,
mark the function body as `async*`,
and use `yield` statements to deliver values:

<?code-excerpt "misc/test/language_tour/async_test.dart (async-generator)"?>
{% prettify dart %}
Stream<int> asynchronousNaturalsTo(int n) async* {
  int k = 0;
  while (k < n) yield k++;
}
{% endprettify %}

If your generator is recursive,
you can improve its performance by using `yield*`:

<?code-excerpt "misc/test/language_tour/async_test.dart (recursive-generator)"?>
{% prettify dart %}
Iterable<int> naturalsDownFrom(int n) sync* {
  if (n > 0) {
    yield n;
    yield* naturalsDownFrom(n - 1);
  }
}
{% endprettify %}

For more information about generators, see the article
[Dart Language Asynchrony Support: Phase 2](/articles/language/beyond-async).


## Callable classes

To allow your Dart class to be called like a function,
implement the `call()` method.

In the following example, the `WannabeFunction` class defines
a call() function that takes three strings and concatenates them,
separating each with a space, and appending an exclamation.
Click the run button ( {% img 'red-run.png' %} ) to execute the code.

{% comment %}
https://gist.github.com/405379bacf30335f3aed
https://dartpad.dartlang.org/405379bacf30335f3aed

<?code-excerpt "misc/lib/language_tour/callable_classes.dart"?>
{% prettify dart %}
class WannabeFunction {
  String call(String a, String b, String c) => '$a $b $c!';
}

var wf = new WannabeFunction();
var out = wf('Hi', 'there,', 'gang');

main() => print(out);
{% endprettify %}
{% endcomment %}

<iframe
src="{{site.custom.dartpad.embed-dart-prefix}}?id=405379bacf30335f3aed&horizontalRatio=99&verticalRatio=73"
    width="100%"
    height="240px"
    style="border: 1px solid #ccc;">
</iframe>

For more information on treating classes like functions, see
[Emulating Functions in Dart](/articles/language/emulating-functions).

## Isolates

Most computers, even on mobile platforms, have multi-core CPUs.
To take advantage of all those cores, developers traditionally use
shared-memory threads running concurrently. However, shared-state
concurrency is error prone and can lead to complicated code.

Instead of threads, all Dart code runs inside of *isolates*. Each
isolate has its own memory heap, ensuring that no isolate’s state is
accessible from any other isolate.

For more information, see the
[dart:isolate library documentation.][dart:isolate]


## Typedefs

In Dart, functions are objects, just like strings and numbers are
objects. A *typedef*, or *function-type alias*, gives a function type a
name that you can use when declaring fields and return types. A typedef
retains type information when a function type is assigned to a variable.

Consider the following code, which doesn't use a typedef:

<?code-excerpt "misc/lib/language_tour/typedefs/sorted_collection_1.dart"?>
{% prettify dart %}
class SortedCollection {
  Function compare;

  SortedCollection(int f(Object a, Object b)) {
    compare = f;
  }
}

// Initial, broken implementation.
int sort(Object a, Object b) => 0;

void main() {
  SortedCollection coll = new SortedCollection(sort);

  // All we know is that compare is a function,
  // but what type of function?
  assert(coll.compare is Function);
}
{% endprettify %}

Type information is lost when assigning `f` to `compare`. The type of
`f` is `(Object, ``Object)` → `int` (where → means returns), yet the
type of `compare` is Function. If we change the code to use explicit
names and retain type information, both developers and tools can use
that information.

<?code-excerpt "misc/lib/language_tour/typedefs/sorted_collection_2.dart"?>
{% prettify dart %}
typedef int Compare(Object a, Object b);

class SortedCollection {
  Compare compare;

  SortedCollection(this.compare);
}

// Initial, broken implementation.
int sort(Object a, Object b) => 0;

void main() {
  SortedCollection coll = new SortedCollection(sort);
  assert(coll.compare is Function);
  assert(coll.compare is Compare);
}
{% endprettify %}

<aside class="alert alert-info" markdown="1">
**Note:**
Currently, typedefs are restricted to function types. We expect this
to change.
</aside>

Because typedefs are simply aliases, they offer a way to check the type
of any function. For example:

<?code-excerpt "misc/lib/language_tour/typedefs/misc.dart (compare)"?>
{% prettify dart %}
typedef int Compare<T>(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  assert(sort is Compare<int>); // True!
}
{% endprettify %}

<aside class="alert alert-info" markdown="1">
**New function type syntax:**
Dart 1.24 introduced a new form of function types, the [generic function type
alias.](https://github.com/dart-lang/sdk/blob/master/docs/language/informal/generic-function-type-alias.md)
You might use this feature if you pass around generic methods,
define fields that are function types,
or define arguments with generic function types.
Here's an example of using the new syntax:

<?code-excerpt "misc/lib/language_tour/typedefs/misc.dart (Function)"?>
{% prettify dart %}
typedef F = List<T> Function<T>(T);
{% endprettify %}
</aside>

## Metadata

Use metadata to give additional information about your code. A metadata
annotation begins with the character `@`, followed by either a reference
to a compile-time constant (such as `deprecated`) or a call to a
constant constructor.

Two annotations are available to all Dart code: `@deprecated` and
`@override`. For examples of using `@override`,
see [Extending a class](#extending-a-class).
Here’s an example of using the `@deprecated`
annotation:

<?code-excerpt "misc/lib/language_tour/metadata/television.dart (deprecated)" replace="/@deprecated/[!$&!]/g"?>
{% prettify dart %}
class Television {
  /// _Deprecated: Use [turnOn] instead._
  [!@deprecated!]
  void activate() {
    turnOn();
  }

  /// Turns the TV's power on.
  void turnOn() {
    // ···
  }
}
{% endprettify %}

You can define your own metadata annotations. Here’s an example of
defining a @todo annotation that takes two arguments:

<?code-excerpt "misc/lib/language_tour/metadata/todo.dart"?>
{% prettify dart %}
library todo;

class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
{% endprettify %}

And here’s an example of using that @todo annotation:

<?code-excerpt "misc/lib/language_tour/metadata/misc.dart"?>
{% prettify dart %}
import 'todo.dart';

@Todo('seth', 'make this do something')
void doSomething() {
  print('do something');
}
{% endprettify %}

Metadata can appear before a library, class, typedef, type parameter,
constructor, factory, function, field, parameter, or variable
declaration and before an import or export directive. You can
retrieve metadata at runtime using reflection.


## Comments

Dart supports single-line comments, multi-line comments, and
documentation comments.


### Single-line comments

A single-line comment begins with `//`. Everything between `//` and the
end of line is ignored by the Dart compiler.

<?code-excerpt "misc/lib/language_tour/comments.dart (single-line-comments)"?>
{% prettify dart %}
void main() {
  // TODO: refactor into an AbstractLlamaGreetingFactory?
  print('Welcome to my Llama farm!');
}
{% endprettify %}


### Multi-line comments

A multi-line comment begins with `/*` and ends with `*/`. Everything
between `/*` and `*/` is ignored by the Dart compiler (unless the
comment is a documentation comment; see the next section). Multi-line
comments can nest.

<?code-excerpt "misc/lib/language_tour/comments.dart (multi-line-comments)"?>
{% prettify dart %}
void main() {
  /*
   * This is a lot of work. Consider raising chickens.

  Llama larry = new Llama();
  larry.feed();
  larry.exercise();
  larry.clean();
   */
}
{% endprettify %}


### Documentation comments

Documentation comments are multi-line or single-line comments that begin
with `///` or `/**`. Using `///` on consecutive lines has the same
effect as a multi-line doc comment.

Inside a documentation comment, the Dart compiler ignores all text
unless it is enclosed in brackets. Using brackets, you can refer to
classes, methods, fields, top-level variables, functions, and
parameters. The names in brackets are resolved in the lexical scope of
the documented program element.

Here is an example of documentation comments with references to other
classes and arguments:

<?code-excerpt "misc/lib/language_tour/comments.dart (doc-comments)"?>
{% prettify dart %}
/// A domesticated South American camelid (Lama glama).
///
/// Andean cultures have used llamas as meat and pack
/// animals since pre-Hispanic times.
class Llama {
  String name;

  /// Feeds your llama [Food].
  ///
  /// The typical llama eats one bale of hay per week.
  void feed(Food food) {
    // ...
  }

  /// Exercises your llama with an [activity] for
  /// [timeLimit] minutes.
  void exercise(Activity activity, int timeLimit) {
    // ...
  }
}
{% endprettify %}

In the generated documentation, `[Food]` becomes a link to the API docs
for the Food class.

To parse Dart code and generate HTML documentation, you can use the SDK’s
[documentation generation tool.](https://github.com/dart-lang/dartdoc#dartdoc)
For an example of generated documentation, see the [Dart API
documentation.]({{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}) For advice on how to structure
your comments, see
[Guidelines for Dart Doc Comments.](/guides/language/effective-dart/documentation)


## Summary

This page summarized the commonly used features in the Dart language.
More features are being implemented, but we expect that they won’t break
existing code. For more information, see the [Dart Language
Specification](/guides/language/spec) and
[Effective Dart](/guides/language/effective-dart).

To learn more about Dart's core libraries, see
[A Tour of the Dart Libraries](/guides/libraries/library-tour).

[AssertionError]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/AssertionError-class.html
[dart2js]: {{site.dev-webdev}}/tools/dart2js
[dart:html]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-html
[dart:isolate]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-isolate
[dart:math]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-math
[dart]: /dart-vm/tools/dart-vm
[dartdevc]: {{site.dev-webdev}}/tools/dartdevc
[double]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/double-class.html
[Error]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Error-class.html
[Exception]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Exception-class.html
[flutter debug mode]: https://flutter.io/debugging/#debug-mode-assertions
[forEach()]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Iterable/forEach.html
[Function]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Function-class.html
[Future]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-async/Future-class.html
[identical()]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/identical.html
[int]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/int-class.html
[Iterable]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Iterable-class.html
[js numbers]: https://stackoverflow.com/questions/2802957/number-of-bits-in-javascript-numbers/2803010#2803010
[List]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/List-class.html
[Map]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Map-class.html
[num]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/num-class.html
[Object]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Object-class.html
[ObjectVsDynamic]: /guides/language/effective-dart/design#do-annotate-with-object-instead-of-dynamic-to-indicate-any-object-is-allowed
[StackTrace]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/StackTrace-class.html
[Stream]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-async/Stream-class.html
[String]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/String-class.html
[Symbol]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Symbol-class.html
[synchronous-async-start]: https://github.com/dart-lang/sdk/blob/master/docs/newsletter/20170915.md#synchronous-async-start
[Type]: {{site.dart_api}}/{{site.data.pkg-vers.SDK.channel}}/dart-core/Type-class.html
