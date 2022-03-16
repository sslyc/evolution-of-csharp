<center><font size=7>C#的进化</font></center> 
<center><font size=4>C#发展史、C#1.0-10.0语法系统性梳理、C#与JAVA的对比</font></center>

# 前言

C#也使用了十年有余了。

一路走来，见证了微软从封闭走向开放，从平台捆绑，到成为活跃于Github的重要贡献者。亲历了C#的开创性引领和影响了诸多语言，也看到了其他语言的优秀机制被有机的融合进C#（好吧，我承认语言之间都在互相抄）。在微软的“开发者至上”理念加持下，C#变得越来越好用。如今，\.Net 6已经发布，这是\.Net家族结束混乱的割据，统一后的第一个LTS版本，也是号称迄今为止最快的\.Net。回顾C#的发展历史，一路走来感慨万千。本着温故而知新的精神，和CShaper那该死的想要“安利”的冲动，感觉是时候对C#做个全面的总结了。

写本文还有一个现实原因：在如今的各大技术区中，鲜有细致地讲解C#全版本语法特点（Feature）的文章。而我也发现有不少博主对一些语法理解有所偏差，例如：大多数的文章都没能很好的阐述C#中枚举器（IEnumerator）和迭代器（Iterator）的区别，也没有很好的说明LINQ和迭代器的紧密联系。而对C#语法和Java语法做出全面对比的文章也不是很多。作者希望通过此一文填补这些空缺。

本文将以C#版本为时间线，从C#1.0到C#10.0梳理每个版本的语法。并尽可能**与Java做出对比**。

本文**目标人群**主要是：

1. **CShaper**：
    1. 想对C#从1.0到10.0的语法特点进行系统梳理的人。
    2. 计划转Java，或者纯粹好奇，想了解C#与Java有哪些异同的人。
2. **Javaer**，或者其他非C#的开发者：
    1. 对C#好奇，想对C#做个全面了解的人。
    2. 计划转C#，通过此文可以直接上手开发的人。（我知道没有😔）

本文旨在：

1. 对C#每个版本引入的语法做系统性梳理。
    - 对于老版本，发掘容易忽略的细节，纠正理解上的谬误。
    - 对于新版本，帮助那些对官方文档抱有“英文懒得看，中文看不懂”态度的人，整理和提炼新版本的语法特点。
2. 介绍C#的同时，就语言机制与Java做出对比。让读者能够一次性掌握两种语言的特点和差异。
3. 用词尽量严谨、规范。部分关键名词给出翻译前的原始英文。以免产生谬误而误导读者。
4. 同时照顾CShaper和没有C#开发经验的人，让两者都有所收获。

本文假设阅读者已有一定语言基础，因而不会讲过于基础且与Java无异的部分。但是，如果基础部分与Java有所不同，会指出与Java的不同之处。**与Java的对比部分将使用下面的格式**：

> 在语法的更进上，C#与Java的采用完全不同的策略：C#的更新相对激进，每个版本都会有不少的更新升级，也大量引入了已在其他语言上实现了的优秀机制；Java则以稳字当头，每个版本关于语法层面的更新内容都不是很多，而且往往新的语法都是先发布预览版，在几个Java版本之后才会发布正式版。

本文对C#的语法描述时，如果需要提及更高版本的C#才支持的语法，会显著的标明支持的C#版本。而与Java对比时，因为在如今的使用场景中，开发者基本上至少会使用Java 8以上的版本，所以仅在所涉及的Java语法需要9以上的版本时，才会明确标注所需的Java版本。

为了同时照顾Javaer和CShaper甚至其他语言开发者，本文篇幅会较长（接近15万字）。但是每个知识点的文字其实并不多。读者可以根据需要从目录快速定位到关注的章节（其实你还可以使用搜索大法）。不过，本文的撰写方式，具有知识延续性：每个章节的介绍会假设之前章节介绍的内容读者已经掌握。因而对于非CShaper而言，跳过章节需要慎重，可能会使相应章节的部分名词和代码难以理解。

---

# 目录

<!-- TOC -->

- [前言](#%E5%89%8D%E8%A8%80)
- [目录](#%E7%9B%AE%E5%BD%95)
- [正文之前](#%E6%AD%A3%E6%96%87%E4%B9%8B%E5%89%8D)
    - [基本概念](#%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)
        - [C#](#c)
        - [\.Net](#%5Cnet)
    - [\.Net和C#发展史](#%5Cnet%E5%92%8Cc%E5%8F%91%E5%B1%95%E5%8F%B2)
    - [本文的重点是语法，而非类库](#%E6%9C%AC%E6%96%87%E7%9A%84%E9%87%8D%E7%82%B9%E6%98%AF%E8%AF%AD%E6%B3%95%E8%80%8C%E9%9D%9E%E7%B1%BB%E5%BA%93)
- [Hello World](#hello-world)
    - [命名空间（Namespace）](#%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4namespace)
    - [using语句](#using%E8%AF%AD%E5%8F%A5)
- [C# 1.0 —— Java的替代品](#c-10--java%E7%9A%84%E6%9B%BF%E4%BB%A3%E5%93%81)
    - [类（Class）和结构（Struct）](#%E7%B1%BBclass%E5%92%8C%E7%BB%93%E6%9E%84struct)
        - [Class与Struct的区别](#class%E4%B8%8Estruct%E7%9A%84%E5%8C%BA%E5%88%AB)
        - [修饰符（Modifier）](#%E4%BF%AE%E9%A5%B0%E7%AC%A6modifier)
            - [可访问性修饰符（Access Modifier）](#%E5%8F%AF%E8%AE%BF%E9%97%AE%E6%80%A7%E4%BF%AE%E9%A5%B0%E7%AC%A6access-modifier)
            - [其他修饰符](#%E5%85%B6%E4%BB%96%E4%BF%AE%E9%A5%B0%E7%AC%A6)
        - [类型别名](#%E7%B1%BB%E5%9E%8B%E5%88%AB%E5%90%8D)
        - [隐式继承、Object类](#%E9%9A%90%E5%BC%8F%E7%BB%A7%E6%89%BFobject%E7%B1%BB)
        - [值类型 vs 引用类型](#%E5%80%BC%E7%B1%BB%E5%9E%8B-vs-%E5%BC%95%E7%94%A8%E7%B1%BB%E5%9E%8B)
        - [值类型（Value Type）](#%E5%80%BC%E7%B1%BB%E5%9E%8Bvalue-type)
            - [结构](#%E7%BB%93%E6%9E%84)
            - [装箱（Boxing）和拆箱（Unboxing）](#%E8%A3%85%E7%AE%B1boxing%E5%92%8C%E6%8B%86%E7%AE%B1unboxing)
            - [枚举（Enum）](#%E6%9E%9A%E4%B8%BEenum)
        - [引用类型（Reference Type）](#%E5%BC%95%E7%94%A8%E7%B1%BB%E5%9E%8Breference-type)
            - [数组（Array）](#%E6%95%B0%E7%BB%84array)
            - [类（Class）](#%E7%B1%BBclass)
                - [类的继承](#%E7%B1%BB%E7%9A%84%E7%BB%A7%E6%89%BF)
                - [嵌套类](#%E5%B5%8C%E5%A5%97%E7%B1%BB)
        - [方法（Method）](#%E6%96%B9%E6%B3%95method)
            - [方法的参数](#%E6%96%B9%E6%B3%95%E7%9A%84%E5%8F%82%E6%95%B0)
                - [out和ref关键词](#out%E5%92%8Cref%E5%85%B3%E9%94%AE%E8%AF%8D)
                - [参数默认值](#%E5%8F%82%E6%95%B0%E9%BB%98%E8%AE%A4%E5%80%BC)
                - [可变参数](#%E5%8F%AF%E5%8F%98%E5%8F%82%E6%95%B0)
            - [构造器（Constructor）、终结器（Finalizer）](#%E6%9E%84%E9%80%A0%E5%99%A8constructor%E7%BB%88%E7%BB%93%E5%99%A8finalizer)
                - [静态构造器（Static Constructor）](#%E9%9D%99%E6%80%81%E6%9E%84%E9%80%A0%E5%99%A8static-constructor)
                - [构造器串联](#%E6%9E%84%E9%80%A0%E5%99%A8%E4%B8%B2%E8%81%94)
                - [终结器（Finalizer）](#%E7%BB%88%E7%BB%93%E5%99%A8finalizer)
            - [多态（Polymorphism）](#%E5%A4%9A%E6%80%81polymorphism)
        - [属性（Property）](#%E5%B1%9E%E6%80%A7property)
    - [接口（Interface）](#%E6%8E%A5%E5%8F%A3interface)
        - [可释放接口（IDisposable）](#%E5%8F%AF%E9%87%8A%E6%94%BE%E6%8E%A5%E5%8F%A3idisposable)
            - [using自动释放语句](#using%E8%87%AA%E5%8A%A8%E9%87%8A%E6%94%BE%E8%AF%AD%E5%8F%A5)
            - [IDisposable释放模式](#idisposable%E9%87%8A%E6%94%BE%E6%A8%A1%E5%BC%8F)
        - [枚举器接口（IEnumerator） 和 可枚举接口（IEnumerable）](#%E6%9E%9A%E4%B8%BE%E5%99%A8%E6%8E%A5%E5%8F%A3ienumerator-%E5%92%8C-%E5%8F%AF%E6%9E%9A%E4%B8%BE%E6%8E%A5%E5%8F%A3ienumerable)
    - [委托（Delegate）](#%E5%A7%94%E6%89%98delegate)
        - [多播委托（Multicast Delegate）](#%E5%A4%9A%E6%92%AD%E5%A7%94%E6%89%98multicast-delegate)
    - [事件（Event）](#%E4%BA%8B%E4%BB%B6event)
    - [运算符（Operator）](#%E8%BF%90%E7%AE%97%E7%AC%A6operator)
        - [特色运算符](#%E7%89%B9%E8%89%B2%E8%BF%90%E7%AE%97%E7%AC%A6)
            - [@符号](#%E7%AC%A6%E5%8F%B7)
            - [default运算符](#default%E8%BF%90%E7%AE%97%E7%AC%A6)
            - [null判断运算符](#null%E5%88%A4%E6%96%AD%E8%BF%90%E7%AE%97%E7%AC%A6)
        - [运算符的特色语法](#%E8%BF%90%E7%AE%97%E7%AC%A6%E7%9A%84%E7%89%B9%E8%89%B2%E8%AF%AD%E6%B3%95)
            - [索引器（Indexer）](#%E7%B4%A2%E5%BC%95%E5%99%A8indexer)
            - [运算符重载（Operator Overloading）](#%E8%BF%90%E7%AE%97%E7%AC%A6%E9%87%8D%E8%BD%BDoperator-overloading)
                - [string的==](#string%E7%9A%84)
                - [DateTime的+、-、>、<、>=、<=](#datetime%E7%9A%84-)
            - [自定义类型转换（User-Defined Conversion Operator）](#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2user-defined-conversion-operator)
    - [语句（Statement）](#%E8%AF%AD%E5%8F%A5statement)
        - [lock](#lock)
        - [说明注释（文档性注释，Documentation Comment）](#%E8%AF%B4%E6%98%8E%E6%B3%A8%E9%87%8A%E6%96%87%E6%A1%A3%E6%80%A7%E6%B3%A8%E9%87%8Adocumentation-comment)
        - [预处理指令（Preprocessor Directive）](#%E9%A2%84%E5%A4%84%E7%90%86%E6%8C%87%E4%BB%A4preprocessor-directive)
            - [#define和#if](#define%E5%92%8Cif)
            - [#region](#region)
    - [特性（Attribute）](#%E7%89%B9%E6%80%A7attribute)
        - [显式指定特性的目标](#%E6%98%BE%E5%BC%8F%E6%8C%87%E5%AE%9A%E7%89%B9%E6%80%A7%E7%9A%84%E7%9B%AE%E6%A0%87)
        - [特性中的@符号](#%E7%89%B9%E6%80%A7%E4%B8%AD%E7%9A%84%E7%AC%A6%E5%8F%B7)
    - [反射（Reflection）](#%E5%8F%8D%E5%B0%84reflection)
        - [Type类](#type%E7%B1%BB)
        - [is运算符](#is%E8%BF%90%E7%AE%97%E7%AC%A6)
        - [as运算符](#as%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [unsafe上下文](#unsafe%E4%B8%8A%E4%B8%8B%E6%96%87)
- [C# 2.0 —— 追赶 + 创新](#c-20--%E8%BF%BD%E8%B5%B6--%E5%88%9B%E6%96%B0)
    - [泛型（Generic）](#%E6%B3%9B%E5%9E%8Bgeneric)
        - [泛型约束](#%E6%B3%9B%E5%9E%8B%E7%BA%A6%E6%9D%9F)
        - [泛型方法的泛型类型的自动推断](#%E6%B3%9B%E5%9E%8B%E6%96%B9%E6%B3%95%E7%9A%84%E6%B3%9B%E5%9E%8B%E7%B1%BB%E5%9E%8B%E7%9A%84%E8%87%AA%E5%8A%A8%E6%8E%A8%E6%96%AD)
    - [分部类型（Partial Type）](#%E5%88%86%E9%83%A8%E7%B1%BB%E5%9E%8Bpartial-type)
    - [匿名方法（Anonymous Method）](#%E5%8C%BF%E5%90%8D%E6%96%B9%E6%B3%95anonymous-method)
        - [强类型委托（Strongly Typed Delegate）](#%E5%BC%BA%E7%B1%BB%E5%9E%8B%E5%A7%94%E6%89%98strongly-typed-delegate)
    - [可null值类型（Nullable\<T>）](#%E5%8F%AFnull%E5%80%BC%E7%B1%BB%E5%9E%8Bnullable%5Ct)
        - [可null值类型的类型判断](#%E5%8F%AFnull%E5%80%BC%E7%B1%BB%E5%9E%8B%E7%9A%84%E7%B1%BB%E5%9E%8B%E5%88%A4%E6%96%AD)
    - [迭代器（Iterator）](#%E8%BF%AD%E4%BB%A3%E5%99%A8iterator)
    - [C# 2.0的其他改进](#c-20%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
- [C# 3.0 —— 分道扬镳、放飞自我、跨时代创新](#c-30--%E5%88%86%E9%81%93%E6%89%AC%E9%95%B3%E6%94%BE%E9%A3%9E%E8%87%AA%E6%88%91%E8%B7%A8%E6%97%B6%E4%BB%A3%E5%88%9B%E6%96%B0)
    - [自动属性（Auto-Implemented Property）](#%E8%87%AA%E5%8A%A8%E5%B1%9E%E6%80%A7auto-implemented-property)
    - [隐式类型（Implicitly Typed）](#%E9%9A%90%E5%BC%8F%E7%B1%BB%E5%9E%8Bimplicitly-typed)
    - [初始化器（Initailizer）](#%E5%88%9D%E5%A7%8B%E5%8C%96%E5%99%A8initailizer)
    - [匿名类型（Anonymous Type）](#%E5%8C%BF%E5%90%8D%E7%B1%BB%E5%9E%8Banonymous-type)
        - [匿名类型的属性名称推断](#%E5%8C%BF%E5%90%8D%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%B1%9E%E6%80%A7%E5%90%8D%E7%A7%B0%E6%8E%A8%E6%96%AD)
    - [Lambda表达式](#lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [分部方法（Partial Method）](#%E5%88%86%E9%83%A8%E6%96%B9%E6%B3%95partial-method)
    - [扩展方法（Extension Method）](#%E6%89%A9%E5%B1%95%E6%96%B9%E6%B3%95extension-method)
    - [表达式树（Expression Tree）](#%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%A0%91expression-tree)
        - [生成、编译和执行表达式树](#%E7%94%9F%E6%88%90%E7%BC%96%E8%AF%91%E5%92%8C%E6%89%A7%E8%A1%8C%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%A0%91)
        - [Expression\<TDelegate>和代码分析](#expression%5Ctdelegate%E5%92%8C%E4%BB%A3%E7%A0%81%E5%88%86%E6%9E%90)
        - [生成表达式树的一个情景化的例子](#%E7%94%9F%E6%88%90%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%A0%91%E7%9A%84%E4%B8%80%E4%B8%AA%E6%83%85%E6%99%AF%E5%8C%96%E7%9A%84%E4%BE%8B%E5%AD%90)
    - [LINQ](#linq)
        - [查询表达式（Query Expression）](#%E6%9F%A5%E8%AF%A2%E8%A1%A8%E8%BE%BE%E5%BC%8Fquery-expression)
        - [查询扩展方法（Query Extension Method）](#%E6%9F%A5%E8%AF%A2%E6%89%A9%E5%B1%95%E6%96%B9%E6%B3%95query-extension-method)
            - [针对IEnumerable\<T>的查询扩展方法](#%E9%92%88%E5%AF%B9ienumerable%5Ct%E7%9A%84%E6%9F%A5%E8%AF%A2%E6%89%A9%E5%B1%95%E6%96%B9%E6%B3%95)
            - [针对IQuerayable\<T>的查询扩展方法](#%E9%92%88%E5%AF%B9iquerayable%5Ct%E7%9A%84%E6%9F%A5%E8%AF%A2%E6%89%A9%E5%B1%95%E6%96%B9%E6%B3%95)
- [C# 4.0 —— 独立发展](#c-40--%E7%8B%AC%E7%AB%8B%E5%8F%91%E5%B1%95)
    - [动态类型（Dynamic Type）](#%E5%8A%A8%E6%80%81%E7%B1%BB%E5%9E%8Bdynamic-type)
    - [命名参数（Named Argument）](#%E5%91%BD%E5%90%8D%E5%8F%82%E6%95%B0named-argument)
        - [可选参数（Optional Argument）](#%E5%8F%AF%E9%80%89%E5%8F%82%E6%95%B0optional-argument)
    - [协变（Covariant）、逆变（Contravariant）](#%E5%8D%8F%E5%8F%98covariant%E9%80%86%E5%8F%98contravariant)
- [C# 5.0 —— 字数越少，事儿就越大](#c-50--%E5%AD%97%E6%95%B0%E8%B6%8A%E5%B0%91%E4%BA%8B%E5%84%BF%E5%B0%B1%E8%B6%8A%E5%A4%A7)
    - [调用者信息（Caller Information）](#%E8%B0%83%E7%94%A8%E8%80%85%E4%BF%A1%E6%81%AFcaller-information)
    - [异步编程（Asynchronous Programming）](#%E5%BC%82%E6%AD%A5%E7%BC%96%E7%A8%8Basynchronous-programming)
        - [为什么要用异步](#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E7%94%A8%E5%BC%82%E6%AD%A5)
        - [如何理解异步和线程的关系](#%E5%A6%82%E4%BD%95%E7%90%86%E8%A7%A3%E5%BC%82%E6%AD%A5%E5%92%8C%E7%BA%BF%E7%A8%8B%E7%9A%84%E5%85%B3%E7%B3%BB)
        - [Task、Task\<TResult>和异步方法](#tasktask%5Ctresult%E5%92%8C%E5%BC%82%E6%AD%A5%E6%96%B9%E6%B3%95)
        - [使用新线程启动任务](#%E4%BD%BF%E7%94%A8%E6%96%B0%E7%BA%BF%E7%A8%8B%E5%90%AF%E5%8A%A8%E4%BB%BB%E5%8A%A1)
        - [等待多个任务](#%E7%AD%89%E5%BE%85%E5%A4%9A%E4%B8%AA%E4%BB%BB%E5%8A%A1)
        - [异步的优势](#%E5%BC%82%E6%AD%A5%E7%9A%84%E4%BC%98%E5%8A%BF)
        - [异步的死锁（deadlock）问题](#%E5%BC%82%E6%AD%A5%E7%9A%84%E6%AD%BB%E9%94%81deadlock%E9%97%AE%E9%A2%98)
        - [异步的Java对照](#%E5%BC%82%E6%AD%A5%E7%9A%84java%E5%AF%B9%E7%85%A7)
- [C# 6.0 —— 语法糖机枪](#c-60--%E8%AF%AD%E6%B3%95%E7%B3%96%E6%9C%BA%E6%9E%AA)
    - [异常筛选器](#%E5%BC%82%E5%B8%B8%E7%AD%9B%E9%80%89%E5%99%A8)
    - [属性初始化表达式](#%E5%B1%9E%E6%80%A7%E5%88%9D%E5%A7%8B%E5%8C%96%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [null传播运算符](#null%E4%BC%A0%E6%92%AD%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [字符串内插（String Interpolation）](#%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%86%85%E6%8F%92string-interpolation)
    - [nameof运算符](#nameof%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [索引初始化表达式](#%E7%B4%A2%E5%BC%95%E5%88%9D%E5%A7%8B%E5%8C%96%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [C# 6.0的其他改进](#c-60%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
- [C# 7.0—— Python是个好东西](#c-70-python%E6%98%AF%E4%B8%AA%E5%A5%BD%E4%B8%9C%E8%A5%BF)
    - [out变量声明](#out%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E)
    - [元组（Tuple Type）](#%E5%85%83%E7%BB%84tuple-type)
        - [元组的赋值](#%E5%85%83%E7%BB%84%E7%9A%84%E8%B5%8B%E5%80%BC)
        - [元组的解构（Deconstruction）](#%E5%85%83%E7%BB%84%E7%9A%84%E8%A7%A3%E6%9E%84deconstruction)
        - [自定义类的解构方法](#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%B1%BB%E7%9A%84%E8%A7%A3%E6%9E%84%E6%96%B9%E6%B3%95)
        - [何时使用元组](#%E4%BD%95%E6%97%B6%E4%BD%BF%E7%94%A8%E5%85%83%E7%BB%84)
    - [C# 7.0的模式匹配（Pattern Matching）](#c-70%E7%9A%84%E6%A8%A1%E5%BC%8F%E5%8C%B9%E9%85%8Dpattern-matching)
        - [常量模式](#%E5%B8%B8%E9%87%8F%E6%A8%A1%E5%BC%8F)
        - [声明模式](#%E5%A3%B0%E6%98%8E%E6%A8%A1%E5%BC%8F)
        - [var模式](#var%E6%A8%A1%E5%BC%8F)
        - [case的when子句](#case%E7%9A%84when%E5%AD%90%E5%8F%A5)
    - [本地函数（Local Function）](#%E6%9C%AC%E5%9C%B0%E5%87%BD%E6%95%B0local-function)
    - [表达式主体（Expression-Bodied Member）](#%E8%A1%A8%E8%BE%BE%E5%BC%8F%E4%B8%BB%E4%BD%93expression-bodied-member)
    - [ref返回值、ref局部变量](#ref%E8%BF%94%E5%9B%9E%E5%80%BCref%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F)
    - [弃元（Discard）](#%E5%BC%83%E5%85%83discard)
    - [throw表达式](#throw%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [更多的可等待类型](#%E6%9B%B4%E5%A4%9A%E7%9A%84%E5%8F%AF%E7%AD%89%E5%BE%85%E7%B1%BB%E5%9E%8B)
        - [异步方法构建器](#%E5%BC%82%E6%AD%A5%E6%96%B9%E6%B3%95%E6%9E%84%E5%BB%BA%E5%99%A8)
    - [C# 7.0的其他改进](#c-70%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
- [C# 7.1、7.2、7.3 —— 小碎步](#c-717273--%E5%B0%8F%E7%A2%8E%E6%AD%A5)
    - [C# 7.1的改进](#c-71%E7%9A%84%E6%94%B9%E8%BF%9B)
    - [C# 7.2的改进](#c-72%E7%9A%84%E6%94%B9%E8%BF%9B)
        - [in参数、readonly struct、ref struct、ref readonly返回值、ref readonly struct](#in%E5%8F%82%E6%95%B0readonly-structref-structref-readonly%E8%BF%94%E5%9B%9E%E5%80%BCref-readonly-struct)
        - [Span\<T>、ReadOnlySpan\<T>](#span%5Ctreadonlyspan%5Ct)
        - [新增了几种泛型约束类型](#%E6%96%B0%E5%A2%9E%E4%BA%86%E5%87%A0%E7%A7%8D%E6%B3%9B%E5%9E%8B%E7%BA%A6%E6%9D%9F%E7%B1%BB%E5%9E%8B)
        - [命名参数不必跟在尾部](#%E5%91%BD%E5%90%8D%E5%8F%82%E6%95%B0%E4%B8%8D%E5%BF%85%E8%B7%9F%E5%9C%A8%E5%B0%BE%E9%83%A8)
        - [C# 7.2的其他改进](#c-72%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
    - [C# 7.3的改进](#c-73%E7%9A%84%E6%94%B9%E8%BF%9B)
        - [元组的==和!=支持](#%E5%85%83%E7%BB%84%E7%9A%84%E5%92%8C%E6%94%AF%E6%8C%81)
        - [针对out变量声明的改进](#%E9%92%88%E5%AF%B9out%E5%8F%98%E9%87%8F%E5%A3%B0%E6%98%8E%E7%9A%84%E6%94%B9%E8%BF%9B)
        - [stackalloc初始化器](#stackalloc%E5%88%9D%E5%A7%8B%E5%8C%96%E5%99%A8)
        - [特性可作用于自动属性的字段](#%E7%89%B9%E6%80%A7%E5%8F%AF%E4%BD%9C%E7%94%A8%E4%BA%8E%E8%87%AA%E5%8A%A8%E5%B1%9E%E6%80%A7%E7%9A%84%E5%AD%97%E6%AE%B5)
        - [含in参数的方法的改进](#%E5%90%ABin%E5%8F%82%E6%95%B0%E7%9A%84%E6%96%B9%E6%B3%95%E7%9A%84%E6%94%B9%E8%BF%9B)
        - [C# 7.3的其他改进](#c-73%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
- [C# 8.0 —— 当语法升级成为日常](#c-80--%E5%BD%93%E8%AF%AD%E6%B3%95%E5%8D%87%E7%BA%A7%E6%88%90%E4%B8%BA%E6%97%A5%E5%B8%B8)
    - [readonly成员](#readonly%E6%88%90%E5%91%98)
    - [接口的默认实现](#%E6%8E%A5%E5%8F%A3%E7%9A%84%E9%BB%98%E8%AE%A4%E5%AE%9E%E7%8E%B0)
    - [C# 8.0的模式匹配](#c-80%E7%9A%84%E6%A8%A1%E5%BC%8F%E5%8C%B9%E9%85%8D)
        - [switch表达式](#switch%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [弃元模式](#%E5%BC%83%E5%85%83%E6%A8%A1%E5%BC%8F)
        - [属性模式](#%E5%B1%9E%E6%80%A7%E6%A8%A1%E5%BC%8F)
        - [元组模式](#%E5%85%83%E7%BB%84%E6%A8%A1%E5%BC%8F)
        - [位置模式](#%E4%BD%8D%E7%BD%AE%E6%A8%A1%E5%BC%8F)
    - [using声明](#using%E5%A3%B0%E6%98%8E)
    - [可null引用类型](#%E5%8F%AFnull%E5%BC%95%E7%94%A8%E7%B1%BB%E5%9E%8B)
    - [异步迭代器](#%E5%BC%82%E6%AD%A5%E8%BF%AD%E4%BB%A3%E5%99%A8)
    - [异步可释放](#%E5%BC%82%E6%AD%A5%E5%8F%AF%E9%87%8A%E6%94%BE)
    - [索引（Index）、范围（Range）](#%E7%B4%A2%E5%BC%95index%E8%8C%83%E5%9B%B4range)
        - [索引定位](#%E7%B4%A2%E5%BC%95%E5%AE%9A%E4%BD%8D)
        - [范围切片](#%E8%8C%83%E5%9B%B4%E5%88%87%E7%89%87)
        - [自定义类型支持索引和范围](#%E8%87%AA%E5%AE%9A%E4%B9%89%E7%B1%BB%E5%9E%8B%E6%94%AF%E6%8C%81%E7%B4%A2%E5%BC%95%E5%92%8C%E8%8C%83%E5%9B%B4)
            - [显式支持Index和Range](#%E6%98%BE%E5%BC%8F%E6%94%AF%E6%8C%81index%E5%92%8Crange)
            - [隐式支持Index和Range](#%E9%9A%90%E5%BC%8F%E6%94%AF%E6%8C%81index%E5%92%8Crange)
    - [null合并赋值运算符](#null%E5%90%88%E5%B9%B6%E8%B5%8B%E5%80%BC%E8%BF%90%E7%AE%97%E7%AC%A6)
    - [C# 8.0的其他改进](#c-80%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
- [C# 9.0 —— 新的征程](#c-90--%E6%96%B0%E7%9A%84%E5%BE%81%E7%A8%8B)
    - [init访问器](#init%E8%AE%BF%E9%97%AE%E5%99%A8)
    - [记录（Record）](#%E8%AE%B0%E5%BD%95record)
        - [记录的继承](#%E8%AE%B0%E5%BD%95%E7%9A%84%E7%BB%A7%E6%89%BF)
        - [记录与struct比较](#%E8%AE%B0%E5%BD%95%E4%B8%8Estruct%E6%AF%94%E8%BE%83)
        - [with表达式](#with%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [顶级语句](#%E9%A1%B6%E7%BA%A7%E8%AF%AD%E5%8F%A5)
    - [C# 9.0的模式匹配](#c-90%E7%9A%84%E6%A8%A1%E5%BC%8F%E5%8C%B9%E9%85%8D)
        - [类型模式](#%E7%B1%BB%E5%9E%8B%E6%A8%A1%E5%BC%8F)
        - [关系模式](#%E5%85%B3%E7%B3%BB%E6%A8%A1%E5%BC%8F)
        - [逻辑模式](#%E9%80%BB%E8%BE%91%E6%A8%A1%E5%BC%8F)
        - [模式匹配的总结](#%E6%A8%A1%E5%BC%8F%E5%8C%B9%E9%85%8D%E7%9A%84%E6%80%BB%E7%BB%93)
    - [目标类型new表达式](#%E7%9B%AE%E6%A0%87%E7%B1%BB%E5%9E%8Bnew%E8%A1%A8%E8%BE%BE%E5%BC%8F)
    - [协变返回类型](#%E5%8D%8F%E5%8F%98%E8%BF%94%E5%9B%9E%E7%B1%BB%E5%9E%8B)
    - [Lambda的弃元参数](#lambda%E7%9A%84%E5%BC%83%E5%85%83%E5%8F%82%E6%95%B0)
    - [模块的初始化方法](#%E6%A8%A1%E5%9D%97%E7%9A%84%E5%88%9D%E5%A7%8B%E5%8C%96%E6%96%B9%E6%B3%95)
    - [条件表达式的目标类型优化](#%E6%9D%A1%E4%BB%B6%E8%A1%A8%E8%BE%BE%E5%BC%8F%E7%9A%84%E7%9B%AE%E6%A0%87%E7%B1%BB%E5%9E%8B%E4%BC%98%E5%8C%96)
    - [C# 9.0的其他改进](#c-90%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
- [C# 10.0 —— 学无止尽](#c-100--%E5%AD%A6%E6%97%A0%E6%AD%A2%E5%B0%BD)
    - [记录结构（Record Struct）](#%E8%AE%B0%E5%BD%95%E7%BB%93%E6%9E%84record-struct)
    - [属性模式的改进](#%E5%B1%9E%E6%80%A7%E6%A8%A1%E5%BC%8F%E7%9A%84%E6%94%B9%E8%BF%9B)
    - [Lambda表达式的改进](#lambda%E8%A1%A8%E8%BE%BE%E5%BC%8F%E7%9A%84%E6%94%B9%E8%BF%9B)
    - [const可以使用字符串内插](#const%E5%8F%AF%E4%BB%A5%E4%BD%BF%E7%94%A8%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%86%85%E6%8F%92)
    - [元组解构声明的优化](#%E5%85%83%E7%BB%84%E8%A7%A3%E6%9E%84%E5%A3%B0%E6%98%8E%E7%9A%84%E4%BC%98%E5%8C%96)
    - [调用者信息改进](#%E8%B0%83%E7%94%A8%E8%80%85%E4%BF%A1%E6%81%AF%E6%94%B9%E8%BF%9B)
    - [C# 10.0的其他改进](#c-100%E7%9A%84%E5%85%B6%E4%BB%96%E6%94%B9%E8%BF%9B)
- [相顾回眸](#%E7%9B%B8%E9%A1%BE%E5%9B%9E%E7%9C%B8)
    - [有什么是Java有但是C#没有的](#%E6%9C%89%E4%BB%80%E4%B9%88%E6%98%AFjava%E6%9C%89%E4%BD%86%E6%98%AFc%E6%B2%A1%E6%9C%89%E7%9A%84)
    - [C# Style](#c-style)
        - [怎样看起来像一个原生的CShaper](#%E6%80%8E%E6%A0%B7%E7%9C%8B%E8%B5%B7%E6%9D%A5%E5%83%8F%E4%B8%80%E4%B8%AA%E5%8E%9F%E7%94%9F%E7%9A%84cshaper)
- [附录](#%E9%99%84%E5%BD%95)
    - [参考资料](#%E5%8F%82%E8%80%83%E8%B5%84%E6%96%99)
    - [作者按](#%E4%BD%9C%E8%80%85%E6%8C%89)

<!-- /TOC -->

# 正文之前

## 基本概念

这里列出C#和\.Net的一些基本概念，供参考：

### C# ###

- C#是一门语言，他的语法类似C++和Java。
- C#是完全面向对象的语言，程序入口点也在类中（Main方法）。
- C#用于编写\.Net程序，但不是唯一的选择。除了C#之外，还有F#、VB\.Net等等语言，也可用于编写\.Net程序。

### \.Net

下面是一些和\.Net有关的名词。（名词解释中出现的英文缩写，也会在列表中找到相关解释。）

- **\.Net**，是一套框架，它主要由CLR和FCL组成。因为\.Net程序不仅仅支持一种语言编写，所以下面的各条术语都有前缀Common。Common翻译为公共，体现的是跨语言、通用。
- **CLR**（公共运行时，Common Language Runtime），是CLI的具体实现，并且也是目前为止的唯一实现。它包含JIT编译器等组件。CLR有很多，包括\.NetFramework，\.NetCore，Mono\.Net，以及最新的\.Net等。

    > CLR相当于Java的JVM。CLR与JVM的最主要区别在于：CLR被设计为与语言无关，而JVM被设计为特定于Java。

- **CLI**（公共语言基础设施，Common Language Infrastructure），是微软公司向ECMA提交的一份语言和数据格式规范。包括CTS、CIL等。CLR实现了该规范。
- **CTS**（公共类型系统，Common Types System），定义了能够在CLR上运行的语言规范。它定义了通用的数据类型。
- **CIL**（公共中间语言，Common Intermediate Language，或简称IL），是一种中间代码，是\.NET框架的低阶人类可读语言，且与开发时所用的上层语言无关。上层的语言，如C#等，会在生成dll和exe时被编译器编译为CIL代码，而非直接编译为机器码。这种代码与底层硬件设施无关，可以由CLR中的JIT编译器翻译为机器语言执行。由于这样的设计，使得不同上层语言调用其他语言编写的库时，不会遇到障碍。

    > CIL对应Java的字节码。

- **JIT编译器**（即时编译，Just-In-Time Compilation），是CLR的重要组成部分。用于将CIL代码翻译成机器码。JIT编译器在运行时（Runtime）工作。在IL代码第一次被执行时，会按照具体的CPU类型、操作系统类型等将IL翻译成机器码并执行。JIT对同一段IL代码的编译只会执行一次，第二次以后执行便会直接使用机器码，不再执行编译过程，以优化效率。
- **托管代码**（Managed Code）和**非托管代码**（Unmanaged Code）：托管代码为可由编译器编译为CIL的代码。正常情况下我们编写的C#代码都是托管代码。调用其他非\.Net语言（如C++）编写的库，或使用unsafe上下文编写含指针操作的代码，属于非托管代码。托管代码是内存安全的，对已分配的内存空间由GC进行管理。
- **GC**（垃圾回收器，Garbage Collector），它通过对象引用计数器管理对象的引用情况，并在对象失去所有引用后执行自动的内存回收工作，因而不必像C++一样手动free掉分配的内存空间。GC是所有高级语言中非常重要的内存管理机制。
- **FCL**（框架类库，Framework Class Library），与CLR并列，是\.Net的重要促成部分。大家都明白，语言和语法只是一方面，真正要完成具体任务，离不开各种类库的帮助。而\.Net提供了大量官方的类库，功能强大，且覆盖极广。从前，CShaper有时倾向于选择官方类库而非第三方类库，很大程度上也是由于官方类库过于强大而培养出来的习惯，算是一种思维定式（俗称：微软大法好）。当然，随着\.Net本身的走向开放，CShaper们的心态现在也很开放了。因而github上C#的优秀开源项目也越来越多。FCL具体又可以划分为BCL和AppModel。
- **BCL**（基础类库，Basic Class Library），\.Net较为底层的类库，与应用类型无关。基础类库可用于各种类型的开发场景中。
- **AppModel**，是\.Net官方类库中，用于决定应用形态的框架性类库。包括 **WCF、WPF、WinForm、Webform、ASP\.NET MVC、ASP\.NET Core**等等等等。例如：WCF用于编写服务，并以各种方式（终结点）暴露服务（几乎已经淘汰）；WPF、Winform用于编写窗体应用；ASP\.NET系列用于编写Web应用等。

    > 可以类比Java的SpringBoot，SpringMVC等。不同点是\.Net的这部分库都是官方的，而非第三方提供。

- **Debug模式**和**Release模式**：在编译时可以选择Debug和Release模式。
    - Debug模式一般用于调试，这种模式会在生成的CIL中插入大量调试符号（Debugging Symbols）。Debug模式下生成的CIL代码依然具有较高可读性。它保留了源码中的代码所处类型、方法、行号等信息，并且可以准确的捕捉和定位异常。Debug模式不会对代码做编译器优化，也不会调整代码执行顺序。表现为程序完全按照书写内容执行。例如：给一个从未被使用过的临时变量赋值常量值，Debug模式的程序会照做。
    - Release模式，用于生产。是程序执行发布（Publish）操作时默认的模式。Release模式打出来的应用程序集文件（dll、exe）要比Debug模式小的多。Release模式会对代码做编译器优化，例如将数个简单赋值语句合并成一句等等。因而可能会丢失原始的代码行号等信息。在IDE中使用Release模式运行调试时，可能无法准确命中断点，也有可能无法准确捕获未被catch的异常。Release模式下，使用Reflector等工具进行反编译，会发现有些代码变得跟原始代码有差异，这包括但不限于本地变量名被抹除、语句顺序调整等。因而，调用第三方发行版包时，很难通过反编译进行包内方法的调试。
- **Module**(模块，或Managed Module，托管模块)。是编译后的一个代码单元，是Assembly的组成部分。一个模块主要包含元数据和IL代码。元数据主要是两部分组成：一部分是模块中所定义的所有类型描述、方法所在位置等信息；另一部分是所引用并且使用到的其他库中类型的描述，这部分信息使得JIT可以在运行时加载这些类库，而不用预先将所引用的库也编译进模块中。IL则是由JIT编译并执行的代码。注意：模块与命名空间之间没有必然连系。
- **Assembly**(应用程序集)，是\.Net程序的组成单元，也是版本控制的最小单元。它由一个或多个模块、资源定义文件（Manifest）、资源文件组组成。资源定义文件包含CLR版本信息、应用形态信息、程序入口点位置等。资源文件组可包含一堆被打包进Assembly的资源文件，甚至可以包含dll。Assembly一般被打包为独立的dll（类库）或者exe（含入口点的程序）文件。\.Net的程序正常情况下不会把不同的dll、exe打包成独立文件，一个完整功能的\.Net程序大都由多个exe和dll文件组成，他们通过引用关联起来。常见的例如：由一个exe文件作为入口点，在该exe中调用了其他的多个dll文件中的功能，它们共同组成了一个完整功能的\.Net程序。这里的每个exe或dll文件都是一个应用程序集。应用程序集是自描述的，因而只需要引用dll文件即可使用，不像C++等可能还需要\.def、\.h文件的配合，也不像Com组件那样需要配合注册表使用。应用程序集采用使用时加载的策略：代码中引用了某个dll，在Runtime实际使用该dll中的任何类或定义之前，应用程序集并不会被实际加载。应用程序集既支持在项目中**静态引用**，以便在编写时提供语法提示和执行编译器检查，并在打包时将被引用的应用程序集类型定义描述写进元数据内；也支持通过Assembly类在运行时**动态加载**，甚至可以从资源文件中加载。默认情况下，一个项目在编译时会生成一个仅包含一个模块的应用程序集，因而大部分时候项目、模块、应用程序集是一一对应的。但是，你仍然可以通过命令行工具将一个项目、甚至一个代码文件编译成一个模块，然后再使用工具将多个模块拼接在一起，打包成一个应用程序集文件。这样做时，你甚至可以用不同的语言来编写这些模块。注意：应用程序集与命名空间之间也没有必然连系。

    > 读者可以自行将Assembly和Module，与Java的多Module项目做下类比。

- **Nuget**：Nuget是\.Net的包管理工具。nuget.org也是支持第三方\.Net的包发布平台。Nuget很好的解决了版本控制的问题。因为类库的dll文件并不会跟随引用它的应用程序打包进exe，而是保持独立的dll，所以当你的解决方案中，一个项目引用了另一个项目，而这两个项目又都引用了同一个包，但是包的版本却不同时，Nuget可以根据一定的策略保证所引用的包版本最终一致，并在无法调和版本时在编译时便给出报错。添加Nuget的包可以直接通过IDE的Nuget包管理界面，或者通过开发命令行的Install-Package命令，也可以直接修改项目文件（一般为.xxxxproj格式，如C#项目为.csproj）。打包自己开发的程序为Nuget包，可以通过IDE直接进行操作；也可以遵循Nuget包结构构建目录，然后使用Nuget命令行工具、Nuget包管理工具进行打包。使用IDE的自动打包时，如果被打包的项目包含对解决方案内其他项目的引用，则打包成Nuget包后，会自动转换为对Nuget包的引用。

    > Nuget类似于Java的Maven。它们的主要差异：
    >
    > - Nuget并不区分开发仓库和发布仓库。Nuget包同一版本不支持重复推送，已下载过的包本地会有缓存。因而推到Nuget仓库的包，不便于使用同一个版本号不断更新。对于非稳定版包，一般使用版本号+后缀的形式推送。如：1.0-preview，1.2-rc3.1等。IDE中搜索时，可以过滤这些非稳定版本的包。
    > - 而Maven则区分Snapshot仓库和Release仓库。Maven的Snapshot仓库拥有更灵活的策略：同一个版本号的Maven包可以重复推送，而引用该Snapshot版本的包的代码，也会根据Maven仓库的推送，拉取最新的包，而不是使用本地缓存的之前拉取得包。这点上Maven要更为强大。

## \.Net和C#发展史

C#版本发布时间，及与\.Net的对应关系，如下表：

| C#版本 | \.NET版本 | 发布日期 |
| --- | --- | --- |
| C# 1.0 | \.NET Framework 1.0 | 2002年2月13日 |
| C# 1.1 | \.NET Framework 1.1 | 2003年4月24日 |
| C# 2.0 | \.NET Framework 2.0 | 2005年11月7日 |
| C# 3.0 | \.NET Framework 3.0 | 2007年11月6日 |
| | \.NET Framework 3.5 | 2007年11月19日 |
| C# 4.0 | \.NET Framework 4.0 | 2010年4月12日 |
| C# 5.0 | \.NET Framework 4.5 | 2012年8月15日 |
| C# 6.0 | \.NET Framework 4.6 | 2015年7月20日 |
| | \.NET Core 1.0 | 2016年6月27日 |
| C# 7.0 | \.NET Framework 4.6.2 | 2016年8月2日 |
| C# 7.1 | \.NET Framework 4.7 | 2017年4月5日 |
| | \.NET Core 2.0 | 2016年8月14日 |
| C# 7.2 | \.NET Framework 4.7.1 | 2017年10月17日 |
| C# 7.3 | \.NET Framework 4.7.2 | 2018年4月30日 |
| | \.NET Core 2.1 | 2018年5月30日|
| | \.NET Core 2.2 | 2018年12月4日|
| C# 8.0 | \.NET Framework 4.8 | 2019年4月18日 |
| | \.NET Core 3.0 | 2019年9月23日 |
| | \.NET Core 3.1 | 2019年12月3日 |
| C# 9.0 | \.NET 5 | 2020年9月4日 |
| C# 10.0 | \.NET 6 | 2021年11月9日 |

C#和\.Net发展，**关键节点**简要介绍：

1. **J++**

    - 1995年，由于互联网兴起。Sun公司推出的Java大火。因为其跨平台特点，微软感受到危机。为了将用户留在Windows，微软启动了J++项目。其含义为Java增强版，旨在优化Java开发体验和执行性能。
    - 1997年，Visual Studio 97发布，首次包含J++。
    - 1998年，大名鼎鼎的Visual Studio 6.0发布（对，就是那个曾经大学必学的VS6）。此时的J++，不仅性能比Sun的Java更高，还支持了WindowsAPI。其易用性迅速抢占了Java的市场，成为业内公认的优秀Java编译器。因其只能在Windows下用，也帮助微软占了操作系统市场。
    - 同年，Sun忍无可忍，将微软告上法庭。
    - 官司一直打到2001年。法院最终判定微软未能遵循Java规范，Sun公司胜诉。同年，Sun和微软达成和解：微软停止J++项目，Sun不再追究经济损失。

2. **\.NetFramework 1.0**

    - 微软之所以甘心放弃J++项目，也是因其早就启动了新的项目，用于替代Java。这便是\.Net。同时，参考了Java和C++的语法，设计了全新的语言：C#。
    - 2002年，\.NetFramework1.0跟随Visual Studio \.NET 2002一同发布。此时的\.Net支持两种语言:C#和VB\.Net。支持VB\.Net也是为了让既有的VB开发人员可以快速上手。从此，\.Net时代正式开启了。
    - 有个玩笑说：C#的含义，有可能是C++++。从本质上讲，Java和C#都是C++语法系统的。所以，这种说法有可能是真的。😊

3. **C#3.0** 和 **\.NetFramework3.5**

    - C#3.0之所以特殊，是因为3.0之前C#主要是模仿Java。而3.0开始，C#正式与老师分道扬镳，开始放飞自我了。
    - 2007年C#3.0跟随Visual Sudio 2008一同发布。这个版本带来了诸多重大更新。它引入了Lambda表达式、表达式树、扩展方法、隐式类型变量、初始化器（Initializer）等等重要机制。同时还引入了LINQ这个重磅炸弹 —— 它被视作CShaper的快乐之源。
    - 到\.NetFramework3.5发布，\.Net的第一个高度成熟的版本形成了。\.Net3.5帮助微软占据了大量市场。

4. **C#5.0**

    - 2010年\.NetFramework4.0（对应C#4.0）正式发布。值得注意的是，\.NetFramework3.5和之前的版本一直做了向下兼容。3.5兼容从2.0到3.5的所有版本。但是到了\.NetFramework4，这种兼容被打破了。在这之后，3.x和4.x成为两个互不兼容、相互独立的CLR版本。因而，此后很长一段时间内，你的机器上可能要装同时装3.x和4.x两个版本的\.NetFramework，才能应对各种\.Net应用。
    - 到了C#5.0发布时，正式了引入异步编程。这又是一项跨时代的技术。对js后来的发展也产生了深远的影响。而C#5.0对应的\.NetFramework4.5，也成为了继3.5之后第二个高度成熟版本。

5. **\.Net Standard**

    - 由于Linux在服务领域的一骑绝尘，\.Net不能跨平台的弊端逐渐显现出来。终于，有人看不惯\.Net的不跨平台了。Mono项目不依赖\.NetFramework的源码（也没法依赖，\.NetFramework并不开源），重新实现了\.Net CLR，即跨平台的Mono\.Net。再到后来的Unity3D、Xamarin，\.Net的第三方实现开始占领市场。
    - 同时，微软自家也在面临多版本问题，首先有互不兼容的3.5和4.5；其次，他们还为不同的系统定制了不同的\.Net。比如，他们为移动设备和XBOX定制了阉割版\.Net Portable。
    - 经过了漫长的封闭、服务器领域市场的不断衰退和Windows Phone的惨败之后。2014年，微软终于迎来了一位靠谱的CEO。他意识到了开放的重要性，开始积极拥抱开源和跨平台。微软开始积极筹备自家的跨平台\.Net。当时还仅仅考虑网站开发，计划命名为Asp\.Net MVC 6。后来随着项目的进行，微软改变策略，决心做成一个全面、通用的、跨平台的\.Net，并取命\.Net Core。
        - 提到这位CEO，不得不吐槽两句。由于他是个印度裔（硅谷已经被印度CEO裔占领了），导致他上任后微软印度裔的开发人员数量大幅上升。因而，我们现在经常能在微软系的软件中，感受到各式各样满满咖喱风味的BUG。
    - \.Net CLR的混乱局面由此便形成了。各式各样的CLR，互不兼容。如果想要重用你的代码，只能针对目标版本重新编译。而且，还需要考虑各版本的框架结构和类库、语法支持度问题，难免要针对不同CLR版本做出不同程度的代码修改。在当时，给人印象深刻的一点是：你下载的Nuget包里的lib目录下，会有许多并列的子目录，包括net30、net35、net45、net46、net461、netcoreapp2.2等等等等。每个目录均由相似的文件构成：都包含类库的dll和xml等文件。不同的是每个dll是面向不同的目标CLR编译的。而你自己写的类库，很多时候也不得不编译成各种不同的目标框架版本，以适应不同目标版本CLR的程序。
    - 因此，微软提出了\.Net Standard。这是一套标准，而非CLR的实现。其目的是将一众\.Net框架统一起来，提高他们的一致性，从而可以共享代码。\.Net Standard其实是一套API规范，目标代码的运行需要由各个\.Net CLR来具体实现。因而，\.Net Standard只能用来编写通用类库，而不能编写有入口的完整程序。使用\.Net Standard编译的类库，可以跑在支持\.Net Standard的任意\.Net实现上，只要CLR支持的\.Net Standard版本不低于你的库的目标\.Net Standard版本。从而实现了Mono\.Net，\.NetFramework，\.Net Core等不同版本的\.Net之间可以共享代码。有趣的是，\.Net Standard生成的dll打包进Nuget，也要放到lib目录下的netstandardx.x的子目录里。针对多种目标CLR和针对Standard的dll还是可以并存。
    - \.Net Standard是微软的无奈之举。这个尴尬的境地，到\.Net5后被使用新的方式彻底破解。

6. **\.Net Core**
    - 2016年，\.Net的官方跨平台版本终于来了。\.Net Core 1.0正式发布。它不仅跨平台，还是开源的。最早开源于微软自家的开放代码平台CodePlex，后来迁移至微软自家的开放代码平台GitHub🙂。\.Net Core的发布标志着微软终于结束了封闭，彻底走向了开放。
    - \.Net Core的版本升级策略也发生了转变。跟诸多常见开源项目一样，虽然它仍然会尽量做到向下兼容，但是这已经不再那么重要了。每当新的大版本发布，可能都会从应用程序框架结构上做出些调整。因此，为了升级到新版本，开发者可能需要少量修改代码，而不像之前\.NetFramework时代那样仅仅需要改一下版本号。不过对于具体的升级改动，官方也会在文档中给出指南。
    - 随着框架不断完善，2019年底，\.Net Core 3.1发布。\.Net Core迎来了第一个LTS（Long Term Support，长期支持）版本。
    - \.Net的后续发布计划也在此刻确定了。\.Net Core 3.1的下一个版本不会是\.Net Core 4.0，而是决定后续将\.NetFramework和\.NetCore合并，不再区分多个版本，并统一命名为\.Net。

7. **\.Net**
    - \.Net的发布时间表（Time Schedule）确定为：从2020年开始，每年的年末会发布一个大版本的\.Net。并且，偶数序号\.Net将获得LTS。
    - 因为合并，以后不会再有\.Net Framework和\.Net Core之分，所以新的\.Net CLR更名为\.Net。合并后的第一个\.Net，实际上就是\.Net Core 4.0。但为了避免跟\.NetFramework 4混淆，跳过了4.0的命名，直接使用了\.Net5。
    - \.Net6是\.Net合并成单一框架后的第一个LTS版本。也是刚刚发布没多久的版本。它与Visual Studio 2022一同发布。

曾经因为封闭，微软尝到了甜头，封闭的开发、运行环境和封闭的操作系统互相促进，奠定了微软的市场霸权。

但是，同样也是因为封闭，在开源社区大行其道的201x年代，Linux逐渐取代Windows成为服务器首选系统。\.Net因为不具备跨平台的能力，也错失先机，被Java抢占了大量市场份额。时至今日，得益于大量优秀的开发者的参与贡献、大量优质开源项目的支撑，如今Java生态要好于\.Net。这在国内更甚，互联网大厂中Java占有绝对统治地位。

虽然\.Net的开放来的迟了些，但是晚到的总胜过没有。随着优质的开源项目的不断加入，相信\.Net还是未来可期的。尤其是在LoT相关领域，在当前还没有哪个语言坐稳垄断地位、局势还不明朗的情况下，它依然还有机会。

\.Net正式合并后，之前的这些熟悉的名称，将成为过去时。让我们记住它们最后定格的版本：

- \.Net Standard 定格在 2.1
- \.Net Framework 定格在 4.8
- \.Net Core 定格在 3.1。

\.Net 加油。

最后多絮叨两句。封闭的坏处显而易见。微软尝尽了封闭的苦果。反观如今的水果，总觉得似曾相识。诚然，水果在很多方面比微软高明得多，而它的用户的粘性也要强的多。但是，近年来一次又一次霸道专横的骚操作，给消费者带来的冲击，还是在不断消耗它的生命力。历史总是惊人得相似，我们都不希望看到微软式悲剧在水果上再次重演，希望水果能早日收起戾气、拥抱开放，真正尊重消费者，而不是一次次让消费者无语。

## 本文的重点是语法，而非类库

进入代码之前，还有些话想说：

本文的主题是C#**语言**，而非\.Net的**类库**。因而大部分篇幅只关注于语法级别的演进。

- 譬如：Task类在\.NetFramework 4.0（对应C#4.0）已经引入。但是此时还不支持async/await关键词。因此，此时的Task类仅仅是\.Net类库的更新而已，并未引起C#语法的变动。而到了C#5推出（\.NetFramework4.5），引入了async/await，才体现在C#语法上。因此，我们不会在C#4.0的章节介绍Task类，而会在C#5.0介绍异步编程。

- 再比如：元组的概念也是\.NetFramwork 4.0（对应C#4.0）就有了。但是，它在当时表现为Tuple类，并不支持独特的圆括号语法，也没有支持解构。直到C#7.0引入ValueTuple时，才在产生了C#的新语法。因此，我们也不会在C#4.0时的章节介绍引用类型的元组类，而会在C#7.0的章节介绍值类型的元组的语法。

- 对于特别重要的类库，本文也会用适当篇幅来介绍。比如：LINQ（C#3.0）的实现既有语法层面的（查询表达式），也有类库层面的（查询扩展方法）。因为查询表达式本质上依赖查询扩展方法，又因为这些扩展方法同时使用了C#3.0的扩展方法、表达式树两种语法，加之其在日常开发中的极高使用频率，也会着重做出介绍。

# Hello World

下面的程序展示了一个C#程序大体长什么样：

```c#
//Program.cs文件：
using System;  //引用命名空间，相当于Java的import
namespace Sample //定义命名空间，相当于Java的定义package
{
    class Program //定义类
    {
        static void Main(string[] args) //定义方法。Main方法是程序的入口点
        {
            Console.WriteLine("Hello World.");  //打印Hello World.到屏幕
        }
    }
}
```

- 首先，C#是完全面向对象的语言，不存在排除在任何类之外的裸露语句。程序入口点也定义在类里。（C#10.0之前）
- 一般而言，一个程序需要有一个程序入口点，才能执行。程序入口点一般为Program.cs里的Main的方法。

## 命名空间（Namespace）

C#采用命名空间来组织类，类似于Java的包，但比Java的包更灵活。

> **与Java的package的主要对比**：
>
> - namespace不必跟目录对应，可以随意指定。只要你愿意，你的类可以全部放在System空间下。而Java的包名必须跟目录对应。
> - namespace是块结构，由花括号包裹（C#10.0之前）。它在一个文件中任意位置可以出现多次，即一个文件可以包含多个命名空间。而Java的单个文件必须对应单个包名，且包声明必须放在第一句。
> - 习惯不同，namespace一般每一段都是大写字母开头，并且没有以com开头的习惯。Java的包名一般全部用小写，且大多数公司的习惯为以com.开头（看各公司要求）。

## using语句

using语句，主要用法：

- 直接引用

    ```c#
    using System.IO;
    ```

- 别名

    ```c#
    using io = System.IO; //给命名空间指定别名

    //使用：
    io.FileStream fs;  //使用别名
    ```

- 静态引用（C#6.0引入）

    ```c#
    using static System.IO.File; //注意：静态引用只能引用类，而非命名空间。

    //使用：
    FileStream fs = Open("test.txt", FileMode.Open);  //直接使用File类的静态方法Open，替代File.Open
    ```

- 释放模式
    using还有一个跟命名空间无关的用法。用于自动释放可释放资源。请参阅[using自动释放语句](#using自动释放语句)

> 与Java的import语句对比
>
> - C#的using的目标是命名空间，不能是具体类型（静态引用除外）。直接引用类型会报错。
> - Java import的目标是类型。直接import包会报错。但是可以通过`包名.*`来一次性引入包下所有类型。
> - C#的`using xxxx;`，实际等于Java的`import xxxx.*;`。

可以通过显式指定命名空间路径，来使用命名空间下的类，即代码中直接使用`命名空间.类名`。显式引用时，可以不用using。

```c#
System.IO.FileStream fs;
```

---

接下来，我们将进入本文的主题。按照C#版本时间线，一步步介绍C#的语法演化。

# C# 1.0 —— Java的替代品

C# 1.0，深度参考了Java，并更多的保留了C++中被Java剔除的特性。同时，针对Java做出了一些改进。因此，C#语法上与Java类似，但是又比Java多了一些语法特性。例如，属性就是一个很好的创新。

C# 1.0，实现了以下功能

## 类（Class）和结构（Struct）

类和结构是C#代码的基本组成单元。

> 对比Java，C#的类定义文件也较为灵活：
>
> - C#单个文件中可以定义多个类，且可以任意指定可访问性，支持多个public类，并且类可以分散在不同命名空间中。而Java单个文件只能有一个public的类。
> - C#文件名与类名不必相同，而Java文件中public的类必须与文件名一致。

### Class与Struct的区别

1. class是[引用类型](#值类型%20vs%20引用类型)，struct为[值类型](#值类型%20vs%20引用类型)。class可以为null，struct不可以。class的赋值为复制引用地址，struct的赋值为元素拷贝。
2. class不可以使用Nullable<>类封装。struct可以。简写作 “类型?”(C#2.0引入。8.0之后新增了可null引用类型，这条不再普遍成立)
3. class可以继承，struct不可以，它是密封的(sealed)。关于密封类请查看[其他修饰符](#其他修饰符)
4. class如果不显式声明构造器，默认拥有无参构造器，但在声明构造器后，默认构造器会被删除。如果仍需要无参构造器，需要显式声明。结构不可以声明无参构造器（在C#10.0取消了这个限制），它默认拥有无参构造器，并且无法被删除。

### 修饰符（Modifier）

#### 可访问性修饰符（Access Modifier）

C#支持的可访问修饰符：

- public
- private
- protect
- internal

    - 只能在同一个应用程序集下可见。在编写类库时，internal的类在类库内相当于public，但是对于引用该类库的使用者，它不可见。

- protected internal

    - 相当于protected or internal

- private protected（C#7.2引入）

    - 相当于protected and internal。因为protected internal组合已经用来表示or的关系，而修饰符的顺序是无关紧要的。因而，只得采用这么个蹩脚的关键词组合来指代and的关系。

直观的对比，请看如下表格：

| 调用方的位置 | public | protected | internal | protected internal | private protected | private |
| ------- | --- | --- | --- | --- | --- | --- |
| 在类内 | ✔️ | ✔️ | ✔️ | ✔️ | ✔️ | ✔️ |
| 派生类（相同程序集） | ✔️ | ✔️ | ✔️ | ✔️ | ✔️ | ❌ |
| 非派生类（相同程序集）| ✔️ | ✔️ | ❌ | ✔️ | ❌ | ❌ |
| 派生类（不同程序集）| ✔️ | ✔️ | ✔️ | ❌ | ❌ | ❌ |
| 非派生类（不同程序集） | ✔️ | ❌ | ❌ | ❌ | ❌ | ❌ |

如果代码中未书写可访问性修饰符，则：

- 对于类，默认的可访问性是internal
- 对于类的成员，默认的可访问性是private
    - 特别的，对于嵌套的类，内部类的默认可访问性也是private

> Java没有类似internal的修饰符。

> Java的类不书写任何修饰符时，此类会被限制在仅Package内可访问，被称作friendly的（注意friedly并不是关键词）。需要注意，是限制在Package内，而非Module内。从C#角度理解，就是限制在命名空间内可访问。C#也没有这种机制的修饰符。

#### 其他修饰符

- static：静态成员、静态类（C# 2.0引入静态类）

- abstract：抽象类或抽象方法
- sealed：
    - 修饰类，表示密封类。密封类不可被继承。
    - 修饰方法，表示密封的方法，此方法不可再被派生类重写。
- const：定义常量。
    - 注意：值必须是编译时常量（可以在编译阶段计算出结果的表达式）。也就是必须是**字面量**（Literal），或者由字面量和简单运算符组成的表达式。特别的，string类型因为其不可变性，是可以作为常量的。如果值需要new运算符，则不能定义为常量。这种情况一般用static readonly的组合。
- readonly：用于修饰字段，表示只读字段。是指仅能通过构造方法、字段初始化表达式(C#2.0引入)赋值的字段。该字段在其他位置只读。
- volatile：用于修饰字段，标识一个字段可能会由多个线程同时修改。在多处理器的系统中，对同一块内存区域的读写顺序，有时会为了提升性能而被编译器、运行时甚至硬件重新排列。标记为volatile的字段，可以避免读写顺序被重排，确保完全按照书写的顺序执行。

> C#的sealed class对应的是Java的final class（最终类），表示该类不可以被任何类继承。注意：Java 15中也引入了sealed class预览版，并在17时变为正式语法。但是其含义与C#的不同。Java的sealed类的条件更宽松一些：它允许声明的已知的子类继承，除此之外其他的类不可继承。

> 用于修饰字段时，C#的const和readonly，相当于Java的final。

### 类型别名

大部分的关键词类型，都是别名：

- int -> System.Int32
- uint -> System.UInt32
- long -> System.Int64
- double -> System.Double
- byte -> System.Byte
- char -> System.Char
- decimal -> System.Decimal
- bool -> System.Boolean
- string -> System.String
- object -> System.Object
- ...

特别注意：在C#中上述别名**完全等价**。

> Java中一般大、小写的类型含义并不相同。大写开头的类型是包装类。基本等价于C#中的Nullable\<T\>（C#2.0引入）。
> > 例如：Java中的Double，相当于C#中的double?。而C#中的Double和double完全等价。

### 隐式继承、Object类

关于**隐式继承**，举例说明：enum（枚举）都隐式继承Enum类，delegate（委托）都隐式继承Delegate类，值类型均隐式继承ValueType类，数组都隐式继承Array类。查看这些基类，会发现其定义都是class。但是编译器处理这种隐式继承时，并不会都把它们都变成引用类型，而是按照语法约定确定是值类型还是引用类型。这种隐式继承关系是编译器变的魔术，你无法直接在代码中显式声明这种继承关系。隐式继承的好处是，所有对应类型都可以使用基类定义的方法，如enum都可以使用Enum类定义的HasFlag方法等。

object类是极其特殊的类。C#中的任何类型，都隐式继承自object。任何类型的对象都能与object对象互转。这也包括值类型。

object类定义了ToString、GetType、Equals、GetHashCode等方法。所有类型均可使用这些方法，也可以重写这些方法。

> 这与Java不同。Java中Object被认为是引用类型的基类，int属于基本类型，不是Object。

### 值类型 vs 引用类型

值类型举例：

- bool
- char
- int
- 所有struct
- 所有enum
- 元组（C# 7.0）

引用类型举例：

- string
- 数组
- 委托
- 所有class
- record（C# 9.0）

值类型和引用类型特点类似于C++。

- 存储
    - 值类型变量在栈空间中直接存储变量值。对于struct，包含的所有字段都在栈中占用相应大小栈空间。struct中的引用类型字段仅在栈上占用一个指针的大小。当struct嵌套时，占用的空间也会等同于每个struct展开的大小。除了struct之外的值类型和仅包含非引用字段的struct又合称**非托管类型**（Unmanaged Type），因为它们不会通过GC来回收资源。栈上的空间有着相对固定的回收时机：跟随方法的调用进行压栈和弹栈。这点学过C++的人应该可以理解。非托管类型可以用来与C++等语言编写的库传递参数和结果，也能用于编写unsafe代码。不过由于栈的大小有限，使用过大的struct并不是很好的主意。尤其在多重递归的场景中，使用不当可能快速耗尽栈空间。
    - 引用类型则只在栈内存储堆空间的地址信息，实际数据则存储于**托管堆**（Managed Heap，以下所提到的堆空间，均指托管堆）空间中。堆的可用空间要大得多，几乎可以使用全部内存。引用类型又叫**托管类型**（Managed Type），其内存资源通过GC机制回收。

- 赋值和传参
    - 值类型在赋值操作、作为参数传入方法时，会引发数据拷贝。一个struct在赋值时，会拷贝每个字段的值（如果字段本身也是struct，会进一步深拷贝）。对被赋值或传入方法后的变量修改不会影响到原变量。
    - 引用类型的赋值和参数传入只是拷贝地址信息，对被赋值后引用对象的修改都会导致用来赋值的对象的变更。

> Java并没有值类型的概念，对应的概念是基本数据类型。基本数据类型包括boolean、float、char、byte、short、int、long共8种。其余均为引用类型。而基本类型全都有对应的包装类。

接下来，我们分别介绍下这两种类型：

### 值类型（Value Type）

#### 结构

结构（Struct）是值类型的。

除了前面章节提到的不同点之外，结构与类还是很相似的。结构中也可以定义字段、属性、方法等。也正因为如此，我们在C#的教程中，**更多提及的是类型（Type）而不是类（Class）**。

int、double等关键词类型，是Int32、Double等的别名。通过定义可以看到，它们本质上都是Struct。因而，int等值类型也能够定义自己的方法。加上隐式继承自ValueType和Object。因而int可以使用Equals、ToString等方法；也能使用GetType方法获取Type对象从而使用反射；还可以使用静态方法：如Parse，用于将string转成int。

事实上，Struct可以用于指代一切值类型，包括枚举。

> Java没有Struct类型。

> Java的基本类型，真的十分“基本”。它们没有成员方法可用。如上例，要将String转成整数，需要用包装类Integer的parseInt方法。

#### 装箱（Boxing）和拆箱（Unboxing）

如果将值类型与object互转，或者与其隐式继承类型互转，会引发装箱（或称为封箱）和拆箱（或称取消装箱）

装箱：

```c#
int x = 9;
object y = (object)x;  //引发装箱
ValueType z = (ValueType)x;  //引发装箱
Status status = Status.OK;  //Status是枚举类型
Enum statusBoxing = (Enum)code;  //引发装箱
```

拆箱

```c#
//接上个例子
x = (int)y;  //引发拆箱
x = (int)z;  //引发拆箱
status = (Status)statusBoxing;  //引发拆箱
```

在装箱前后，调用GetType获取类型描述会得到相同的类型。上例中，`x.GetType()`和`y.GetType()`获取到的类型相同，都是Int32；`status.GetType()`和`statusBoxing.GetType()`获得到的类型相同，都是Status。

需要注意，装箱和拆箱需要大量计算，因而不是最优选择。如需接收或者传递任意类型参数，应该优先考虑[泛型](#泛型（Generic）)（C#2.0引入），而非使用Object

> Java将int赋值给Object对象，也会进行装箱操作。它事实上是将int转成包装类Integer后赋值给Object。装箱后的对象事实上发生了类型变化，原先为int类型，装箱后为Integer。

> Java的泛型类型并不允许基本类型。因此，使用泛型时，不会因为可以是基本类型而节省装箱的操作，因此使用Object传递参数和使用泛型类型传递参数相同，并不会导致效率差异。

#### 枚举（Enum）

枚举是值类型的，默认情况下等价于int类型，且可以与int类型显式互转。这点与Java的枚举类不同。C#的enum定义更像C++。

枚举定义中列举可能出现的枚举项名称，这些名称分别对应一个int值。其值默认从0开始，每项递增。

但是你仍然可以指定枚举项对应的值，方法是在枚举项后面书写 `= 值` 。你还可以只指定一部分枚举项的值而省略另一部分，未指定值的枚举项会从上一个指定了值的枚举项顺序递增下来。

枚举还允许赋值为未在枚举项中列出的int值。即：可以将任意int值显式转换成枚举类型，并赋值给该类型对象，不会报错。

枚举的ToString方法，返回的是该项的定义文本。但是如果值未对应已定义的项，则ToString直接输出数字。

```c#
public enum StatusCode //定义枚举
{
    Success = 0,  //显式指定Success项值为0
    DatabaseError,  //未指定DatabaseError值，因而其值为前一项加1，为1
    SystemError  //同前，此项值为上一项加1，为2
}

//测试
StatusCode code = StatusCode.Success;
Console.WriteLine((int)code); //输出为 0 
Console.WriteLine(code.ToString()); //输出为 Success
code = (StatusCode)100;  //有效赋值，不会报错
Console.WriteLine(code.ToString()); //输出为 100
```

枚举也可以指定其实现类型。方法是用类似继承的语法，枚举定义时在枚举名后面使用 `:` 指明实现类型。实现类型只能是byte、sbyte、short、ushort、int、uint、long、ulong这几个**整数类型**。虽然这里是 `:` 符号，但是我们不称之为继承，毕竟Struct本就无法继承，并且枚举既不能重写方法，也无法定义其他方法。

```c#
public enum StatusCode : ulong //定义枚举，并指定枚举为ulong类型
{
    Success = 0uL,  //顺便提一嘴：数字后面的L，从规范上来讲要用大写，避免跟1混淆。
    DatabaseError,
    SystemError
}
```

> 与Java枚举的对比：
>
> - C#枚举为值类型，等价于int（或其他整数类型）。Java的枚举实际是枚举类，因而是引用类型。
> - C#枚举定义仅能列举枚举项，不支持编写成员方法、不能编写构造器，虽然仍能使用object类、ValueType类、Enum类定义的方法，但是却不能重写它们。Java枚举定义实际是定义了枚举类和该类的常量对象。Java的枚举定义中可以插入构造器、方法等，也可以重写toString方法。
> - C#的枚举仅能指定实现类型，并且必须为整数类型。Java的枚举虽无法继承类，但是可以实现接口。
> - C#枚举可以与int等整数类型直接互转，并且支持将未在枚举中定义的整数值赋值给枚举对象。而Java与int等类型互转，需要通过枚举类定义的字段和get、set方法来实现，并且不存在超出枚举定义项的赋值。
> - C#可以给每个枚举项直接指定值，语法为 `枚举项=值` ，值为所指定类型，默认是int。而Java必须通过构造器来实现，并在定义枚举项时指定该项如何使用构造器，因而语法是 `枚举项(构造器参数列表)` 。
> - Java的枚举都有个original方法，它返回的是该枚举项的序号，且固定顺序为0、1、2...。从概念、用法来讲，它并不等同于C#意义上的枚举值。
> - C#支持位枚举，而Java不支持。（马上我们会讲到位枚举。）
> - 最后又是习惯问题。C#的枚举项一般仍旧按照Pascal规则命名，而Java的枚举项习惯于全大写字母，单词间用下划线连接。

> C#和Java的枚举，可以说各有优劣。
>
> - C#的枚举可以直接用来接收数据库、WebApi传入传出参数等中int的值，使其在程序代码内被赋予明确的枚举含义。而Java要把数据库字段转为枚举需要更多额外操作。
> - Java的枚举项可以携带更多信息，例如可以同时包含一个int类型的id、一个String类型的name。这在特定场景下十分好用。而C#的枚举只有整数信息，如果要附带其他信息需要通过中文枚举名（为了使用ToString，不推荐）、编写扩展方法（C#3.0）、使用Dictionary映射、封装Struct等手段。

> 额外To CShaper —— Java的枚举长这样：
>
> ```java
> //==Java==
> public enum StatusCode { //定义枚举
>     SUCCESS, DATABASE_ERROR, SYSTEM_ERROR; //枚举项，此处分号可以省略
> }
> ```
>
> 或者：
>
> ```java
> //==Java==
> public enum StatusCode { //定义枚举
>     SUCCESS(0), DATABASE_ERROR(1), SYSTEM_ERROR(2); //枚举项，调用构造器。因为下面还有定义内容，此处分号不能省略
>     // 成员字段
>     private int statusCodeValue;
>     // 构造器（注意，枚举的构造器只能是私有的），枚举不可以new，只能使用已定义的项
>     private StatusCode(int statusCodeValue) {
>       this.statusCodeValue = statusCodeValue;
>     }
>     //字段值的get方法
>     public int getStatusCodeValue() {
>         return statusCodeValue;
>     }
> }
> ```
>
> 使用
>
> ```java
> //==Java==
> StatusCode code = StatusCode.SUCCESS;
> StatusCode cod2 = StatusCode.valueOf("SYSTEM_ERROR");
> boolean eq = code == code2;  //因为枚举项是常量，所以==也可以用于判断相等
> ```

C#还支持**位枚举**:

位枚举一般每个枚举项都是2的整次幂。

虽然不是必须，但是定义位枚举时，一般添加`FlagsAttribute`特性。这样会影响ToString的输出。

位枚举可以方便单个枚举变量同时包含多个枚举项。方法是使用按位与运算符`|`来合并枚举项。并且可以使用枚举类型内封的HasFlag方法，轻松判断枚举变量是否包含了特定位枚举项：

```c#
[Flags]
public enum Operation //定义位枚举
{
    Add = 0x01,
    Modify = 0x02,
    Remove = 0x04,
    Execute = 0x08
}
//...
Operation operation = Operation.Execute | Operation.Add; //赋值位枚举为多个值
Console.WriteLine(operation.ToString());  //输出为 Add, Execute。如果未标记FlagsAttribute，则输出为 9
bool haveRemove = operation.HasFlag(Operation.Remove); //查询位枚举是否包含枚举项
```

值得注意的是：任何枚举都可以使用HasFlag方法，即使未标注 `FlagsAttribute` 。

### 引用类型（Reference Type）

#### 数组（Array）

数组是引用类型的。因而C#的数组与C++不同，它被分配在堆空间上，而不是栈空间上。数组的初始化也使用new关键词。这点与Java一致。

数组隐式继承自Array类，因而Array具有的方法、[属性](#属性（Property）)等，数组都可以用。比如Length属性，用于获取数组长度。不过，无法直接使用Array类来声明数组。

```c#
//一维数组
int[] t = new int[10];
t[0] = 1;

//二维矩形数组
int[,] a = new int[10,10];
a[0,0] = 1;

//可变长度的二维数组
int [][] b = new int[10][];
b[0] = new int[10];
b[1] = new int[6];
b[0][0] = 1;
```

> 与Java不同，C#定义数组时，[]只能放到变量名前面。而Java则既可以放在前面，也可以放在后面。
>
> - `byte [] bytes= new byte[100]; //合法`
> - `byte bytes [] = new byte[100]; //不合法`

#### 类（Class）

##### 类的继承

C#的继承使用`:`

> Java使用`extends`关键词

C#不支持多重继承（实现接口数量则不限制），这点与C++不同，但是与Java一致。

##### 嵌套类

类支持嵌套，且嵌套类支持protected、private等修饰符

```c#
public class AA
{
    public class BB //public的嵌套类，其他类里可见
    {
    }
    protected class CC //protected的嵌套类，仅其派生类可见
    {
    }
}
public class DD
{
    public AA.BB bb; //ok
    public AA.CC cc; //not ok，编译器报错
}
```

### 方法（Method）

方法与函数、过程是同义词，是类或结构的成员，用于描述一段执行过程，并返回或者不返回结果。

C#的命名规范中，方法名以大写开头（即Pascal命名法）

> Java编码规范中，方法名是小写字母开头（驼峰命名法）。

#### 方法的参数

##### out和ref关键词

C#的方法，支持`out`和`ref`两个特殊修饰符，来修饰参数。

虽然语法上并不禁止这两个关键词用于引用类型，但是实际上它几乎只被用于值类型。

它们表明，传递参数时，不应复制值，而是传递值变量的引用。

传递为`out`和`ref`参数，必须是左值类型的。所谓**左值类型**，是指可以被放在赋值号`=`的左侧——也就是说，只能是变量（unsafe模式下还可以是指针取值表达式）。

- `out`表示输出参数，表明该方法会将此参数作为输出。out参数传入方法前不必赋初始值。对于包含out参数的方法，编译器会检查方法体内每个分支路径，确保每一条分支在return之前都对此参数做了赋值。如果有分支路径没有赋值，会在编译时报出编译错误。这跟检查每个分支路径都有return语句一样。
- `ref`表示引用参数。方法体内可以对该变量值进行赋值，并实际改变调用时传递得变量的值。ref变量不要求一定要在方法体内更改，也不会做分支路径检查。作为ref参数的变量，在传入方法之前，必须已经赋值。

具有`out`和`ref`修饰的参数，在调用方法时，参数前也必须显式添加`out`和`ref`关键词

```c#
//官方库中int的TryParse方法定义
public struct Int32 
{
    public static bool TryParse(string str, out int outValue);
}
//使用：
int value; //不必赋初值
bool success = int.TryParse("1", out value); //value的值由方法输出
Console.WriteLine(value); //输出为 1
```

> Java不支持上述特性，可以考虑使用自己定义一个类实现包装器的功能，从而变相实现引用传递。注意，无法直接使用官方提供的包装类，因为Integer等包装类内的数据是只读的。

##### 参数默认值

像C++一样，C#支持参数的默认值。

有默认值的参数，在方法调用时可以省略。

```c#
public class Class
{
    public List<Student> GetStudents(int limit = 20) //limit含默认值20
    {
        //省略
    }
}
//使用：
Class oneClass = new Class();
List<Student> students = oneClass.GetStudents(); //可以不指定limit值
```

> Java不支持参数默认值。因而想要实现少传参数的简写形式，只能通过方法重载。
> > 事实上，后续C#还支持了以命名的形式指定参数的值，而对于未指定值的有默认值的参数使用默认值。这个特性被称为[可选参数](#可选参数（Optional%20Argument）)（C# 4.0引入）。而Java语法无法支持此操作。

##### 可变参数

C#使用params关键词标记可变数量的参数

params只能修饰数组类型

```c#
//官方库关于string的Format方法的定义
public class String 
{
    public static string Format(stirng format, params object[] args);
}
//使用
string.Format("你好"); //0个可变参数
string.Format("你好，{0}", "帅哥"); //1个可变参数
string.Format("你好，{0}。现在是{1}年。今日天气：{2}。出行建议：{3}。", "帅哥", 2021, "晴", "适合出去浪"); //4个可变参数
```

> Java可变参数的关键词为`...`。他们在语法上的区别：
>
> 1. C#声明可选参数时，需要正常带上`[]`符号，表示该参数是个数组。而Java，虽然可选参数变量实际为数组类型，但是声明时不带上`[]`符号。
> 2. C#的params放在类型前面，而Java的`...`放在类型后面。

#### 构造器（Constructor）、终结器（Finalizer）

构造方法又叫构造器。类和结构都可以拥有构造器。默认情况下，类和结构都拥有无参数的构造器。类如果主动声明了构造器，则默认的无参构造器会被删除。结构则始终拥有无参构造器。

##### 静态构造器（Static Constructor）

静态构造方法的语法是`static 类名() { ... }`。它不能拥有可访问性修饰符，不能指定返回类型。并且不能拥有参数。

它会访问类型的任何可访问成员之前被执行。

- 在第一次使用并访问任何静态成员之前
- 实例的构造器被执行之前

它只会执行一次。

```c#
public class What
{
    static What()
    {
        Console.WriteLine("作甚");
    }
    
    public What()
    {
        Console.WriteLine("干啥");
    }
}

What what = new What();  //先打印 作甚，再打印 干啥
What what2 = new What(); //只会打印 干啥
```

注意：仅仅声明What类型的变量what，而不用`new`初始化，是不会引起静态构造器被调用的。

静态构造器中无法访问非静态成员。

> Java的叫做类初始化器（Class Initializer），它的语法是`static { ... }`。功用完全一致，语法更加简洁。

##### 构造器串联

C#支持本类构造器或者基类构造器的串联，这被称为**构造器调用**，我们习惯将其形象的称为构造器串联。语法为：构造方法声明之后、方法体之前使用`:this(参数列表)`或者`:base(参数列表)`

```c#
public class ArtBook : Book
{
    private string Name;
    public ArtBook()
        : base()    //base串联，调用基类构造方法
    {
    }
}
public class NovelBook : Book
{
    private string Name;
    public NovelBook()
        : this("无名")  //this串联，调用本类其他构造方法
    {
    }
    public NovelBook(string name)
    {
        Name = name;
    }
}
```

> Java中的构造器调用使用`super();`和`this();`语句，直接在构造方法体内调用。虽然是直接写进方法体内的语句，但规定了只能放在第一句，因此与C#的机理并无不同。对比之下，C#的写法更好的表达了其自然含义。

##### 终结器（Finalizer）

类似于C++，C#支持类的析构方法，又叫终结器。

终结器命名为类名前面加上`~`

终结器不能加任何修饰符，包括public、private等。

一般不会单独重写终结器。如果类中包含需要释放的资源，一般使用[IDisposable释放模式](#IDisposable释放模式)。

#### 多态（Polymorphism）

C#支持的多态包括**重载**(Overload)、**重写**(Override，又叫覆盖)和**隐藏**(Hidding)：

- 重载
    1. 同一个类中，相同方法名，不同参数的方法重载。
    2. 同一个类中，相同方法名，参数也相同，泛型和非泛型的方法重载。（C#2.0以后）
    3. 同一个类中，相同方法名，参数也相同，泛型参数数量不同的泛型的方法重载。（C#2.0以后）
- 重写
    - 父类声明为`virtual`的虚方法，子类可以通过`override`关键词进行重写。如果没有标记为虚方法，则子类无法对其进行重写。需要特别注意：必须加上`override`关键词才是重写，否则就是隐藏，请参考下条。
- 隐藏
    - 任何方法（包括`virtual`和非`virtual`的方法），子类都可以对其进行隐藏。使用隐藏语法时，父类的方法没有被覆盖，而是被隐藏了。在调用同名同参方法时，如果调用的对象声明为子类型，则正常调用子类定义的方法；而如果声明为父类型，但实际类型为子类型，则会取消隐藏，调用父类的方法。
        - 隐藏不要求与父类方法拥有一样的访问级别，也不要求其返回类型必须相同。
        - 隐藏一般使用`new`关键词修饰方法。虽然`new`可以省略，但是仍强烈建议显式加上`new`，以提高代码可读性。

下面我们通过举例，看看子类对父类的方法重写和隐藏的区别：

```c#
public class Book
{
    public virtual int GetPage() //声明为虚方法
    {
        return 0;
    }
}
public class NovelBook : Book 
{
    public override int GetPage() //重写父类方法
    {
        return 1;
    }
}
public class MathBook : Book
{
    public new int GetPage() //隐藏而不覆盖父类方法，此处关键词new可以省略，但推荐加上
    {
        return 2;
    }
}
```

然后，我们看看调用：

```c#
Book oneBook;

NovelBook novelBook = new NovelBook(); //NovelBook的GetPage方法是重写
oneBook = novelBook;
Console.WriteLine(novelBook.GetPage()); //输出 1
Console.WriteLine(oneBook.GetPage());   //输出 1

MathBook mathBook = new MathBook();  //MathBook的GetPage方法是隐藏
oneBook = mathBook;
Console.WriteLine(mathBook.GetPage());  //输出 2
Console.WriteLine(oneBook.GetPage());   //输出 0
```

可见：

- 调用重写的方法，会根据调用对象的实际类型，调用其类型的重写方法。子类对象和赋值为子类对象的父类对象，调用的都是子类的方法。上例中，novelBook对象和oneBook对象，调用的都是子类NovelBook定义的方法。
- 调用隐藏的方法，会根据当前对象的声明类型，调用声明类型的方法。此时，子类对象调用的为子类的方法，赋值为子类对象的父类对象调用的是父类的方法。上例中，mathBook对象调用的是MathBook定义的方法，而oneBook对象调用的是Book中定义的方法。

不过，无论重写还是隐藏，其内部均可以使用`base.方法`来调用基类的方法。

PS：上述重写和隐藏描述的都是非静态的方法。静态方法无法被重写，所以实际上只能被隐藏。

> Java没有`virtual`和`override`关键词。但是，Java的方法被设计成默认就是虚的。直接在子类中定义对父类方法的重写即可。但也可以通过`@Override`注解，来标注子类的方法是重写方法。标注此注解同样可以实现编译阶段的检查功能，以确保父类包含此方法。(Java的注解与C#的特性是同义词)

> Java没有C#意义上的方法隐藏机制。但是同样可以实现静态方法的隐藏。

### 属性（Property）

属性，是C#1.0对Java的一个较为明显的优化。

> 对于Java的类，为了提升可控性，我们一般不会直接将字段标记为`public`，暴露给外界操作。我们会将字段标记为`private`、`protected`，通过暴露public的get和set方法来获取和设置该字段。这样做可以方便进行安全检查、权限控制以及执行额外操作。
>
> 例如：
>
> ```java
> //==Java==
> public class Person
> {
>     private String name;
>     public void setName(String name) {
>         this.name = name;
>     }
>     public String getName() {
>         return this.name;
>     }
> }
> ```

考虑到get、set模式的通用性，C#提出了一种新的成员类型：属性，用于等价替代上述模式。

上述功能，用属性实现长这样：

```c#
public class Person
{
    private string name;
    public string Name
    {
        get { return name; }  //getter
        set { name = value; } //setter
    }
}
```

上述代码中，Name就是一个string类型的属性。其中，`get`和`set`方法被称为**访问器**。它们又分别被称为getter和setter，实现了与Java中使用get和set方法操作字段一样的功能。

在setter中，可以使用`value`关键词，来指代要赋值的内容。

由于属性本质上等价于get和set方法，所以可以视作方法。属性可以出现在接口中，也能被子类重写（Override）和隐藏。

从语法上，属性带来了更多便捷。使用属性时，语法形态跟直接使用字段类似：

```c#
person.Name = "你好"; //调用setter，给属性赋值
string name = person.Name; //调用getter
```

需要注意的是，属性需要通过背后的实现字段来进行赋值和获取操作。如果在属性的`get`、`set`方法中操作属性本身，可能会引起无限递归。

C#3.0引入了[自动实现的属性](#自动属性（Auto-Implemented%20Property）)，自动属性才是属性的最常见定义方式。

> 对比Java：
>
> - 属性给与了C#更加简洁的语法。既简化了get和set方法的定义，又在使用时避免了Java那样的大量的圆括号，代码更为美观。
> - 更为重要的是，属性可以作为表达式的一部分，使得属性可以嵌入到更多场景中。具体说来，在使用属性的setter时（代码表现为赋值表达式），表达式仍具有返回值（即赋值表达式的值）。
> - 在后续C#支持的[初始化器](#初始化器（Initializer）)（C#2.0引入）等语法中，因为有属性的存在，也使得初始化对象时代码简洁不少。这在多重嵌套的情况下尤为明显。而Java虽然有双括号初始化语法，但是一般不建议使用，而且代码也要啰嗦的多。

## 接口（Interface）

C#的接口习惯于以单个大写字母I作为前缀。而接口的实现类，一般没有固定前后缀。

> 作为对比，一般Java的接口名无固定前后缀。而接口实现类，习惯加Impl后缀。

接口的实现，语法为`类:接口`，与类的继承使用相同的符号。

> Java则使用了不同的关键词，类的继承为`extends`，接口的实现为`implement`。

这里介绍两组比较重要的接口：

### 可释放接口（IDisposable）

IDisposable指定了Dispose方法，用于释放资源。

#### using自动释放语句

实现了IDisposable接口的类对象，C#在语法上允许使用`using`语句自动释放：

```c#
using (FileStream fs = File.OpenRead("test.txt"))  //fs会在using块结束后自动调用Dispose方法释放资源
{
    //省略
}
```

它等价于下面的代码：

```c#
FileStream fs = File.OpenRead("test.txt");
try
{
    //省略
}
finally
{
    fs.Dispose();  //释放
}
```

需要注意，using的括号内是表达式，它返回一个可释放的对象。因而，using并不要求一定要在using的同时声明变量，也可以using已有的对象。

```c#
FileStream fs = File.OpenRead("test.txt");
using (fs)   //合法
{
    //省略
}
```

对于实现了IDisposable的类，如果没有使用using，也没有主动调用Dispose方法。则会在失去所有引用后，于GC回收时被释放。注意，这种情况下具体的释放时机可能变得不可控。如果程序中有循环等大量产生资源的语句，未及时的释放可能引起资源因无法及时回收而快速消耗（例如TCP连接）。

> IDisaposable相当于Java的AutoClosable接口

> using语句相当于Java的try-with-resources语句。不过，他们也有用法的区别
>
> - C#的using语句，圆括号内为表达式而非语句。因此，using语句的圆括号内只能指定一个对象。如果要同时对多个对象自动释放，需要使用using嵌套。（C#8.0以后支持更为美观的写法，但其本质没有变化）
> - Java的try-with-resources，try后面的圆括号为多个声明了可释放资源的语句。因此，可以在一个try语句内一次性同时指定多个资源在块结束后自动释放。
> - C#既可以在using括号内同步声明变量，也可以直接使用已声明过的变量。而Java则必须在try括号内同步声明资源（在Java 9之后，不再有此限制）。 

> 在这一点上，Java比C#要更灵活。

> To CShaper：Java的自动释放示例
>
> ```java
> //==Java==
> try (
>     //同时释放两个资源
>     ZipFile zf = new ZipFile(zipPath);
>     BufferedWriter writer = Files.newBufferedWriter(outputPath, outputCharset); //最后一个资源后面的分号可以省略
> ) {
>     //省略
> } catch (IOException e) {
>     e.printStackTrace();
> }
> ```

#### IDisposable释放模式

一般在实现IDisposable接口时，不是简单实现Dispose方法，而是会遵循“释放模式”。

释放模式可以在Visual Sudio中自动生成范式代码。它长这样：

```c#
public class ChatRoom : IDisposable
{
    private bool disposedValue;

    protected virtual void Dispose(bool disposing)
    {
        if (!disposedValue)
        {
            if (disposing)
            {
                // TODO: 释放托管状态(托管对象)
            }

            // TODO: 释放未托管的资源(未托管的对象)并重写终结器
            // TODO: 将大型字段设置为 null
            disposedValue = true;
        }
    }

    // // TODO: 仅当“Dispose(bool disposing)”拥有用于释放未托管资源的代码时才替代终结器
    // ~ChatRoom()
    // {
    //     // 不要更改此代码。请将清理代码放入“Dispose(bool disposing)”方法中
    //     Dispose(disposing: false);
    // }

    void IDisposable.Dispose()
    {
        // 不要更改此代码。请将清理代码放入“Dispose(bool disposing)”方法中
        Dispose(disposing: true);
        GC.SuppressFinalize(this);
    }
}
```

具体来说：

- 在释放模式中，通过一个含布尔参的Dispose方法重载，来实际处理释放资源。接口定义的无参Dispose方法，调用该重载方法，并调用GC方法完成释放。
- 释放模式中，定义了一个标记字段disposedValue，用于避免重复释放。
- 开发者可以根据TODO任务提示，将类中包含的不同类型的资源的释放逻辑写在相应位置。
- 当类中包含未托管资源时，还需要重写终结器。方法是把上述终结器的注释解开即可。

使用释放模式，可以更好的处理托管、非托管资源的释放。

关于非托管资源和非安全上下文，请参考[unsafe上下文](#unsafe上下文)

### 枚举器接口（IEnumerator） 和 可枚举接口（IEnumerable）

IEnumerator：**枚举器接口**，它定义了MoveNext方法、Reset方法和Current属性，用于移动到下一个元素、移动到第一个元素和获取当前元素。IEnumerator也有其泛型版本IEnumerator\<T\>（C#2.0引入），泛型版本的Current类型不是object而是泛型指定的类型。

IEnumerable：**可枚举接口**，它定义了GetEnumerator，用于获取该类的IEnumerator对象。IEnumerable也有其泛型版本IEnumerable\<T\>（C#2.0引入）。泛型类型的GetEnumerator返回类型也是IEnumerator\<T\>。

实现了IEnumerable（或IEnumerable\<T>）接口的类，可以使用`foreach`语句进行遍历。

foreach语句的关键词为foreach和in：

```c#
foreach (object item in list)
{
    //省略
}
```

我们可以把上述枚举过程叫做迭代（Iterate、Iterating）。但是一定一定要注意，它与[迭代器](#迭代器（Iterator）)（C#2.0引入）不是一回事，后者在C#中特指迭代器方法（Iterator Method）。

特别的：定义了返回类型为IEnumerator且名称为GetEnumerator的方法的类，即使未指明实现IEnumerable接口，也可以使用foreach。这个特点在C#9.0时被强化：GetEnumerator即使是扩展方法也可以使用foreach。（泛型版本同理）

IEnumerator和IEnumerable（及它们的泛型版本）非常重要，因为它们：

- 可以用来实现迭代器方法（C#2.0引入），这是一个非常重要的机制。
- 可以支持LINQ（C#3.0引入，且LINQ建立在迭代器之上）。LINQ可以算得上CShaper的快乐源泉。

这两个接口都应该**优先使用泛型版本**（C#2.0）。

> C#的枚举器相当于Java的迭代器（Iterator），Java使用迭代器遍历的foreach语法为`for (object item : list)`。

> C#在2.0版本引入了迭代器，但是它与Java的迭代器是两种不同的概念。C#的迭代器是独有的特色语法，它通过编译器进行语序重排，因而具有延迟执行、执行顺序反常识的特点。

## 委托（Delegate）

委托类似于C++的函数指针，用于指代方法。委托跟类一样，是一种类型定义。

声明委托时定义了一种类型，这个类型规定该委托类型的对象所指代的方法必须满足的参数列表和返回类型。

委托使用`delegate`关键词声明。

```c#
public delegate int Compare(int a, int b); 
```

上述代码定义了一个委托类型Compare，该委托类型描述了一种需要两个int类型参数，且返回int类型值的方法。

假设，我们有一个方法定义，如下

```c#
//接上例
public int CompareMethod(int left, int right)
{
    return left - right;
}
```

我们看到，该方法的参数数量、每个参数的类型、返回值类型都与Compare这个委托类型的定义相同。这种情况下，定义一个Compare类型的委托变量compare，可以通过赋值使得compare指代CompareMethod方法：

```c#
//接上例
Compare compare;
compare = CompareMethod;
```

这时我们称，compare将实现**委托给**了CompareMethod方法；CompareMethod是**被**compare**委托**的方法，或者说CompareMethod是compare的**委托实现**。

赋值运算符的右侧，可以是方法名、匿名方法实现或者另一个委托对象。

这里需要注意，赋值方法给委托时，需要满足静态方法、实例方法的要求：在静态方法中，无法给委托变量、静态成员赋值为非静态的方法。

如果赋值给委托的方法在另一个类中，则可以使用`对象.方法名`或者`类名.方法名`赋值，具体用法也同样需要满足上一条的要求。

```c#
//接上例
Compare compare2 = compare;  //将委托赋值给另一个委托
```

同时，我们也注意到：在上面例子中，委托规定的参数名和所指代的方法所定义的参数名并不相同。这种情况下仍然可以用委托指代该方法。由此可见，方法要赋值给委托时，参数的名称并不重要。这同方法签名是一致的。

如上声明过后，就可以使用该委托对象，进行方法调用了：

```c#
//接上例
int result1 = compare(1, 2);         //第一种调用方式
int result2 = compare.Invoke(4, 2);  //第二种调用方式
```

上述代码实际调用了被委托的CompareMethod方法。

这里特别提一下，没准你可能会对下里面的语法感到新鲜，但是其实它很好理解：

```c#
//接上例
int result3 = someObject.GetCompareDelegate()(3, 7);  //someObject的GetCompareDelegate返回了Compare类型的委托对象。此处在拿到委托对象后立即调用，因而出现连续两个()
```

使用委托的好处是：可以先声明方法的规格，专心于使用者代码的书写。而该方法规格具体的实现，则可以在运行时再绑定到具体的方法。

注意，委托也是引用类型的，可以为null。

> 许多语言都有委托机制。如：用于编写IOS程序的Object-C语言，也有委托机制，被称为协议（protocol）。JS就更不用说了，`var func = function(){}`大伙都写过吧。

> Java中没有委托类型。如果要在Java中实现类似委托的效果，需要利用反射。
> > 这里提供一种可行的实现方法：
> >
> > - 定义一个方法。该方法接收三个参数：一个Object参数，作为提供被委托方法的对象，定义为obj；一个字符串参数，用于提供被委托的方法名，定义为methodName；一个Object类型的数组、Map或者可变参数，用于提供调用该方法时的参数列表，定义为args。
> > - 实现此方法：先通过反射找到obj对象的、名称为methodName的方法，然后调用这个方法，并将args作为参数传入。
>
> 因为Java没有语法层面的支持，上述套路虽然也能够实现类似功能，但显然，这不够优美。

### 多播委托（Multicast Delegate）

事实上，我们定义的委托类型，属于多播委托（多路广播委托，MulticastDelegate）。对于被委托的方法、委托对象，是可以组合起来的。这被称为**委托组合**（Delegate Combination）：

```c#
Compare compare; //定义委托变量
compare = CompareMethod1 + CompareMethod2; //委托给CompareMethod1和CompareMethod2的组合
```

`+`运算符两侧的操作数，同样可以是方法名、匿名的方法实现、委托对象等。它用于组合两个符合同一个委托定义的操作数。如果其中包含null，则仅仅返回另一个操作数（也可能是null）。上述例子中，委托对象compare将委托给两个方法CompareMethod1、CompareMethod2共同处理。执行的顺序会按照从左到右的顺序。

如果要删除一个委托实现，则使用`-`运算符。

事实上，除了`+`和`-`，我们同样可以使用`+=`和`-=`运算符。因而我们还可以这样使用委托：

```c#
Compare compare; //定义委托变量
compare = CompareMethod1; 
compare += CompareMethod2;
```

有趣的是，委托对象即使为null，也可以使用`+=`：

```c#
Compare compare = null; 
compare += CompareMethod1; 
```

> Java中如果要实现多播委托，需要记录**一组**被委托对象，并在委托调用时遍历所有对象，通过反射挨个调用这些对象的指定方法。具体实现我就不举例了。读者可自行思考。（或者问度娘）

## 事件（Event）

事件是C#引入的一种机制，它的自然含义为回调：当有事件发生时，订阅该事件的类会接到回调通知，并允许订阅者执行额外的处理过程。

C#中的事件是基于委托的。有了委托，才有事件。

与属性一样，事件是类的成员。

**事件是一种特殊的委托类型成员**。

这句话有三重含义：

1. 委托是类型定义范畴的，而事件是类成员声明范畴的。
2. 事件是委托类型的。
3. 事件是比较特殊的委托成员，它一般为EventHandler类型或EventHandler\<T>(C# 2.0引入)类型。

为了给事件赋予自然含义，我们给对事件委托的操作起了更利于人类理解的别名：我们把对事件的`=`、`+=`操作称为订阅、添加订阅、绑定回调；对事件委托的调用，称为触发事件、下发事件通知、回调给订阅者。

事件利用了委托的特点，采用后期绑定机制。声明了某个事件的类，本身不必提供该事件的实现。它可以放心的预先编写代码，并在合适的时机触发该事件。

事件还利用了委托的多播性质，允许不止一个订阅者订阅该事件。即：单个事件委托可以提供多个实现方法。事件被触发时，多个实现方法会被依次调用。

事件的典型的应用场景有：某个按钮被点击、设备连接的连上与断开、收到有人给你发的消息等等。

如何声明事件：

- 只能用作类的成员
- 添加`event`关键词
- 该成员的类型必须是一种委托类型

例如：

```c#
public event EventHandler OnConnected; //声明OnConnected事件
```

上述例子中，定义了一个名为OnConnected的事件。该事件用于在设备建立连接时，向事件的订阅者发起回调。

我们来查看EventHandler的定义：

```c#
public delegate void EventHandler(object sender, EventArgs e);
```

可见，EventHandler是一个委托类型。它描述了一个没有返回值，包含两个参数的方法。两个参数中，第一个object类型的参数，为引发该事件的对象；第二个EventArgs类型的参数，为引发该事件时的额外参数。

虽然任何委托类型都可以用于定义事件，但是**一般而言，事件是EventHandler类型或者EventHandler\<TEventArgs>(C#2.0)类型的**。

EventHandler\<TEventArgs>作为泛型版本，被更多的使用。其中，泛型参数TEventArgs的约束条件（C#2.0，[泛型约束](#泛型约束)）为：必须是EventArgs类的子类。我们看到EventArgs类事实上是一个空类，不包含任何成员。通常我们会继承EventArgs类，并使用泛型参数为该派生类的泛型版本的EventHandler\<子类>来声明事件，以便在事件触发时使用该派生类传递额外参数。

回到上面的例子。声明OnConnected事件后，在编写类库的时候，可以在设备连接成功的时候触发该事件，通知到所有订阅者：

```c#
//代码运行到此处，已经成功连接了设备
if (OnConnected != null)
{
    OnConnected(this, EventArgs.Empty);
}
```

在声明了事件的类中，一般不必提供此事件委托的具体实现。

而对于该类的使用者 —— 一般为其他类，在创建了该类的对象后，可以给该事件添加实现方法，从而实现对事件的订阅。接上例：

```c#
Device device = new Device("SomeID"); //声明设备类的对象，该类定义了OnConnected事件
device.OnConnected += ConnectedMethod;  //ConnectedMethod是一个符合EventHandler委托定义的方法
device.Open(); //调用Open方法后，设备会开始建立连接。在建立成功时，将引发OnConnected事件。此时，此处指定的ConnectedMethod方法就会被调用。
```

由于委托即使为null也可以使用`+=`运算符，因而事件的订阅者不必确定自己是否为第一个订阅该事件的。实际上，由于使用`=`运算符会覆盖所有的其他订阅，因而一般不推荐使用`=`进行绑定回调的操作。

事件也具有访问器，并且可以重写访问器。但是注意，事件与属性不同，它不具备get和set访问器。取而代之的是，它拥有`add`和`remove`访问器。

重写`add`和`remove`访问器，使用这种形式的定义：

```c#
private EventHandler onConnected; //事件背后的实现字段
public event EventHandler OnConnected  //定义事件，并重写访问器
{
    add { onConnected += value; }
    remove { onConnected -= value; }
}
```

在`add`和`remove`访问器内都可以使用`value`关键词。

同属性一样，重写了访问器的事件，也需要背后的实现字段支撑。访问器内直接调用事件的访问器也可能引发无限递归。

另外一点，一旦你重写了`add`、`remove`访问器，事件本身便只能被放在`+=`和`-=`的左侧了，甚至无法放在`=`的左侧。而如果需要调用（触发）事件，只能通过背后的委托类型的实现字段来操作。

> 因为没有委托的概念，Java同样也没有事件的语法概念。可以参考前面例子中实现多播委托的方式实现事件。

## 运算符（Operator）

这里仅仅列出一些C#独特的运算符语法

### 特色运算符

#### @符号

`@`符号的两个用途：

1. 可以作为变量的名称前缀。可以用来解决变量名与系统关键词冲突的问题。

    注意：`@`不被视作变量名称的一部分。例如，使用nameof运算符（C#6.0引入）计算变量名称时，或者做对变量做JSON序列化时，`@for`都会被视为名称为`for`。

2. `@`作为字符串常量的前缀，表示非转义字符串。

    非转义字符串（或称原义字符串），不会转义\符号，也支持在字串内换行。`@`字符串仅仅会转义两个双引号 —— `""`。

    ```c#
    string originString = @"Dear 大家:
        欢迎来到""C#的世界""
    请查看样例：D:\Sample\";
    Console.WriteLine(originString);
    //输出结果为：
    //Dear 大家:
    //    欢迎来到"C#的世界"
    //请查看样例：D:\Sample\
    ```

    > 这与Java在12版本引入的文本块有些类似，文本块使用三个连续的`"`包裹，中间可以换行。这明显是参考了python的语法。不过文本块并不像python那样支持内插。C#也要到C#6.0以后才支持字符串内插。

#### default运算符

`default`运算符可以用于计算任意类型的默认值：

```c#
int a = default(int);  //结果为 0
string b = default(string);  //结果为 null
```

default作用于值类型，返回该值类型的`0`值（例如：int为0，bool为false）；作用于引用类型，返回null。

default运算符作用于struct类型时，将得到所有字段均为default值的该结构类型对象。struct包含嵌套时，每一层struct也都会如此。

default运算符，也可以作用于接口。它将返回`null`。

default运算符，在给泛型类型赋初值时十分有用。在泛型类型为值类型和引用类型时可获取到不同的默认值。（C#2.0）

C#7.1之后，支持[default文本](#C#%207.1的改进)，可以自动进行类型推断。

> 因为Java的泛型类型不能是int、boolean等基本类型，因而Java的泛型对象并不存在默认值不同的情况（因为泛型对象一定可null，所以默认值必然为null）。因此，Java没有，也没必要有default运算符。

#### null判断运算符

`??`是一个二元运算符，左值必须为可null类型

它的含义为：

1. 左值如果为null，则表达式返回右侧的值
2. 左值如果不为null，则表达式返回左侧的值

注意，左侧类型需为右值类型的协变类型、或者可隐式转换为的类型。表达式返回的类型为左值的类型。

```c#
int? a = null; //Nullable<int>类型，C#2.0引入
int? b = a ?? 1;  //b的值为1
```

### 运算符的特色语法

相较于Java，C#有以下特色语法：

#### 索引器（Indexer）

C#允许开发者，使用类似访问数组的方式，来访问对象内的元素

索引器的定义，如下形式：

```c#
public class SomeList
{
    object[] objs = new object[100];
    public object this[int index] 
    {
        get { return objs[index]; }
        set { objs[index] = value; }
    }
}
```

其中，`this[]`是索引器定义的关键语法。

索引器内必须要指定getter和setter。

上述例子定义了一个使用单个int类型的索引键（key）、数据类型为object的索引器。其中，索引键的数量可以是多个，使用语法与使用多维矩阵数组相同。

一个类支持同时定义多个索引器。不同的key数量，或者不同的key类型，视作不同索引器，可以并存。

定义了索引器之后，就可以像使用数组一样，使用索引器来操作对象：

```c#
SomeList someList = new SomeList();  //这里假设someList已经包含了一些元素
object firstItem = someList[0];  //调用索引器的getter，获取元素
someList[0] = new object();      //调用索引器setter，设置元素
```

对于了实现多种索引器的类，多种索引器可以同时使用：

```c#
SomeCollection someCollection = new SomeCollection();   //这里假设someCollection已经包含了一些元素
string item0 = somecollection[0]; //索引键为int类型，数据类型为string的索引器
bool itemA = someCollection["a"]; //索引键为string类型，数据类型为bool的索引器
somecollection['c', 1.0] = 7;     //索引键为char和float类型，数据类型为int的索引器
```

> 从功能上讲，索引器与Java的List等接口的get，set方法作用相同。因为有索引器语法，且C#的List、Dictionary等系统类均实现了索引器，在使用List、Dictionary等列表、集合类型获取和设置元素时，可以使用更简洁的语法，提高代码美观度。而在初始化器（C#2.0引入）和索引初始化表达式（C#6.0引入）语法中，这种代码表现力的差异更加明显。

#### 运算符重载（Operator Overloading）

跟C++一样，C#允许类对运算符进行重载

**可重载**的运算符有：

- `+`, `-`, `!`, `~`, `++`, `--`, `true`, `false` 等一元运算符
- `+`, `-`, `*`, `/`, `%`, `|`, `&`, `^`, `<<`, `>>` 等二元运算符
- `==`, `!=`, `<`, `>`, `<=`, `>=` 等二元比较运算符

**不可重载**的运算符：

- `&&`和`||`作为关系运算符，不可以重载。
- 合并赋值运算符：`+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`，不可被重载。
- `^x`, `x=y`, `x.y`, `x?.y`, `c?t:f`, `x??y`, `x??=y`, `x..y`, `x->y`, `=>`, `f(x)`, `as`, `await`, `checked`, `unchecked`, `default`, `delegate`, `is`, `nameof`, `new`, `sizeof`, `stackalloc`, `switch`, `typeof`, `with`这些运算符不能被重载。

运算符重载方法，必须满足以下条件：

- 必须是`static`方法
- 方法名为`operator`关键词后面跟上运算符（可以有空格）
- 不能返回`void`
- 参数个数必须与原运算符的参数个数相同，即一元运算符参数只能是1个，二元运算符参数只能是2个
- 参数中，至少有一个是本类的类型
- 如果重载了`==`，则必须也重载`!=`；同理`<`和`>`也必须一起重载，`<=`和`>=`也必须一起重载。否则编译器会报错。

重载运算符的返回类型，不必是本类类型。

另外，这里有一个有趣的细节：`true`和`false`的operator也是可以重载的。配合比较运算符的重载（事实上比较运算符也可以返回非bool类型）。可以让类型进行逻辑运算。但是，除非你是用作科学运算，并且有明确的数学工具作为支撑，否则非常不建议这么干，这会降低代码可读性。

在重载`==`时，一般建议同步重写Equals方法，以便符合一致性要求。如果重载`==`而不重写Equals方法，编译器会给出警告，但不是报错。

> **运算符的重载特性，是大多数开发者在最初对比Java和C#时，最快感受到的语法差异冲击。**

以两个例子来看看，运算符重载带来的酣畅淋漓的好处：

##### string的`==`

系统类库已经对string类做了`==`运算符的重载。因此，在C#中，使用`str1 == str2`来判断字符串相等时没有任何问题的。这也符合大多数语言的语义习惯。

> 作为C#开发者，首次接触Java时，非常容易犯的错误就是用`==`来判断字符串相等。因为Java中对于引用类型，`==`事实上仅仅判断了两个引用对象是否指向同一块内存区域。在Java中，只能用equals方法进行字符串相等判断。这也是许多CShaper刚刚转Java时，吐槽最多的地方。

##### DateTime的`+`、`-`、`>`、`<`、`>=`、`<=`

两个DateTime对象相减，可以得到一个TimeSpan类型的对象，该对象表示度过了多长时间。

DateTime对象`+`或者`-`一个TimeSpan对象，可以得到一个新的DateTime对象，为加减时间差之后的时间。

两个DateTime对象可以直接通过`>`、`<`、`>=`、`<=`等来比较先后。

```c#
DateTime now = DateTime.Now;  
DateTime timeSince = new DateTime(2021, 12, 24, 18, 0, 0);  
TimeSpan ts = now - timeSince;  //获取时间差
Console.WriteLine(ts.TotalSeconds); //打印度过了多少秒，包含小数

TimeSpan addOneDay = new TimeSpan(1, 0, 0, 0); //一天后
DateTime tomorrowSameTime = now + addOneDay;  //加上1天
Console.WriteLine(tomorrowSameTime.ToString("yyyy-MM-dd HH:mm-ss")); //打印明天的这个时间

bool isBefore = tomorrowSameTime < now;  //使用<号比较时间先后
```

PS: 事实上，现在的项目中，大多用DateTimeOffset结构来替代DateTime。DateTimeOffset拥有更强的时区控制，可以避免一些因为时区导致的问题。

> Java要实现时间的加减法，大体有三种方式：
>
> - 使用Date类时，仅靠Date类不够，还必须使用Calendar类。Calendar类在调用方法进行时间加减时，其表达方法相当反人类，你无法只调用一个方法就将时间增加1天零3小时21分7秒。
> - 使用时间戳，对时间戳直接计算。显然，这也不够humanity。
> - 使用java.time包下面的类，例如LocalDateTime。该包下面的类相对人性化一点。但是它的加减计算仍然需要通过方法调用。由于语言的机制无法支持`+`/`-`运算符。

综上，通过运算符重载，可以书写出更贴近自然语言的代码。从而使得代码更加易于理解，更有利于维护。

#### 自定义类型转换（User-Defined Conversion Operator）

自定义类型转换，也是很好用的语法。是省事儿的利器。

先看下系统默认的类型转换：

```c#
int x = 0;
double y = x;  //隐式类型转换
double z = (double)x;  //显式类型转换
```

而对于自定义的类，C#也允许开发者定义自定义的类型转换

类型转换方法的定义形如：

```c#
public static implicit operator SomeClass(byte byteValue) { ... }  //隐式类型转换
public static explicit operator int(SomeClass someClassObject) { ... }  //显式类型转换
```

类型转换方法需要满足以下条件：

- 必须是`static`方法
- 必须指定是隐式（`implicit`）还是显式（`explicit`）
- 包含`opertaor`关键词
- `operetor`关键词后面跟要转换返回的类型名称，该方法不必像其他方法一样声明返回类型，方法名称就是返回类型。
- 参数只能有一个
- 参数或者方法名（即返回类型）中，至少有一个是本类类型

注意：

- 作为方法名兼返回类型，别名与完整名称是等效的。以下三者是同一个类型转换方法：
    - `public static implicit operator int(MyClass obj)`
    - `public static implicit operator Int32(MyClass obj)`
    - `public static implicit operator System.Int32(MyClass obj)`
- 从一个类型到另一个类型的转换，只能指定隐式的或者显式其中之一，不能同时声明两者，会冲突。

下面我们来举个常见的应用场景作为例子。

考虑常见的Result类:

```c#
public class Result
{
    public int Code { get; set; }  //此处写法为自动属性，C#2.0会讲到。且此处用枚举会更好。这里仅作示例
    public string Message{ get; set; }  
}
```

常用来作为Web接口的返回：

```c#
public Result SomeOperation()
{
    Result rsl = new Result();
    bool successful = doSomeThing();
    if (successful)
    {
        rsl.Code = 0;
        rsl.Message = "操作成功";
    }
    else
    {
        rsl.Code = -1;
        rsl.Message = "操作失败";
    }
    return rsl;
}
```

上述例子极具代表性。我们可能大部分时候只会返回固定的两种组合：返回Code为0，且Message为“操作成功”；返回Code为-1，且Message为“操作失败”。

因此，我们考虑给Result类增加如下的隐式类型转换

```c#
public static implicit operator Result(bool success)
{
    //此处使用了初始化器，用于在new出一个对象的同时，给对象的属性赋值。C#2.0引入，以后我们会讲到
    return success 
        ? new Result { Code = 0, Message = "操作成功" }
        : new Result { Code = -1, Message = "操作失败" };   
}
```

于是，Result类就实现了从bool类型到Result类型的隐式类型转换。对于原先的SomeOperation方法，便可以简化成这样：

```c#
public Result SomeOperation()
{
    bool successful = doSomeThing();
    return successful;  //会触发隐式类型转换
}
```

可以看到，我们可以通过类型转换，在适当场景下减少代码量。

> Java不支持类型自定义转换。要达到类似效果，请实现一个专用处理方法，用于将传入的bool转换成Result。在每个需要做类型转换的地方调用该方法。

> 仅仅针对上述例子的话，Java可以直接使用枚举类型实现。但是，对于更普遍使用的 —— 包含数据返回的Result，则无法用枚举实现。因为要用到泛型，这里就不举例了。

## 语句（Statement）

### lock

之所以提到`lock`语句块，一是因为它是语法级别的多线程互斥锁。二是几乎\.Net的面试都会被问到。

lock块是一段语句块，它在同一时间仅允许一个线程进入该块。

```c#
lock (x)
{
    //做一些只能单线程进行的操作
}
```

lock为语法级别的，使用起来非常简单，所以深受欢迎。

在使用lock时，仍然有一些注意事项：

1. 用于lock的对象只能是引用类型
2. 用于lock的对象应当避免是public的，以免超出预期控制范围
3. 避免lock string类型的对象。这是\.Net的机制所决定的。在\.Net中，相同的字符串会指向同一块存储区域，即使是计算后得来的字串（因为string是不可变类型）。
4. 避免lock(this)。

> Java的对照物为`synchronized`，而且它可以使用在更多的地方。
>
> - synchronized可用作开启语句块，用法于lock相同，作用也一致。不同于lock一般要避免lock(this)，synchronized则一般直接synchronized(this)。
> - synchronized还可以用于修饰方法，表明整个方法均满足线程互斥，相当于整个方法被synchronized(this)包裹。
> - synchronized还可用于修饰静态的方法，同样表明整个方法均满足线程互斥。但此时不再限制在对象内，任何对该方法的调用都是互斥的。也就是说，如果你是使用对象调用的此静态方法，它表现为对所有对象都互斥。
> - synchronized还可以使用synchronized(类名.class)，此时这个类的所有静态方法都会使用互斥锁。

### 说明注释（文档性注释，Documentation Comment）

C#的说明注释，格式为///开头的一段XML

- 说明注释的每一行都是以三个/开头（可以多，但不可以少）
- 说明注释的是XML格式的，需要符合XML定义。例如：标签需要有开和关。

使用了说明注释描述的类、方法、参数等，在被引用时，IDE会给出说明提示。

说明注释举例：

```c#
/// <summary>
/// 随机选择一个元素样本
/// </summary>
/// <typeparam name="T">元素类型</typeparam>
/// <param name="source">待选择样本</param>
/// <returns>随机选择的样本</returns>
public static T SelectRandom<T>(this IEnumerable<T> source) { ... } //此处定义了扩展方法，扩展方法在C#3.0引入
```

说明注释可在编译设置中启用生成XML文档的情况下，自动生成XML描述文档。该文档有很多用途，例如：

- 打成Nuget包后，如果存在XML文档，引用者在使用类库时，IDE会给出说明提示。
- Swagger组件可以直接读取XML文档内容，自动生成Swagger文档。

> To CShaper：做为对比，Java的说明注释为 /**开头， */结尾的一段。每一行都是\*开头，具体section则以@开头的。

> ```java
> //==Java==
> /**
> * 计算平方
> * @param num 要计算的数
> * @return num的平方
> */
> public double square(double num) { ... }
> ```

### 预处理指令（Preprocessor Directive）

与C++的宏指令一样，以`#`开头的指令为预处理指令，是工作在编译阶段的指令。该指令只会影响编译器工作，不会生成为IL代码。作用是告诉编译器应该怎么做。

这里只讲两组常用的指令：

#### #define和#if

`#define`指令用于定义标记（类似于C++的宏定义）

`#if`指令用于判断标记是否存在，对应的指令还有`#else`、`#endif`

典型的应用场景：Debug模式判断。

在Debug模式下，当前编译上下文会定义`DEBUG`标记。可以利用`#if`来插入仅Debug模式下可见的调试代码。

例如：

```c#
#if DEBUG
bool flag = true;
#else
bool flag = false;
#endif
```

则在Debug模式下，flag为true。

再次强调一下：#if的判断发生在编译阶段。因而，分支未命中的那部分代码，根本不会被编译进dll或exe。如上例中，IL中只会出现`bool flag = true;`编译后的代码。`bool flag = false;`则不会被编译。

#### #region

`#region`为区域折叠标记，对应的结束标记为`#endregion`。区域可以提供名称。

被区域折叠标记包裹的代码，在IDE中可以作为一个整体折叠起来。

这在拆分较大的类时非常好用。可以使代码看起来更整洁。

```c#
//在IDE中，下面的#region到#endregion之间的代码可以折叠为一行。折叠后的位置仅显示区域名称“私有方法”
#region 私有方法
//在这里定义一些私有方法
#endregion
```

## 特性（Attribute）

C#中的特性，与Java的注解（Annotation）是同义词。

特性是一类特殊的类。它标记在特定位置，用来给类、方法、参数、返回值等添加额外的声明、元数据信息。

定义特性：

- 声明一个类，继承自Attribute类，该类是一个抽象类，是所有特性的基类。
- 在该类上标注AttributeUsageAttribute特性，该特性用于指明所声明的特性类的作用目标、是否允许多重标注、是否允许派生类继承等信息。
    - AttributeUsageAttribute的构造器含一个参数，表示允许的作用目标。它是一个AttributeTargets类型的位枚举：
        - Assembly，值为0x1，作用于应用程序集
        - Module，值为0x2，作用于模块
        - Class，值为0x4，作用于类
        - Struct，值为0x8，作用于结构
        - Enum，值为0x10，作用于枚举
        - Constructor，值为0x20，作用于构造器
        - Method，值为0x40，作用于方法
        - Property，值为0x80，作用于属性
        - Field，值为0x100，作用于字段
        - Event，值为0x200，作用于事件
        - Interface，值为0x400，作用于接口
        - Parameter，值为0x800，作用于参数
        - Delegate，值为0x1000，作用于委托
        - ReturnValue，值为0x2000，作用于方法的返回值
        - GenericParameter，值为0x4000，作用于泛型类型参数（C#2.0）
        - All，值为0x7FFF，即等于上述所有位枚举的按位或，作用于上述任何目标
    - AttributeUsageAttribute包含bool类型属性AllowMultiple，表示是否允许在同个元素上标注多次
    - AttributeUsageAttribute包含bool类型属性Inherited，表示是否允许派生类或派生类对应元素继承此特性
- 规范而言，特性类的类名，一般以Attribute结尾

```c#
[AttributeUsage(AttributeTargets.Property | AttributeTargets.Field | AttributeTargets.Parameter, Inherited = false)] //指明AllowNullAttribute的作用对象为属性、字段或者方法的参数。并指定不允许派生类继承该特性
public sealed class AllowNullAttribute : Attribute
{
}
```

使用特性:

- 使用特性的语法为`[特性]`，标注在修饰目标之前。
- 如果要同时使用多个特性，既可以使用`[特性1][特性2]`的语法，也可以使用`[特性1, 特性2]`的语法
- 如果特性类有含参构造方法，则可以使用语法`[特性(构造器参数列表)]`调用。
- 如果特性类包含公开属性，可以在使用特性时指定属性值，语法为`[特性(构造器参数列表, 属性1 = 值1, 属性2 = 值2, ...)]`。但是需注意，能够用此语法指定的属性值，只能是编译时常量、或者数组的初始化表达式（C#2.0，[初始化器](#初始化器（Initializer）)。不知为何，对于数组，此处不支持直接使用`{}`这种最简形式）。如果属性的类型无法使用常量进行赋值，则无法通过上述方法在使用时指定属性值。
- 如果特性类以Attribute结尾，则使用特性时可以简写：省略Attribute后缀。

```c#
public class Test
{
    [AllowNull]  //省略了Attribute后缀
    private string name;

    [AllowNullAttribute, CheckPhone] //同时使用两个特性
    private string phone;

    [JsonProperty("no")] //使用具有含参构造器的特性
    private int number;

    [Document("obj的文档", Url = "http://doc.somedomain.com/obj")] //采用DocumentAttribute的一个string参数的构造器，同时指定其属性Url的值
    private object obj;
}

```

> Java的注解，虽然与C#的特性同义，但是也有不少差异。
> Java的自定义注解的声明和使用：
> - 声明自定义注解：
>     - 通过`@interface`关键词，因而注解是一个特殊类型，而非class。它默认继承Annotation接口，并且不能继承和实现其他类和接口。
>     - 注解类只能是public或者friedly（即无修饰符）的，
>     - 定义注解有者独特的语法。注解中的字段被称之为元素。定义时以`()`结尾，圆括号内不能有参数。并且可以在其后面紧跟default关键词提供默认值。元素的类型只能是简单数据类型、String、Class类（大体相当于C#的Type类）、枚举、注解和上述类型的数组。
>     - 使用`@Target`标注注解的作用目标。它是个ElementType类型的枚举，可以取值的范围：
>         - TYPE：作用于类
>         - FIELD：作用于字段 
>         - METHOD：作用于方法
>         - PARAMETER：作用于方法
>         - CONSTRUCTOR：作用于构造器
>         - LOCAL_VARIABLE：作用于局部变量
>         - ANNOTATION_TYPE：作用于注解类
>         - PACKAGE：作用于Package
>         - TYPE_PARAMETER：作用于泛型的类型参数
>         - TYPE_USE：作用于任何目标，即上述所有目标
>     - 使用`@Inherited`标注注解是否允许派生类继承
>     - 使用`@Retention`来标识注解的生存周期。它是个RetentionPolicy类型的枚举，支持：
>         - SOURCE：仅在源码中有效，编译时被丢弃（请类比预处理指令）
>         - CLASS：默认值。指编译后存在于.class的字节码文件中，可以用于某些工具对.class文件进行动态修改。但不会被加载到内存中，无法在运行时获取该注解。
>         - RUNTIME：最常用的生存周期范围。编译后在.class字节码中，会被加载到JVM中，并且可以在运行时通过反射获取。
>         > 对比之下，C#没有这样的机制。所有特性都是运行时可见的，相当于RUNTIME。
> - 使用注解
>     - 通过`@注解名`使用注解。
>     - 未提供default值的元素，必须在使用时指定值。有default值的则可以省略。
>     - 如需要指明元素值，单个元素时可以使用`@注解名(值)`，多个元素时可以使用`@注解名(元素1名称 = 元素1值, 元素2名称 = 元素2值, ...)`。
>     - 对数组类型的元素指定值：若只有一个元素，可以直接指定单个元素的值；若有多个元素，可以通过`{项1, 项2, ...}`来指定值。
> - 举例
>     ```java
>     //==Java==
>     @Target({ElementType.METHOD, ElementType.TYPE})  //该注解可作用于方法或类
>     @Retention(RetentionPolicy.RUNTIME)  //该注解是运行时可见
>     public @interface AutoLog {  //定义还有两个字段元素的注解@AutoLog
>         String name();  //name没有默认值，使用时必须指定值
>         int[] levels() default {0, 1}; //levels有默认值，使用时可以省略值
>     }
>     //使用注解，作用于类
>     @AutoLog(name = "测试类", levels = 0) //指定元素的值，其中level是数组类型，因而既可以直接指定单个元素值，也可已用{}指定多个元素值
>     public class Test {
>     }
>     ```

### 显式指定特性的目标

特性的作用目标，也可以显式的指定。语法是`[作用目标:特性1,特性2...]`。

可以指定的目标：

| 关键词 | 含义 |
| --- | --- |
| assembly | 整个程序集 |
| module | 当前程序集模块 |
| field | 字段 |
| event | 事件 |
| method | 方法， 或属性的访问器 |
| param | 方法参数，或setter的参数 |
| property | 属性 |
| return | 方法、索引器、getter返回值 |
| type | 结构、类、接口、枚举或委托 |

例如：

```c#
[method: Validated] //指定作用于方法
int Method1(){ return 0; } 
int ConvertInt([param:NotNull] string data) { return 0; } //指定作用于参数
[return : NotNull] //指明作用于返回值
public string CombineNames(string firstName, string lastName) { return string.Empty; }
```

assembly和module作用域比较特殊。绝大部分的特性作用于特定的语言元素，但是目标为assembly和module的特性作用于应用程序集和模块。例如：指定应用程序集的版本，可以这么指定

```c#
[assembly: AssemblyVersion("1.0.0.0")]
```

### 特性中的@符号

特性类的Attribute后缀不是强制要求，但是以Attribute作为后缀的特性在使用时可以省略后缀。因而，考虑一种特殊情况：

```c#
[AttributeUsage(AttributeTargets.Class)]
public class Info : Attribute
{
   private string information;

   public Info(string info)
   {
      information = info;
   }
}

[AttributeUsage(AttributeTargets.Method)]
public class InfoAttribute : Attribute
{
   private string information;

   public InfoAttribute(string info)
   {
      information = info;
   }
}
```

上例定义了两个特性。一个是Info，作用于类；另一个是InfoAttribute，作用于方法。

这两个特性，一个带后缀，一个不带。这样定义两个不同的Attribute是合法的（类名不同嘛）。但是要如何分别使用这两个特性呢？

如果仍然采用省略Attribute的后缀的语法，会出现二义性：

```c#
[Info("some string")] //会报错，编译器无法确定调用的是Info还是InfoAttribute
```

此时，调用Info时，在Info前加`@`符即可。而调用InfoAttribute，使用全名。

```c#
[@Info("This is a class.")] //使用@Info调用Info特性
public class Example
{
   [InfoAttribute("This is a method.")]//调用InfoAttribute时使用全名
   public static void SomeMethod()
   {
   }
}
```

## 反射（Reflection）

同Java和绝大多数的高级语言一样，C#也有反射机制。反射其实是个很大的话题，这里只做简要介绍。

### Type类

C#的反射，核心是Type类。

C#中的任何类型，都可以描述为Type类的对象。

对于对象，可以通过GetType方法，获取用于描述其类型的Type对象。该方法定义于object上，任何类型都继承了该方法。这也包括值类型。

而如果不使用对象，想直接通过类型获取描述该类型的Type对象，则可以使用`typeof`运算符。

不同的是，GetType是运行时获取Type对象的，而`typeof`运算符是在编译阶段获取的。

```c#
Type typeInt = 1.GetType();   //通过对象的GetType方法，获取Type对象
Console.WriteLine(typeInt.Name);  //输出为Int32
Type typeInt2 = typeof(int);  //通过typeof运算符，作用于类型，获取Type对象
Console.WriteLine(typeInt2.Name);  //输出为Int32
```

获取Type对象后，可以通过该对象获取该类型的各种信息。如：字段、属性、方法、特性等等。

下面列出Type对象一些常用的方法：

- GetProperties：获取属性列表
- GetFields：获取字段列表
- GetMethods：获取方法列表
- GetCustomAttributes：获取自定义特性列表

> 与Type类对应的Java类是Class类。虽然Java也有Type，但是Java的Type是接口，而Class实现了该接口。通过对象来获取Class对象实例时，需要使用对象的getClass方法（类比GetType）；通过类名获取时，则使用`类名.class`（与typeof运算符作用相同，缺点是泛型类型不可以使用）。
>
> 关于为什么`泛型类.class`不可用，这就是Java的硬伤 —— 泛型类型擦除导致的了。我们会在C#2.0介绍泛型时，作为对比对Java的类型擦除做出介绍。

### is运算符

可以通过`is`运算符，来判断某个对象是不是某个类型。

在如下情况下，`is`运算符返回true

- 对象的实际类型是精确的目标类型
- 对象的实际类型实现了目标接口
- 对象的实际类型是目标类型的派生类型
- 对象拆箱后类型为目标的值类型
- 对象的实际类型隐式继承目标类
- is的右侧是object

因为任何类型都被认为是object类型的，所以任何对象，无论它的类型是某个class、某个struct、某个enum还是某个delegate，判断其`is object`，返回都是true。

对于右侧类型是左侧对象的隐式继承类的情况，`is`运算符都会返回true。如任何enum对象，判断`is Enum`都是true。任何值类型对象，判断`is ValueType`都是true。

这里有个非常特殊的情况：Enum类本身是引用类型的，它继承自ValueType。但是一个Enum类型的对象（由enum类型装箱的来），判断`is ValueType`却是false。

```c#
int a = 1;
bool isInt = a is int; //true
bool isObject = a is object;  //true
bool isValueType = a is ValueType;  //true
bool isStruct = a is Enum;  //false
object obj = a; //装箱
bool isInt2 = obj is int; //true，拆箱后为int
```

```c#
NovelBook novelBook = new NovelBook();  //假设NovelBook类继承自Book类，且实现了IBook接口
bool isNovelBook =  novelBook is NovelBook; //true
bool isBook =  novelBook is Book; //true
bool isIBookImplement = novelBook is IBook; //true
Book book = novelBook;
bool isNovelBook2 = book is NovelBook; //true，判断实际类型
```

> Java对应的运算符是`instanceof`。所不同的是：
>
> - `instanceof`只能用于引用类型，无法用于基本类型。
> - `instanceof`会进行编译器检查，明确无法进行类型转换的会报错，无法编译。C#虽然也会做编译器检查，但是仅仅是给出警告。

### as运算符

`as`运算符类似类型转换，用于将对象转换成指定类型。

`someObject as SomeClass` 等价于 `someObject is SomeClass ? (SomeClass)someObject : (SomeClass)null`

因此，它跟强制类型转换有关，但又不同：

- `as`右侧的类型，只能适用于引用类型，不可适用于值类型
- `as`不会抛出异常，如果无法进行类型转换，会返回null

`as`不同于`is`，在编译器验证时，如果确认对象无法进行到目标类型的类型转换，则会报错。根据上面的等价代码，这点很好理解。

## unsafe上下文

要使用unsafe上下文，必须**在项目的编译设置中勾选允许不安全代码选项**。它在实际项目中使用较少。

unsafe是一个关键词，用于描述一段不安全的代码。它可以修饰类，也可以修饰方法，还可以直接在语句中通过`{}`启用一段代码块。在unsafe上下文中，允许编写非托管的代码，这允许不安全的内存操作：直接使用指针。

```c#
public unsafe class Class1 //在该类内部所有方法内可以使用指针
{
}
public class Class2
{
    public unsafe void DoSomething() { ... }  //在该方法内可以使用指针
}
public class Class3
{
    public void DoSomething() 
    {
        unsafe   //在接下来的unsafe块内可以使用指针
        {
            ...
        }
    }
}
```

关于指针，用过C++的同学一定非常熟悉。

指针是一种指向内存区域的变量，它的变量本身存储的是所指向的内存区域的地址。指针指向的可以是单个数据，也可以是一串数据组成的数组的起始位置。

指针的语法同C++完全一致，声明指针使用`*`，取指针所指区域作为引用使用`*`运算符，取变量的地址使用`&`运算符，取指针所指的struct对象下的字段作为引用使用`->`运算符。

因为直接使用指针时，无法使用垃圾回收机制。因此C#规定unsafe块中的指针不能是引用类型的。换言之，必须是非托管类型的，而且是完全非托管的。具体来说，指针只能是以下类型之一：

- 非托管类型（Unmanaged Type），具体说来，可以是：
    - sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool
    - 枚举类型
    - struct
        - 需要注意，这要求struct内定义的所有字段均不含引用类型。如果有struct的嵌套，则每一层的struct也不能有引用类型
- 指针类型（即多重指针，如`byte**`）
- void类型（即`void*`），表示未知类型的指针

给指针赋值，有三种方式：

- 使用`&`运算符，但需要满足：
    - 运算符的操作数必须是左值类型，即变量
    - 操作数要么是满足上面要求的值类型，要么是值类型的数组元素。如果使用数组元素，则需要固定（fixed）
- 指向数组
    - 可以使用直接分配到栈空间上（使用`stackalloc`）的数组
    - 使用托管数组名赋值，也需要固定（使用`fixed`）。
- 指针赋值给指针

具体来说，如果要使用`&`给指针赋值为数组的某个元素地址，则会遇到问题：因为托管代码中引用类型的地址并非固定的，它可能被GC回收并重新分配。因此我们需要告诉编译器，将这个数组的位置固定在堆空间中，不再变化。这就要求将赋值语句限制在fixed块内。或者，如果你试图创建与C++相似的数组的话，可以直接将数组分配到栈空间内。

例1：

```c#
//下列代码在unsafe上下文中
int x = 1;
int* pX = &x;  //取x的地址
int[] y = new int[100];
fixed (int* pY = &y[0])  //此处必须使用fixed固定，否则编译器报错
{
}
fixed (int* pY2 = y)  //直接赋值为数组，这跟赋值为数组第一个元素的地址含义相同
{
}
int* pZ = stackalloc int[100]; //直接将内存分配在栈上（这样该数组便与C++的数组分配方式相同了）
```

例2：

```c#
//下列代码在unsafe上下文中
string str = "12345678";
fixed (char* pStr = str)  //string依然可以看作char数组
{
    char* current = pStr;
    *current++ = 'a';
    *current++ = 'b';
    *current++ = 'c';
    *current++ = 'd';
}
Console.WriteLine(str);  //输出为 abcd5678
```

`fixed`除了用作fixed块之外，还可以直接给`unsafe`的struct声明fixed的数组。这要求数组必须是sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool之一（注意，跟指针相比，fixed的数组类型不可以是decimal）。此时定义的语法退化为C++的语法：`[]`放在字段名后面，并且必须提供大小，且不能用`new`初始化。它将被分配在栈空间上，与`stackalloc`相同。

```c#
unsafe struct SomeStruct
{
    fixed int data[15];
    public void Test()
    {
        fixed (int* dataPtr = data)
        {
        }
    }
}
```

`fixed`和`stackalloc`也都只能在unsafe上下文中使用。(从C# 7.2开始，`stackalloc`可以分配给Span\<T>，因而可以用于非unsafe上下文了)

PS：事实上，我们会更多使用`IntPtr`和`Marsha1`来进行指针和非托管的内存操作。使用它们无需开启不安全上下文。

> 虽然不是语法级别的支持，但是Java仍可以参考Unsafe类，它也能实现内存的直接操作。同样的，它也很少被用到。

---

洋洋洒洒，啰啰嗦嗦，终于把1.0讲完了。接下来我们将进入到C#2.0。

# C# 2.0 —— 追赶 + 创新

C# 2.0仍然走在追赶Java这位前辈的路上，不过仍然是追赶和创新并存。例如同为泛型，C#对泛型做了优化，使得C#的泛型为“真”泛型。

C# 2.0支持以下语法：

## 泛型（Generic）

C#2.0 正式引入了泛型。这是C#和Java都有的重要的机制。它的灵感明显来源于C++的模板（template），但是要进化得多。C#的泛型支持：

- 泛型类
- 泛型接口
- 泛型方法

```c#
public interface IGenericClass<T> //定义泛型接口
{
}
public class GenericClass<T> : IGenericClass<T>  //定义泛型类，该类实现了泛型接口，此处接口的T是class的泛型参数T传入
{
    public void Add(T data) { } //使用泛型类的类型作为参数的方法
    public void Compare<TOther>(T data1, TOther data2) { }  //定义泛型方法
}
public class MultipleGenericClass<T1, T2, T3> //多个泛型参数
{
}
```

> 语法上，Java与C#相差不大。仅在泛型方法的定义上有所区别：Java将泛型参数放在返回类型前面，而C#
放在方法名后面（跟泛型类定义一致）：
>
> ```java
> //==Java==
> public <T> void add(T data){}
> ```

需要注意：

- 泛型与非泛型的同名类、同签名方法，是两个不同的类、方法。
- 泛型类型个数不一样的类、方法，也是不同的类和方法。

因此，`SomeClass`和`SomeClass`\<T>`是两个不同的类。`SomeClass\<T>`和`SomeClass\<T1, T2>`也是不同的类。这与Java不同。

这里要重点讲讲C#泛型与Java泛型的区别：

> Java其实是“伪”泛型的，它的泛型类型只存在于编译器检查阶段，在进入JVM时会进行对泛型类型擦除：一直擦除到规定的类型上界（指定extends的情况下为extends的类型，否则为Object）。（指定extends的语法叫做泛型通配符，我们在C#的协变和逆变章节中，会作为比较进行介绍。）

> 例如下面的代码：
>
> ```java
> //==Java==
> public class SomeClass<T>{
>     T field;
> }
> ```
>
> 在编译后，T会被擦除至Object类型。因而实际编译的后的类与下面的原始类型等价：
>
> ```java
> //==Java==
> public class SomeClass{
>     Object field;
> }
> ```

> 不信？我们看下面的代码：
>
> ```java
> //==Java==
> SomeClass<String> obj1 = new SomeClass<String>();
> SomeClass<Integer> obj2 = new SomeClass<Integer>();
> System.out.println(obj1.getClass() == obj2.getClass); 
> ```
>
> 上面的代码会输出true。SomeClass\<String>和SomeClass\<Object>在运行时（Runtime）是同一个类。它们都等同于SomeClass这个原始类。

> 因此，在Java中List\<String>和List也是同一个类。你可以用以下的任意方式赋值，均合法：
>
> - `List<String> list = new ArrayList<String>();`
> - `List<String> list = new ArrayList<>();` 
> - `List list = new ArrayList<String>();`
> - `List list = new ArrayList();`

> 其中第二种为使用钻石运算符。下面讲到泛型类型推断的章节时会在对比环节中介绍。

> 使用后两种都会降低泛型的可用性。用List接收会使得List类中含泛型参数的方法无法通过list对象调用。最后一种更甚：无法利用编译阶段的类型检查功能来排除可能存在的元素类型转换错误，因而不推荐使用。

> 在Java中，你无法同时定义两个SomeClass：一个是泛型的，一个是非泛型。

> 泛型的类型擦除还带来一些硬伤，导致泛型类中，想获取泛型的类型相对比较困难：
>
> - 不能使用`泛型类型.class`来获取
> - 只能通过对象，然后利用反射获取其真实类型

而C#的泛型则为“真”泛型。我们看下面的例子：

```c#
Console.WriteLine(typeof(List<string>) == typeof(List<int>));
```

上面的代码输出为**False**。

介绍C#的泛型机制，需要引入两个新概念：

- **封闭类型**（Closed Type）：是指一个包含泛型的类型，它的所有泛型类型均被具体类型确定。它可以被用来实例化对象。
- **开放类型**（Open Type）：是指一个包含泛型的类型，它有至少一个泛型参数还未被具体的类型确定。它不能被用来实例化对象，但用来作为泛型方法、泛型类的参数、返回值类型声明。

事实上，C#中定义泛型类时，定义的是一个开放的类型，该类使用占位符标记需要被替换的泛型类型。

而在实例化具体的泛型类的对象时，需要确定其中的泛型类型，建立一个封闭类型的新的泛型类。因此，你会得到一个根据你选择的类型定制的“类型安全”的类。

回到上例中：

- List\<T>: 开放泛型类，T为占位符
- List\<string>：泛型类型为String的List<>的封闭泛型类
- List\<int>：泛型类型为Int32的List<>的封闭泛型类

通过查看类型全名，我们发现三者的Type均不相同：

```c#
Console.WriteLine(typeof(List<>).FullName);  //List<>指代List<T>的开放泛型类，对于多个泛型参数的集合类则是类名<,,>这种形式
Console.WriteLine(typeof(List<string>).FullName); //List<T>的、泛型参数T为String的封闭泛型类
Console.WriteLine(typeof(List<int>).FullName);  //List<T>的、泛型参数为Int32的封闭泛型类
```

上例代码的输出为：

```
System.Collections.Generic.List`1
System.Collections.Generic.List`1[[System.String, System.Private.CoreLib, Version=6.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e]]
System.Collections.Generic.List`1[[System.Int32, System.Private.CoreLib, Version=6.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e]]
```

使用真泛型的好处是，泛型类型在运行时也是类型安全的。不过，为了解决派生类应用于泛型的问题，必须引入泛型的协变和逆变机制。我们将在C#4.0章节中介绍[协变和逆变](#协变（Covariant）、逆变（Contravariant）)。

### 泛型约束

有了“真”泛型，便可以对泛型类型或泛型方法进行泛型的约束。

泛型约束，又叫泛型类型限定语。它使用`where`关键词，并放在类型声明、方法声明之后，`{}`体之前。语法为：`where 泛型占位符 : 约束类型, 约束类型`。同时，如果有多个泛型占位符，可以使用多个`where`。

```c#
class MyClass<T, U>
where T: class, new()
where U: struct
{
}
```

可用的约束包括：

- class：用于指示泛型类型必须是类
- struct：用于指示泛型类型必须是结构
- 具体类型名：用于指示泛型类型必须是该类型，或者该类型的派生类型，或者该类型的隐式继承类
- 具体接口名：用于指示泛型类型必须实现了该接口
- new()：用于指示泛型类型必须包含无参构造器

多个泛型约束条件是“与”的关系，必须同时满足。

使用泛型约束的好处是，在代码内可以直接使用约束类型进行操作。如：约束泛型类型`T`符合`new()`，则在代码中可以直接使用`new T()`。

### 泛型方法的泛型类型的自动推断

对于泛型方法，如果所有泛型类型都包含在参数中，调用方法时能明确推断每个泛型参数类型的话，可以不必在调用时指明泛型类型。即：可以省略`<>`

例如，对于下述定义：

```c#
public class Client
{
    public void Get<T>(T key) { ... }
    public void GetExtra<T1, T2>(T1 key, T2 extra = null) where T2 : class { ... }
}
```

则有：

```c#
Client client= new Client();
client.Get<int>(1);  //OK，正常的调用
client.Get(1);  //OK，省略泛型类型
client.GetExtra<string, string>("1");  //OK，正常的多泛型参数调用，并省略了默认参数
client.GetExtra("1", null);  //Not OK，编译器报错，无法从null推断出T2的类型。
```

> 虽然本质上没啥联系，但是这里还是想提一下Java泛型在初始化时的一个用法：。在new一个泛型类时，如果前面的定义明确了泛型的类型，后面new的时候可以将该泛型类型省略。形如：`List<String> list = new LinkedList<>();`。这个表达式的好处是，既可以简化书写，又可以兼顾编译器的类型判断。如果书写`List list = new LinkedList<>();`会引起报错，因为左侧无法确定泛型的类型。由于<>很像钻石，因此又叫**钻石运算符**（Diamond Operator）。它的思想跟刚刚介绍的自动类型推断有相似之处。

## 分部类型（Partial Type）

分部类型允许在多处、多次定义同一个类型。

class、interface和struct都可partial。

声明分部类型的关键词为`partial`

```c#
public partial class Eployee
{
    public void Work()
    {
    }
}
//再次定义
public partial class Eployee
{
    public void Relax()
    {
    }
}
```

上述例子中，Eployee被定义在两处，编译器会将它们合并。最终，Eployee将同时具有Work和Relax两种方法。

定义分部类时，可将它们放在不同的文件中、不同的命名空间中、甚至不同的应用程序程序集中。

编译器，会对下列内容进行合并：

- 说明注释（XML注释）
- 实现的接口
- 泛型类型参数的特性
- 类型的特性
- 成员（字段、属性、方法等）

```c#
[Cold]
partial class Mercury { }
[Hot]
partial class Mercury { }
//特性会合并，所以我们的水星有了冷和热两个特性。

partial class Earth : IPlanet, IRotate { }
partial class Earth : IRevolve { }
//接口会合并，所以我们的地球不仅是行星，还会自传和公转。
```

分部类型，有利于拆解较大的类、结构等。

## 匿名方法（Anonymous Method）

匿名方法，允许在不预先定义方法的情况下，在代码中插入一个方法。这在给委托添加实现时非常有用。

匿名方法，有两种实现方式

- `delegate`运算符
- Lambda表达式（C# 3.0引入）

事实上，Lambda表达式才是最常用的方法。因此`delegate`运算符只做简单介绍。

```c#
public delegate int Add(int a, int b); //定义委托

Add add = delegate (int a, int b) { return a + b; };  //定义匿名方法
```

匿名方法中，可以使用当前上下文环境。即：可以使用定义所在位置能够访问到的本地变量。当你这样用时，就可能会产生**闭包**（Closure）。闭包的概念很多语言都有，如Java，JS，Python等等，相信大家都有所了解，这里就不多做介绍了。

### 强类型委托（Strongly Typed Delegate）

讲到匿名方法，这里有必要提及强类型委托。如果你提供了一个匿名方法，要把它赋值给一个委托，但是你又不想事先定义一个委托类型，此时就可以使用强类型委托。

**强类型委托**，又叫**通用委托**，是两组预定义的委托，分别为`Func`和`Action`。`Func`可以用于指代有返回值的方法，而`Action`可以用于指代无返回值的方法。查看其定义：

```c#
//Func委托的官方定义
delegate TResult Func<out TResult>();
delegate TResult Func<in T, out TResult>(T arg);   //in和out是协变、逆变关键词，我们在C# 4.0会将
delegate TResult Func<in T1, in T2, out TResult>(T1 arg1, T2 arg2);
... //一直到T16

//Action委托的官方定义
delegate void Action();
delegate void Action<in T>(T arg);
delegate void Action<in T1, in T2>(T1 arg1, T2 arg2);
... //一直到T16
```

因而，可以很方便的将通用委托与匿名方法结合使用。例如上例，可以简化为：

```c#
Func<int, int, int> add =  delegate (int a, int b) { return a + b; };  //无需预先定义委托来接收此方法
```

同时，基于通用委托，C#支持对匿名方法的自动类型推断。上述代码可简写作：

```c#
var add = delegate (int a, int b) { return a + b; };  //将自动推断出add类型为Func<int, int, int>
```

## 可null值类型（Nullable\<T>）

`Nullable\<T>`，又叫可null值类型。

> 它对应Java的包装器。不同点是，它对一切值类型都有效，包括自定义类型。

它仍然是语法级别的支持，`Nullable\<T>`可以简写做`T?`。

```c#
double? pi = 3.1415926;
int index1 = 0;
int? index2 = index;  //引起装箱
bool? isCorrect = null;
SomeStruct? someStruct = default(SomeStruct); //SomeStruct为struct
```

### 可null值类型的类型判断

这里要特别讲一下，可null值类型的类型判断，它有些特殊。

```c#
int a = 1;
int? b = 2;
Console.WriteLine(a.GetType().Name);  //输出为 Int32
Console.WriteLine(b.GetType().Name);  //输出也是 Int32
```

所以，Nullable\<T>在获取类型时，获取的是其拆箱类型。

同样的，接上例，对于is运算符：

```c#
bool equalA = a is int?;  //int is int?，返回true
bool equalB = b is int;   //int? is int，返回也是true
```

因而，不可以直接使用Type来判断是否Nullable\<T>类型。如果需要判断当前变量是不是可null类型，需要这样：

```c#
bool isNullable = Nullable.GetUnderlyingType(type) != null
```

## 迭代器（Iterator）

迭代器，特指迭代器方法（Iterator Method），用于创建可枚举的序列。是**非常非常非常重要**的。没错，我用了三个“非常”。

一个方法被编译器认作迭代器方法，需要满足：

- 返回为IEnumerable、IEnumerator，或它们的泛型版本接口
- 方法中包含`yield`语句

`yield`语句有两种：

- `yield return`：用于完成一次迭代，并返回迭代值
- `yield break`：用于终止迭代过程

迭代器的执行顺序有些违反常识，举例说明：

```c#
public IEnumerable<int> Some() //定义迭代器方法
{
    Console.WriteLine(1);
    for(int i = 2; i < 5; i++)
    {
        yield return i;
    }
}
public void TestForIterator()
{
    IEnumerable<int> list = Some();  //调用迭代器方法
    Console.WriteLine(0);
    foreach (string item in list)  //调用枚举器
    {
        Console.WriteLine(item);
    }
}
```

读者可以暂停一下，先自行猜测下，上面的代码输出是什么。

\*

\*

\*

我

是

分

隔

符

\*

\*

\*

实际上，代码输出为

```txt
0
1
2
3
4
```

啥？这么违反直觉的吗？

事实上，迭代器具有**延迟执行**的特点。我们来仔细看看，上例中，迭代器是如何工作的：

为了方便描述，我们把上面的代码标上行号。

```c#
[1]  public IEnumerable<int> Some() //定义迭代器方法
[2]  {
[3]      Console.WriteLine(1);
[4]      for(int i = 2; i < 5; i++)
[5]      {
[6]          yield return i;
[7]      }
[8]  }
[9]  public void TestForIterator()
[10] {
[11]     IEnumerable<int> list = Some();  //调用迭代器方法
[12]     Console.WriteLine(0);
[13]     foreach (string item in list)  //调用枚举器
[14]     {
[15]         Console.WriteLine(item);
[16]     }
[17] }
```

执行过程如下：

1. \[1]声明了含有yield语句的Some方法，编译器将认为这是一个迭代器方法
2. TestForIterator被调用，方法在执行到\[11]时，并不会真的触发迭代过程。方法会立刻返回，并开始执行TestForIterator的后续语句。
3. 程序执行到\[12]，打印了`0`。
4. 执行到\[13]，由foreach触发了枚举器遍历，此时迭代器开始工作。进入Some方法开始执行。
5. 执行到\[3]，打印了`1`。
6. 进入\[4]的遍历，在执行到第一条\[6]处的yield return时，Some方法的执行暂停，并把i的值2作为迭代值返回。
7. TestForIterator的foreach拿到了第一个迭代值2，从\[13]继续执行，到\[15]时打印了`2`。
8. 继续执行到foreach循环的下一次遍历\[13]，再次需要从迭代器中取值，此时Some继续被唤起，从\[6]处继续执行。然后进入i的下一次循环\[4]。又一次执行到\[6]的yield return，将3作为迭代值返回。
9. TestForIterator的foreach又拿到了迭代值3，从而继续执行，在\[15]处打印了`3`
10. 继续重复上述步骤，在\[15]处打印了`4`。
11. 这时执行到\[13]，foreach又会去要下一个迭代值，回到Some，执行到\[4]，for的条件已经不满足，于是for结束了。代码执行到了\[8]。这意味着迭代器方法的执行结束了。因而上层的foreach在此刻也结束了，继续执行到\[17]，TestForIterator方法结束。

因而，使用迭代器后，编译器将代码执行顺序进行了重排。调用迭代器方法不是立即执行并将计算结果存入某个IEnumerable对象返回给调用者，而是在迭代时每取出一条数据便交由调用者处理一条。

这里有一个比较有趣的细节：基于上述机制，迭代器方法返回的IEnumerable，并**不是某个具体的实现类**。实际上**没有类和对象来承载**它的返回结果，它是一个一个吐出迭代值的。换句话说，迭代器方法**本身就是个数据源**，并且迭代器的迭代结果不会被集中存储在某个列表里。

我们举另一个更简单的迭代器方法的例子，这会更有利于理解：

```c#
public IEnumerable<int> Some2() //该方法在迭代过程中，依次返回 2、3、4
{
    yield return 2;
    yield return 3;
    yield return 4;
}
```

通过这个例子，你应该能更好的理解“迭代器方法本身就是个数据源”这句话。迭代器方法在`yield return`处返回一个迭代值，因而可以有多个`yield return`，它们会被依次执行。而不像一般的方法只会`return`一次。

我们趁热打铁，再举个终极例子。就算上面的代码没有让你理解，下面的例子一定能令你彻底明白：

```c#
public static IEnumerable<int> GetInfinite()  //0到无穷大的序列
{
    int i = 0;
    while (true)   //没错，我们定义了一个死循环
    {
        yield return i;
        i++;
    }
}
```

要是一般的方法，这里已经弹出编译器警告了：“嘿，哥们，快看！你的代码里有个无法跳出的死循环，你是不是脑袋秀逗了？”。但是，由于将迭代器赋值给变量时他还未执行，而迭代执行的时候迭代器又是一个一个吐出数据的，所以什么时候停止迭代完全可以由调用者说了算。上面的例子我们可以这么用：

```c#
foreach (var integer in infinite)
{
    if (integer > 10)  //大于10则结束迭代
    {
        break;
    }
    Console.WriteLine(integer);
}
```

它的运行结果是：

```txt
0
1
2
3
4
5
6
7
8
9
10
```

程序没有并陷入死循环。

好了，相信到这里，你应该不可能不理解迭代器的工作原理了。

接下来我们聊聊使用迭代器需要注意的地方：

基于上述特点，被迭代器赋值的变量**不会保存方法执行结果**。对于上例中，如果再次调用foreach迭代，迭代器方法会被**再次执行**。

- 这样做的好处是：迭代器方法可以支持连缀，而不必担心每次连缀都会真实的执行一次迭代，可以在连缀完成后一次性执行迭代。这也是LINQ的思想基础。在LINQ中，这个特点在预测用的迭代器被多个查询复用的情况下会非常有用。
- 这样做的坏处是：迭代器中如果进行大量计算要当心重复调用带来不必要性能损失。而如果迭代器中包含对程序状态的修改，则需要当心重复调用导致重复执行更改的问题。切记！切记！

所以，如果你希望重复使用迭代器方法获取的数据，而这些数据又不是零成本的话（比如必须从数据库读取，必须通过计算获得）。最好使用实现了IEnumerable接口的对象，将迭代器的结果固化下来。便捷的方式是使用LINQ的ToList，ToArray等方法。

迭代器为什么很重要？因为大名鼎鼎的LINQ便是基于它的。LINQ因此也有延迟执行的特点。

> 重要：Java的迭代器（Iterator）跟C#中的迭代器（Iterator）不是一个概念！Java的迭代器指类型（Iterator接口）；而C#特指方法（迭代器方法）。Java的迭代器（Iterator）对应的是C#的枚举器接口（IEnumrator）。事实上，迭代器方法是C#特有的语法，Java不存在C#意义上的迭代器。Java的返回迭代器的方法不会出现这种编译器重排，也没有奇怪的执行顺序，同时也没有延迟执行的特点。

## C# 2.0的其他改进

- **getter、setter的单独可访问性**：现在，getter和setter支持使用不同的访问级别：

    ```c#
    public string Name 
    {
        public get { ... }  //公有的读
        private set { ... }  //私有的写
    }
    ```

- **static类**：`static`可以用来修饰类。static的类中只能包含static的成员。
- **数组的协变**：数组支持了协变。但C# 2.0的变种不是完整的功能。完整的功能要在C# 4.0才引入。我们会在C#4.0中，同泛型的[协变和逆变](#协变（Covariant）、逆变（Contravariant）)一起介绍。

# C# 3.0 —— 分道扬镳、放飞自我、跨时代创新

没错，我用了好几个形容词。C#3.0是一个跨时代的版本，它提出了非常多创新、超前的概念。而从这个版本开始，C#也彻底脱离了对Java的追赶，与曾经的老师分道扬镳，走向了独立发展。

这一章，又会比较长。

C# 3.0，支持以下语法：

## 自动属性（Auto-Implemented Property）

自动实现的属性，简称自动属性。是我们现在定义属性时最常用的语法：

```c#
public string Name { get; set; }
```

这样书写的属性，将自动实现`get`和`set`访问器，也不必再提供支撑字段。

> 与之非常类似的是，Java中可以使用Lombok来实现类似功能。使用Lombok中的`@Data`、`@Setter`、`@Getter`注解，标注于类或者字段上，可以自动实现字段的get和set方法。需要注意，要使得使用了Lombok的代码在IDE中获得语法提示，需要安装额外的插件。

## 隐式类型（Implicitly Typed）

`var`关键词用于自动推断变量的类型，可以用简化本地变量的声明：

```c#
int x = 1; //显式类型
var y = 1; //隐式类型

var a = 1; //a为int型
var b = 'c'; //b为char型
var c = "Hello"; //c为string型
```

需要注意：

- 使用`var`声明的变量，依旧是强类型的。一旦对象的类型推断完成，该变量便始终具有该类型，不可改变。
- `var`只能用于本地变量，不可用于类的成员。

> Java在10版本也引入了var关键词，用法一致。

## 初始化器（Initailizer）

初始化器可以在给变量、成员初始化时，快速设置、填充内容。

包含属性的类，可以在初始化同时设置属性的值。

考虑如下类定义：

```c#
public class Dog
{
    public int Age { get; set; } //年龄
    public string Name { get; set; } //昵称
    public Dog() { }  //无参构造器
    public Dog(string name)  //含参数构造器
    {
        Name = name;
    }
}
```

在创建Dog对象时，可以：

```c#
//使用无参构造器时，()可以省略
Dog dog1 = new Dog  //这将调用无参构造器 
{
    Age = 10,
    Name = "旺财"
};  //作为一行语句，此处需要分号
Dog dog2 = new Dog("大黄")
{
    Age = 5
};
```

另外，有一种特殊情况，当一个对象满足下面条件之一：

- 对象是个数组
- 对象实现了`IEnumerable`或者`IEnumerable\<T>`，并且对象有一个公开的（`public`或`internal`）的`Add`方法

则可以使用花括号的初始化器格式，形如：

```c#
int [] array = new int[5] { 1, 2, 3, 4, 5 }; //数组的初始化器
int [] array2 = new int[] { 1, 2, 3, 4, 5 }; //特别的，由于数组的大小不可变，因此使用初始化器可以省略长度
int [] array3 = { 1, 2, 3, 4, 5 }; //更特别的，对于数组，可以支持这种简写形式。

List<int> digits = new List<int> { 1, 2, 3 }; //这会调用List<int>的Add(int)方法
SomeClass someObjects = new SomeClass { {1, "你好"}, {2, "你不好"} }; //这将调用SomeClass的Add(int, string)方法。
```

使用初始化器，可以使对象的初始化变得更加简洁美观。

让我们考虑更复杂的情形，来看看初始化器带来的优势：

```c#
Student student = new Student
{
    Age = 13,
    Name = "小明",
    Scores = { 100, 95, 95 }, //Scores是一个int型数组
    HaveCats = new List<Cat>  //他养了许多猫 
    {
        new Cat { Name = "咪咪" },
        new Cat 
        { 
            Name = "卡卡", //卡卡是我养过的一只猫，后来走丢了
            Hobby = new List<string>
            {
                "爬高",
                "上低", //此处逗号可以保留，不会报错
            } 
        } //同样的，这里可以添加逗号
    }, //同理，此处逗号可写可不写
};
```

> Java没有初始化器的对照物。不过从功能的实现来讲，倒是可以讲讲两个东西：双花括号初始化、Java 9引入的of静态方法。

> 双花括号初始化，语法为new一个对象的同时在后面添加双花括号。在其中调用set、add等方法。我们先来看下用法，然后再说说为什么它只是看似实现了类似功能，本质上与C#的初始化器完全不同。
>
> ```java
> //==Java==
> Person person = new Person() {{
>     setName("张三");
> }};
> ```
>
> 如果要实现上面的Student初始化一样的功能，Java需要这么写
>
> ```java
> //==Java==
> Student student = new Student() {{
>     setAge(13);
>     setName("小明");
>     setScores(new int[]{100, 95, 95});
>     setHaveCats(new LinkedList<Cat>(){{
>         add(new Cat() {{
>             setName("咪咪");
>         }});
>         add(new Cat() {{
>             setName("咪咪");
>             setHobby(new LinkedList<String>() {{
>                 add("爬高");
>                 add("上低");
>             }});
>         }});
>     }});
> }};
> ```
>
> 显而易见，这时代码的可读性已经很差了，书写的复杂度也上升了不少。但这还不是最要命的。
>
> 更要命的是：这样做的含义，其实是创建了匿名内部类（外层括号），然后再在匿名类中执行了实例初始化代码块（内层括号）。因而在这种情况下，非静态的内部匿名类会持有外部对象的引用。而外部对象如果被更广泛的引用到更大的生命周期内——比如作为方法的返回值，并赋值给生命周期更长的对象作为字段值——有可能导致GC无法及时回收内部类的资源。这有可能引起内存泄漏，甚至极端情况下引发OOM（Out Of Memory，即内存溢出）。
> > 关于Java的匿名内部类，我们会在下一个小结的对比中介绍。
> 至此，我们已经发现，它与C#的初始化器虽然可以实现相同的功能，但是完全不是一回事儿。还是不用为妙。
>
> 事实上，很多公司明确要求禁止双括号初始化语法出现在项目中。

> 只针对序列，在Java 9之后，List、Set、Map等接口增加了用于初始化并添加元素的新方法：静态的of方法，of方法的参数是可变参数，可以在初始化时一次性添加多个元素到序列中：
>
> ```java
> //==Java==
> List<String> list = List.of("a", "b", "c", "d", "e");
> ```
>
> 这个与C#针对可枚举对象的初始化器有些许相似，但是：
>
> - 它们只能用于初始化这几种特定接口的序列。
> - 用它们初始化的序列是只读的，不可以再add和remove。
>
> 事实上，of方法也是为了满足函数式编程而出现的。
>
> 所以，还是无法与C#的初始化器相提并论。

## 匿名类型（Anonymous Type）

有了隐式类型和初始化器作为基础，便可以描述匿名类型了。

匿名类型是指你可以定义一个对象，该对象不必是事先已定义的类型。这样做可以在需要使用一个由简单结构组成的对象的场合，不必中断思路先去定义一个类来承载这个对象。

匿名类型的声明如下：

```c#
var anonymousObject = new 
{
    Name = "匿名类型",
    Description = "这是一个匿名类型",
    Levels = new int[] { 1, 2, 3 }
};
```

可见，匿名类型的语法，是在创建一个对象时，只用new，不指定类型。在后面书写初始化器，直接初始化该对象。初始化器中声明的均是该匿名类型的属性。也由于是匿名的，它也只能由var隐式类型接收（由Object接受的话，无法直接使用匿名类型的属性）。

使用匿名类型，编译器会自动生成一个匿名的强类型类。所有反射的操作都可以正常使用。

同时，编译器还对匿名类型做了优化：具有完全相同属性的匿名类型，会被合并成一个相同的匿名类型。

```c#
var a = new { x = 1 };
var b = new { x = 2 };
var c = new { x = 3, y = 3 };
Console.WriteLine(a.GetType().FullName);
Console.WriteLine(b.GetType().FullName);
Console.WriteLine(c.GetType().FullName);
```

结果为：

```txt
<>f__AnonymousType0`1[[System.Int32, System.Private.CoreLib, Version=6.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e]]
<>f__AnonymousType0`1[[System.Int32, System.Private.CoreLib, Version=6.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e]]
<>f__AnonymousType1`2[[System.Int32, System.Private.CoreLib, Version=6.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e],[System.Int32, System.Private.CoreLib, Version=6.0.0.0, Culture=neutral, PublicKeyToken=7cec85d7bea7798e]]
```

a和b的类型完全相同。此时我们将b赋值给a是完全可以的。

```c#
a = b; //OK
```

正因为如此，可以直接创建匿名类型的数组：

```c#
var array = new [] 
{
    new { x = 1, y = 2 },
    new { x = 2, y = 3 },
    new { x = 4, y = 5 },
};  //OK，合法
```

> 这里可以对比一下Java的匿名内部类（Anonymous Inner Class）。事实上，这是Java为数不多的在语法层面超越C#的机制。
>
> C#的匿名类型，只能提供属性及其值，因而匿名类型都是**POCO**（Plain Old CLR Object，对应Java的**POJO**，即Plain Old Java Object）。而Java的内部匿名类，不仅能提供字段、字段的get和set方法，还可以提供实例初始化代码（Instance Initializer Block），甚至可以定义方法和重写方法。唯一的限制是：匿名内部类必须继承一个类，或者实现一个接口，而不能无中生有。
>
> 上述区别使得二者使用的场景并不相同：C#匿名类多用于**临时聚合数据**（C# 7.0后有了更好的方式——元组），而Java的匿名内部类则是用来**临时添加功能**。

> 举例说明：
>
> ```java
> //==Java==
> Person person = new Person() {  //这里花括号是指实现一个内部匿名类，它继承了Person类，与C#的初始化器不是一回事
>     {    //这里是实例化初始化块，是指该内部匿名类的对象被创建时应该执行的语句，相当于构造器。双括号初始化本质上就是利用的这个
>         setName("张三");  //Person类中已经有name字段和setName方法
>     }
>     @Getter
>     @Setter
>     private int age;  //定义了字段，并通过Lombok添加了get和set方法，但是无法被访问到
>     public int computeImaginaryAge() { //定义了方法：计算虚岁，但是无法被访问
>         return age + 1;  //请不要纠结虚岁不是这么算的
>     }  
>     @Override
>     public String toString() {  //重写toString方法
>         return name;
>     }
> };
> ```
>
> 上述代码实际上声明了一个Person的匿名内部类，并对其实例化，然后将其赋值给了Person类型的变量person。person的实际类型为该匿名类型，Person是它的父类。注释中已经列出了上述代码存在的问题：由于内部匿名类使用父类进行操作，在内部类中定义的public方法无法被直接访问到。虽然仍然可以通过反射访问到，但是谁会这么做呢？实际场景中匿名内部类新增的方法会用private修饰。public的方法要么是对父类方法的重写，要么是对接口的实现。

> 匿名内部类的对象实际上隐式的包含了一个字段，用于存储对父类的引用，该字段为`this$0`，可以通过反射读取到。

> 匿名内部类最为好用的场景，在于它可以直接提供一个接口的匿名实现，而不必为此特意提前定义一个类。因而，可以很方便地为一个从未被实现过的接口提供临时的实现。这点比C#要舒坦，C#中没有这样的机制。

> 特别的，在使用钻石运算符时，Java 8之前的版本不可以定义内部匿名类，但是Java 9以后的版本支持定义内部匿名类。

### 匿名类型的属性名称推断

当创建一个匿名类型对象时，具有明确名称的对象、对象的字段或属性等可以直接用于描述匿名类型的属性，而不需要显式的提供`属性=值`的格式。

```c#
int n = 100;
Cat cat new Cat { Name = "喵呜" };
var anonymousObject = new  //该匿名类对象具有两个属性：Name和n
{
    cat.Name,  //自动推断属性名为Name，赋值为cat.Name的值 
    n //自动推断属性名为n，赋值为n的值
}
```

## Lambda表达式

Lambda表达式，简称Lambda，用于描述方法的实现。符号为`=>`。

Lambda有两种形式：

- 表达式Lambda：主体为一个表达式，Lambda在执行时计算该表达式的结果并返回（可以为void）。此时，无需`{}`。格式为：

    ```c#
    (参数列表) => 表达式
    ```

- 语句Lambda：主体为语句块，Lambda根据语句块中return类型确定Lambda的返回类型（可以不return，即void）。此时，使用`{}`包裹，格式为：

    ```c#
    (参数列表) => 
    {
        语句;
        语句;
        ...
    }
    ```

表达式Lambda可以理解为仅包含一条return语句的语句Lambda。（只是可以这么理解，在特定场合下，它们在语法上并不等同）

Lambda才是提供匿名方法实现的最常用方法，举例如下：

```c#
Action writeLine = () => Console.WriteLine();  //0参数
Func<double, double> square = x => x * x;  //1个参数，此时()可以省略
Func<int, int, int> add = (a, b) => a + b; //两个参数
```

注意，Lambda不能指定参数和返回值的类型（C#10.0之前），在使用时，会根据接收的委托类型自动推断参数和返回类型。

Lambda也可以使用当前上下文中的本地变量。因此也同样可能产生闭包。

所有委托类型均可以使用Lambda描述。另外，Lambda还可以用于**自动生成表达式树**。在使用LINQ的查询扩展方法时Lambda被大量使用。它**很重要**。

> Java也有Lambda，语法仅仅是将`=>`改成`->`。Java的Lambda跟随Java8一起推出，时间是在2014年。这比C# 3.0的2007年晚了7年时间。
>
> 我们知道Java是没有委托类型的。那么Java是用什么类型来接收Lambda的呢？
>
> 这又是一场编译器的魔术了。
>
> Java规定了一种接口类型，被称作函数式接口。**函数式接口**是指只有一个需要实现的方法的接口。函数式接口中允许有其它已经提供了默认实现的方法，但未实现的只能有一个。当指定使用函数式接口作为参数、变量类型时，可以用两种方式传递参数和赋值：
>
> - 使用`类名::方法名`的语法，直接将某个类的某个方法作为该接口中待实现方法的实现。该方法必须与接口方法的声明一致。
> - 使用Lambda表达式。此时编译器将Lambda的描述视作该接口中待实现的方法的实现。提供的Lambda需要有与此方法一致的参数列表和返回类型。
>
> 基于编译器的上述魔术，对Lambda的调用被转化成了调用接口对象的方法，从而避免了引入函数指针的概念。
>
> 函数式接口一般都会添加@FunctionalInterface注解。该注解标明此接口是一个函数式接口。编译器会检查该接口是不是只有一个未实现的方法。如果不是，则编译器会报错。
>
> ```java
> //==Java==
> @FunctionalInterface
> public interface MyFunctionalInterface {  //定义函数式接口
>     void method();
> }
>
> public class MyClass {
>     public void forLambda(MyFunctionalInterface impl) {  //函数式接口作为参数
>         impl.method();  //调用接口的方法。
>     }
>     public void test() {
>         forLambda(()->System.out.println("Lambda测试"));  //调用forLambda方法，并使用Lambda描述参数impl，此时Lambda会成为该接口的method方法的实现。
>     }
> }
> ```
>
> Java系统提供了一堆预定义的函数式接口，它们被定义在java.util.function包下。这些接口基本满足了stream编程的需求（Java的stream编程语法类似LINQ的查询扩展方法，本文会在介绍到LINQ的时候做出介绍）。
>
> PS：事实上，函数式接口同样是向函数式编程靠拢的一次尝试。就本质上讲，LINQ和Stream都很函数式，然而无论Java还是C#都并不是函数式的语言。后面我们还会看到两者更多向函数式看齐的更新。

## 分部方法（Partial Method）

分部方法是分部类的扩展。分部方法必须放在分部类中，它允许先声明分部方法的签名，但是不在此提供实现。该方法可由分部类的其他部分来实现。

分部方法在声明时有一些限制：（到了C#9.0这些限制被取消）

- 不能指定修饰符
- 不能返回void
- 不能带out参数

分部方法未提供实现，则会被编译器忽略。（到了C#9.0，要求必须提供实现）

```c#
partial class A
{
    partial string FetchIt(); //此处不提供实现
}
partial class A
{
    partial string FetchIt()  //此处提供实现
    {
        return "拿回来了，给你";
    }
}
```

## 扩展方法（Extension Method）

扩展方法的使用十分广泛，包括LINQ的查询扩展方法也是基于扩展方法。

扩展方法提供了在类型定义之外任意位置扩展类型的功能能力。

扩展方法可用于类、结构、枚举等等等等。

定义扩展方法，需要满足：

- 扩展方法的只能定义在static类中，且自身必须是static方法
- 使用`this`关键词修饰参数，并且this参数只能放在第一个，它标识出是该方法是哪个类型的扩展方法

扩展方法定义如下：

```c#
public static ArticleExtensions
{
    public static int WordCount(this Article article)  //定义Article类的扩展方法WordCount，用于数出单词数量
    {
        return article.Content.Split(new char[] { ' ', '.', '?', '!' },
            StringSplitOptions.RemoveEmptyEntries).Length;
    }
}
```

此定义不在Article内，而是在独立的静态类ArticleExtensions中。这样定义后，Article类的对象便拥有了WordCount这个扩展方法可用。

事实上，单个静态类中，可以定义多个不同类型的扩展方法。

使用扩展方法，可以像使用类型的方法一样：`对象.扩展方法(参数列表)`

上例中，可以这样用：

```c#
Article article = new Article("A Story.txt");
var wordCount = article.WordCount();  //调用扩展方法，调用者本身作为参数列表里的被扩展的对象（即第一个参数）传入方法，因此调用时括号内会少了第一个参数。
```

需要注意，需要引用扩展方法所在的命名空间后，才可以使用该扩展方法。

扩展方法也能当作一般的静态方法使用：

```c#
Article article = new Article("A Story.txt");
var wordCount = ArticleExtensions.WordCount(article);  //当作一般静态方法使用
```

扩展方法也支持泛型。例如我们可以实现一个泛型扩展方法ToJson\<T>，T类型作为被扩展的类型。之后便可以使用`任意对象.ToJson()`将对象转换成Json字串（这个例子中有个细节：ToJson的泛型参数也被省略了，因为调用者就是第一个参数，可以推断出泛型类型）。

另外，扩展方法如果跟既有方法同名，由于静态方法只能是隐藏，无法作为重写，所以：

- 扩展方法与类型自身方法冲突时：将会优先使用自身方法
- 祖先类型拥有相同签名的扩展方法：由于会进行方法隐藏，将使用对象所显式声明类型的扩展方法，而不是实际类型的方法。这适用于各种情况：实际类型拥有自身定义的静态的或非静态的同签名方法；实际类型拥有同签名的扩展方法。这些情况下都不会使用实际类型的方法。
- 多处定义多个同签名的扩展方法（只要不在一个类中定义，编译器便不会报错）：如果它们在不同的命名空间中，使用时可以只using需要使用的扩展方法所在的命名空间，可以正常调用。如果它们在同一个命名空间下，或者使用时同时using了这两个命名空间，则在调用时会引起二义性错误。此时请直接用普通静态方法的语法来调用它们。

> Java没有扩展方法

## 表达式树（Expression Tree）

表达式树，主要提供两种能力：

- 可以在运行时动态**生成**可编译和执行的表达式
- 可以在运行时**分析处理**代码中编写的表达式

### 生成、编译和执行表达式树

对于下列简单的表达式

```c#
int sum = 1 + 2
```

它具体由以下部分组成：

- 左值部分
    - 变量类型声明 `int`
    - 变量名 `sum`
- 赋值符号 `=`
- 右值部分
    - 左操作数 `1`
    - 加法符号 `+`
    - 右操作数 `2`

学过算法的同学应该都知道，我们书写的符合自然语义的表达式为中缀表达式，它无法直接被计算机处理。一般在计算表达式时，需要将中缀表达式转成后缀表达式，这就会用到二叉树。表达式可以表示成一棵二叉树，树的非叶子节点为表达式的运算符，叶子节点为操作数；节点的左侧子节点为左操作数，右侧子节点为右操作数。

上述表达式，如果用C#的表达式树来描述：

```c#
var varibleSum = Expression.Variable(typeof(int), "sum"); //声明int类型的变量sum
var one = Expression.Constant(1);  //声明左操作数常量表达式 1
var two = Expression.Constant(2);  //声明右操作数常量表达式 2
var add = Expression.Add(one, two); //声明将两个常量表达式加起来的表达式 1+2
var assignment = Expression.Assign(varibleSum, add); //声明赋值表达式
```

可见，表达式树与上述二叉树的结构一致。因此构建的方式是先构建叶子节点，然后再通过运算符连接叶子节点构成一个个森林，依次进行下去直到合并成一棵树。

需要注意的是，表达式树是不可变的。一旦生成后，你就无法修改它了。如果需要修改，请考虑复制一棵表达式树，并在复制的过程中替换你要修改的部分。

表达式树是可以被执行的。只需要

1. 用Expression的Lamdba方法来生成一个Lambda表达式的表达式树，以便封装成一个可调用的方法。
2. 编译它
3. 执行

Expression的Lamdba方法返回一个`Expression\<TDelegate>`类型的表达式，它可以被编译为一个方法。因此你也可以将它分配给一个委托变量。

```c#
var expFunc = Expression.Lambda<Func<int>>(assignment); //生成Lambda，expFunc的类型是Expression<Func<int>>
var func = expFunc.Compile(); //编译，并赋值给委托。func的类型是Func<int>
var assignResult = func();  //执行委托，assignResult为int sum = 1 + 2赋值表达式的结果，为3
```

### Expression\<TDelegate>和代码分析

这里有必要特别絮叨一下`Expression\<TDelegate>`。它派生自LambdaExpression，用于描述一个Lambda的表达式。其中TDelegate虽然未指定泛型约束条件，但是一般为强类型委托类型（Func或者Action）。

该类型的对象可以由下列方式创建：

- 使用`Expression.Lambda`静态方法构建
- 直接使用表达式Lambda进行赋值，但是有限制：
    - 只能是“表达式Lambda”，不能是“语句Lambda”
    - 这种赋值要求表达式不能包含赋值运算符`=`

当**直接赋值为表达式Lambda**时，编译器会自动将你的Lambda表达式内容转换成表达式树。开发者因此可以读取表达式树的每个节点，从而进行代码分析。也基于此，表达式树并不仅仅是类库层面的更新，同样也是语法级别的升级。

表达式`1 + 2`，如果直接用表达式Lambda赋值为Expression\<TDelegate>，则可以写作：

```c#
Expression<Func<int>> funcExp = () => 1 + 2;
var rsl = funcExp.Compile()();  //rsl为 3
```

编译器自动生成了`() => 1 + 2`的表达式树，上面的代码等同于:

```c#
Expression<Func<int>> funcExp = Expression.Lambda<Func<int>> (
    Expression.Add(
        Expression.Constant(1, typeof(int)),
        Expression.Constant(2, typeof(int))
    )
);
var rsl = funcExp.Compile()(); //rsl为 3
```

如果需要，你可以分析funcExp内表达式树，实现代码分析。甚至，你可以根据分析结果，按照自己的规则执行新的逻辑，从而实现对表达式的转换。

这十分十分强大！我们下一节讲到[LINQ](#LINQ)时，会看到它在实体框架（Entity Framework）中的应用。

### 生成表达式树的一个情景化的例子

表达式树用于代码分析的例子我们会在LINQ章节中看到；这里我们来看一个动态生成表达式树并执行的例子（情节过于狗血，请自备纸巾）：

假设，因为某些历史原因，你们公司有A、B两套功能重叠的系统。两套系统之前是独立开发的，没有直接联系。两套系统都有自己的用户系统。某一天，你们的老总忽然觉得，维护两套系统需要的成本太高，既然功能是重叠的，为什么不合成一套系统呢？于是，老总给你布置了任务：以A系统为主体，将B系统功能完全实现，然后将B系统迁移至A系统。项目进展很顺利，你们很快进入了数据迁移的环节。这时你发现，其他的数据都很好迁移，唯独用户的迁移存在问题：两套系统用了完全不同的密码校验规则。由于用户密码在库中存储的均为哈希校验值，无法反解出用户的原始密码，因此不可能将密码按照A系统的密码规则重新生成一遍。而因为B系统在完成迁移后会被彻底关停，你也不希望保留B系统的用户系统服务做OAuth授权。

最简单的办法：将B系统的密码校验规则也在A系统内实现一遍，然后根据用户归属系统的标识采用不同的规则进行校验。你也这么做了。项目顺利上线，你拿到了丰厚的奖金，美滋滋。

合并后的A系统由于做了大量优化升级，功能已经十分完善，性能也是杠杠的。虽然A系统仅仅是你们公司内部使用的系统，但是在接纳其他公司的参观学习时，受到了特别关注。很快你们的系统名声鹊起，前来参观取经的公司络绎不绝。此时，你的Boss一拍脑袋，何不将系统打包成产品卖给其他公司，以替代它们那些不太好用的既有系统。于是，你的公司忽然找到了另一条发家致富的道路。

这时，你发现情形变了。每个客户都有自己的既有系统，又都想保留自己的用户信息。但是每个系统可能用的都是不同的密码校验规则，你不可能针对每一家用户的校验规则都去写一段代码实现。于是你考虑，可以通过一段字符串表达式，来描述密码校验规则——你称之为密码表达式。然后通过解析该表达式，用表达式描述的过程来验证密码。

这时候，你祭出了表达式树。你实现了对密码表达式字串的解析，并将其转成表达式树。然后，将表达式树编译并缓存。密码校验时，只需要调用已缓存的编译好的委托，而不必再次解析该字串。

你又这么做了，使得A系统成功产品化。之后，公司通过积极的市场化运作，利用A系统得大卖特卖，赚的盆满钵满。作为主程序员之一，你也拿到了巨额的奖金。因此你得以在一线城市核心地段买了房，从此走向人生巅峰。

上面的故事显然是虚构的，想吐槽的话请忍着。

不过，密码验证表达式的功能确实是我在项目中实现了的。下面是我的部分单元测试代码，读者从中应该能体会出表达式树的作用：

```c#
[Fact]
public void PasswordExpressionCombinedTest2()
{
    var passExp = "sha1(lower(md5($password+$salt))+'_usr'); //密码表达式字串，其中sha1、lower、md5等为预定义的方法，$开头表示变量
    var func = PasswordExpression.Build(exp);  //Build方法根据exp的描述生成表达式树并编译并且缓存，然后返回Func<string, object>的委托对象。已缓存的exp该方法会直接返回委托，不再解析exp。
    var actual = func(new { password = "pwd", salt = "abc" }); //这里的调用使用了匿名类和反射。这样设计的好处是：1. 代码含义更明确； 2. 方便于将数据库的Model直接传入作为参数。坏处是：使用反射，多少会损失点性能。
    var expect = HashHelper.Sha1((HashHelper.Md5("pwd" + "abc")).ToLower() + "_usr"); //按照上述密码表达式字串+提供的参数的实际语义，模拟执行一遍
    Assert.Equal(expect, actual);  //这句是单元测试中的断言，这里是比较模拟执行的期望结果和密码表达式委托的实际执行结果，两个结果字串应该相等。
```

> Java也没有表达式树。

## LINQ

有了迭代器、扩展方法、Lamabda表达式和表达式树这4种语法，LINQ终于可以闪亮登场了。

LINQ —— Language Integrated Query，读作\[link] 。翻译成中文叫集成语言查询。

这是C# 3.0的一颗重磅炸弹。

LINQ试图提供一种抽象，对于可枚举（IEnumerable）、可查询（IQueryable）接口，我们可以用统一的方法来查询其中的元素。这种查询是无差别的，使用者可以不用关心底层数据的存储、获取方式。被查询的数据可以来自一个内存对象，来自迭代器生产的数据，或者来自数据库、硬盘远程取出的数据等等。

LINQ两种语法形式：

- **查询语法**（Query Syntax）——使用[查询表达式](#查询表达式（Query%20Expression）)
- **方法语法**（Method Syntax）——使用[查询扩展方法](#查询扩展方法（Query%20Extension%20Method）)

这两种形式可以组合使用。

查询表达式，在底层上依赖查询扩展方法。编译器会将查询表达式语法转换成对查询扩展方法的调用。因此，两者在性能上没有差异。而且，使用扩展方法可以完成所有查询表达式所能完成的工作。不过，一些功能却只能使用扩展方法来实现。例如：计算元素数量，取元素最大值等等。

LINQ的用途十分广泛，如：

- 内存数组、列表、字符串等查询——LINQ to Objects
- 文件查询——LINQ to IO
- XML文档查询——LINQ to XML
- 实体框架查询——LINQ to Entity
- Elastic Search查询
- Excel查询
- ...

因为十分重要，在开始之前，我要再来强调一次：

**LINQ基于迭代器，因而也有延迟执行的特点！**

下面我们将分别介绍两种语法：

### 查询表达式（Query Expression）

查询语法使用查询表达式，它是语法级别的支持。其形式非常类似sql语句。但是，又与sql有所区别：

```c#
IEnumerable<string> oldCatNames = 
    from cat in cats
    where cat.Age > 10
    orderby cat.Age descending
    select cat.Name; 
```

其中，cats是List\<Cat>类型的。cat是指遍历时取出的每一个Cat对象，其他的部分应该很好理解。上述语句，筛选了所有年龄大于10的猫，并按照年龄倒序排序，然后将这些猫的名字取出来。

注意：由于延迟执行特点，这里在赋值oldCatNames时查询过程并未真正执行。真正的执行要等到枚举器被调用。

查询表达式实际会由编译器转换成对查询扩展方法的调用。

查询表达式有以下特点：

1. 查询的对象为一个可枚举或可查询对象
2. 表达式的返回是一个迭代器
3. 以`from`开头，以`select`或者`group`结尾
4. `from`和`select`、`group`之间中间可以包含`where`、`orderby`、`join`、`let`等子句
5. `from`可以嵌套
6. 可以使用`into`将`select`或`group`的结果存入临时标识
7. 过程中每一步都是强类型的，它是“流式”的

查询表达式的可用关键词如下：

| 子句 | 说明 |
| --- | --- |
| from | 指定数据源和范围变量（类似于迭代变量，配合in关键词） |
| where | 提供由逻辑关系运算符（&& 或 \|\|）分隔的一个或多个布尔表达式作为筛选条件 |
| select | 指定执行查询时，返回序列的元素类型 |
| group | 根据指定的Key对查询结果分组 |
| into | 将join、group、select子句的结果存入临时标识 |
| orderby | 根据元素类型的默认比较器，对查询结果进行升序或降序排序 |
| join | 根据指定匹配条件，联接两个数据源 |
| let | 引入范围变量，在查询表达式中存储子表达式结果 |
| in | from和join子句中的上下文关键字，in前为迭代变量，in后为元素序列 |
| on | join子句中的上下文关键字，用于提供join条件 |
| equals | join子句中的上下文关键字，用在on中，比较两个序列中对应元素 |
| by | group子句中的上下文关键字，用于提供group的聚合键 |
| ascending | orderby子句中的上下文关键字，指示升序排列 |
| descending | orderby子句中的上下文关键字，指示降序排列 |

在官方文档中，建议使用LINQ时优先选用查询语法，而不是方法语法。但是，从实际项目经验看，查询表达式的使用率远不如马上要介绍的查询扩展方法。原因是我们认为方法语法的语义也足够明确，可读性与查询语法不分伯仲；并且因为有些功能必须使用方法语法完成，全程使用方法语法反而会增加代码的一致性和连贯性。因此，关于查询表达式这里就不再继续展开来讲了，感兴趣的请自行查询官方文档。

> Java没有这种语法。不过它支持流式编程，语法类似下面要讲到的查询扩展方法。

### 查询扩展方法（Query Extension Method）

方法语法使用查询扩展方法。它们是针对IEnumerable\<T>和IQuerayable\<T>接口的一系列扩展方法。它们被定义在System.Linq命名空间下。

大部分扩展方法仍旧返回IEnumerable\<T>和IQuerayable\<T>接口，因此大部分方法支持连缀，是“流式”的。

#### 针对IEnumerable\<T>的查询扩展方法

LINQ的基础类库中实现了针对IEnumerable\<T>的大量扩展方法，以用于查询。我们来看其中一些定义：

```c#
public static IEnumerable<TSource> Where<TSource>(this IEnumerable<TSource> source, Func<TSource, bool> predicate){} //相当于where子句

public static IOrderedEnumerable<TSource> OrderBy<TSource, TKey>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector){}  //相当于 orderby子句+ascending

public static IOrderedEnumerable<TSource> OrderByDescending<TSource, TKey>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector){}  //相当于 oderby子句+descending

public static IEnumerable<TResult> Select<TSource, TResult>(this IEnumerable<TSource> source, Func<TSource, TResult> selector){}  //相当于select子句

public static IEnumerable<IGrouping<TKey, TSource>> GroupBy<TSource, TKey>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector){}  //相当于group子句+by

public static IEnumerable<TResult> Join<TOuter, TInner, TKey, TResult>(this IEnumerable<TOuter> outer, IEnumerable<TInner> inner, Func<TOuter, TKey> outerKeySelector, Func<TInner, TKey> innerKeySelector, Func<TOuter, TInner, TResult> resultSelector){} //相当于join子句+on+equal


public static IEnumerable<int> Range(int start, int count){}  //取范围内元素

public static IEnumerable<TSource> Concat<TSource>(this IEnumerable<TSource> first, IEnumerable<TSource> second){} //拼接两个序列

public static IEnumerable<TSource> Skip<TSource>(this IEnumerable<TSource> source, int count){} //跳过count个元素

public static IEnumerable<TSource> Take<TSource>(this IEnumerable<TSource> source, int count){}  //取最多count个元素

public static TResult Aggregate<TSource, TAccumulate, TResult>(this IEnumerable<TSource> source, TAccumulate seed, Func<TAccumulate, TSource, TAccumulate> func, Func<TAccumulate, TResult> resultSelector){} //累加器

public static TSource FirstOrDefault<TSource>(this IEnumerable<TSource> source){} //取第一个元素，不存在时返回default<TSorce>的值。这将引起立刻执行。

public static TSource Max<TSource>(this IEnumerable<TSource> source){} //取最大值。这将引起立刻执行。

public static int Count<TSource>(this IEnumerable<TSource> source){} //数元素数量。这将引起立刻执行。


public static List<TSource> ToList<TSource>(this IEnumerable<TSource> source){} //将结果转为List\<TSource>。这将引起立刻执行。

public static TSource[] ToArray<TSource>(this IEnumerable<TSource> source){} //将结果转为数组。这将引起立刻执行。

public static Dictionary<TKey, TSource> ToDictionary<TSource, TKey>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector){} //将结果转为字典。这将引起立刻执行。

...
```

还有很多很多。LINQ提供了丰富的扩展方法。它们有如下特点：

- 许多扩展方法返回的仍旧是IEnumerable\<T>因而可以支持**连缀**。

- 大部分方法并不会引起立刻执行，仍然具有延迟执行的特点。上述代码中未在注释中注明会引起立刻执行的方法，均会延迟执行。

- 引起立刻执行的方法，返回的均是具体的类型，不再是IEnumerable\<T>接口。例如对于ToList方法，会引起查询执行，并将查询结果存入List\<T>的对象中，从而使迭代器的结果固化到内存中，而不再需要担心`foreach`该对象会引起迭代器的重复执行。

- 不少扩展方法中使用了委托作为参数：例如Where方法，传递一个参数为元素项，返回为bool类型的委托，来指定筛选的条件。使用它们时，就是Lambda大放异彩的时候。

回顾之前在查询表达式中，我们看到的筛猫例子。用查询扩展方法就可以写成：

```c#
IEnumerable<string> oldCatNames = 
    cats.Where(cat => cat.Age > 10)
        .OrderByDescending(cat => cat.Age)
        .Select(cat => cat.Name); 
```

而使用更多查询表达式不支持的方法，可以实现更多查询功能：

```c#
var names = persons
    .Where(i => i.Name != null && i.Name.StartsWith("李"))
    .OrderBy(i => i.Name)
    .Select(i => i.Name)
    .Skip(2)
    .Take(3)
    .ToList();  //触发立刻执行，并将结果类型转换为List<string>。
```

> Java中与C#的IEnumerable\<T>的LINQ语法类似的是流式（Stream）编程。方法是将任意Collection首先转换为java.util.stream.Stream。然后针对Stream接口执行一系列可连缀的流式处理方法。

> 上例的功能用Stream处理写法如下：
>
> ```java
> //==Java==
> List<String> names = persons.stream()
>     .filter(i->i.getName() != null && i.getName().StartsWith("李"))
>     .sorted(Compartor.comparing(Person::getName))
>     .map(i->i.getName())
>     .skip(2L)
>     .limit(3L)
>     .collect(Collectors.toList());
> ```
>
> 其中：
>
> - 任意Collection调用stream方法，进入Stream Api。
> - Stream Api效仿了LINQ的**延迟执行**，在使用Collector之前，连缀并不会引起遍历的执行。同时，Stream也对连缀的执行顺序进行调配：例如将两个filter合并到一次迭代中。
> - collect方法传递一个Collector接口对象，用于进行数据收集、拼接、转换，并引发实际遍历。
> - Collectors是一个系统预置类，它提供了多种预置Collector。
> - 在collect方法之后，将退出Stream模式，结果退化为普通列表、Map、Set等。
>
> 相较而言：
>
> - 由于Java没有C#意义上的迭代器，因此Stream虽然效仿了延迟执行，但Java的流式编程无法直接针对普通Iterator接口实现，必须通过一套新的Stream接口实现。而C#利用迭代器的延迟执行，直接针对IEnumerable设计，通用性更好。
> - Java的流式编程在collect之后，将退出流式处理——它的返回不再是Stream。因而会导致流式处理中断。如果需要对结果继续处理，则需要再次调用stream方法，转换成新的Stream。而C#即使调用了ToList等方法，仍然可以继续连缀。
> - LINQ的语义更加直观、更好理解。Stream有些操作多少有些拗口，这在进行复杂查询的时候会更为明显。
> - Java没有表达式树，因此Stream也无法支持下一节要讲到的LINQ的更强大的特性：通过转换表达式树实现更多功能。
>
> 事实上，Stream编程在Javaer中间，流行度也不是特别的高。
>
> 关于LINQ和Stream的相似功能的实现对比，可以参考[这篇文章](https://www.zeusro.tech/2018/03/08/linq-vs-stream/)。

因为LINQ实在很有趣，所以这里留给读者一道**思考题**：

我们知道IPv4地址的长度为4个字节，因此IPv4可以使用一个uint存储。uint的比较效率自然高于string。

请读者思考，利用LINQ中的累加器方法（Aggregate），仅用一行代码，实现将一般的`xxx.xxx.xxx.xxx`格式的string类型的ip地址转换成uint值。

#### 针对IQuerayable\<T>的查询扩展方法

针对IQuerayable\<T>的查询扩展方法，几乎与IEnumerable\<T>的一一对应。唯一不同点是，IEnumerable\<T>的扩展方法中传递委托的地方，IQuerayable\<T>传递的是同类型的委托作为泛型参数的表达式树Expression\<TDelegate>。

例如Where扩展方法，定义如下：

```c#
public static IQueryable<TSource> Where<TSource>(this IQueryable<TSource> source, Expression<Func<TSource, bool>> predicate){}  //筛选条件
```

这有什么用呢？

**这用处大了**！

还记得之前我们介绍的Expression\<TDelegate>吗？传递Lambda时，编译器会自动生成该Lambda对应的表达式树。

例如：

```c#
var predict = Persons.Where(person => person.Name == "张三" && person.Age == 18);
```

这里，Where内的Lambda会被转换成等效于下面语句生成的表达式树：

```c#
ParameterExpression personParam = Expression.Parameter(typeof(Person), "person");
Expression<Func<Person, bool>> whereCondition = Expression.Lambda<Func<Person, bool>>(
    Expression.And(
        Expression.Equal(
            Expression.Property(
                personParam,
                "Name"
            ),
            Expression.Constant("张三", typeof(string))
        ),
        Expression.Equal(
            Expression.Property(
                personParam,
                "Age"
            ),
            Expression.Constant(18, typeof(int))
        )
    ),
    personParam
);
```

看起来很复杂，却很好理解。

但是，这又有什么用？

很简单！我可以不按照Lambda的描述来执行，而是按照我们自己的套路修改执行逻辑！

通过遍历表达式树，我们发现`person.Name == "张三"`和`person.Age == 18`是与的关系（&&），这时候我们打算偷天换日，模拟这个执行过程，但是把与换成或（||）。这样，调用我们Where方法的人的代码就被我“篡改”了。我们把这个过程称作**表达式转换**（这个例子中，叫表达式篡改更合理🙂）。

显然，表达式树不会用来干这个，我们不会这么无聊。要举例说明它的实际用处，没有比实体框架更合适的了。

**实体框架**（Entity Framework，简称EF），是一套用于访问数据库的框架，通过LINQ to Entity，可以轻松使用LINQ语句来查询数据库内容。

在LINQ to Entity中，扩展方法Where会将传入的Lambda作为表达式树进行语义分析，根据表达式树将它转换为该语义对应的SQL的where语句。

例如，上述例子中，`person.Name == "张三" && person.Age == 18`这个C#的表达式，会被转换成SQL的语句：`Name = '张三' and Age = 18`。

LINQ to Entity把LINQ的大部分扩展方法重写了一遍，以用于查询数据库。在Where等方法调用时，仅仅是构建数据库查询的语句，当枚举器触发时，才会真的进行查库操作。因而我们可以这样执行数据库的查询：

```c#
var rsl = dbContext.Table1
    .Where(i => i.Flag || i.Parent == null)
    .Where(i => i.Url.StartsWith("http"))
    .Skip(10)
    .Take(10)
    .Select(i => new { i.Name, i.Title })
    .ToList();  //ToList方法将引发查库操作
```

上面的代码会被翻译成下列SQL语句并执行（假设数据库为mysql，且这里仅用作示例，实际上EF生成的语句会更规范一些）

```sql
select `Name`, Title 
from Table1
where (Flag = 1 or Parent is null)
    and `url` like 'http%'
limit 10,10
```

Linq to Entity的能力远远不止如此。它支持外键引用，支持关联查询，支持各种group by、join操作。就实际项目而言，目前还没有发现所需的查询操作用LINQ无法完成书写的。因此，作为CShaper，彻底告别Sql语句也是常有的事。

多说两句，EF除了支持通过LINQ来查询数据，也支持数据的插入和更新。它还支持从代码生成数据库（Code First）和从数据库生成代码（DB First），使得数据库的设计、使用对变得更加容易，从而使开发者可以专注于代码的书写。

现在你应该已经理解了，IQuerayable\<T>的查询扩展方法能做些什么了。是不是很棒？

PS：由于查询语法和方法语法的等效性，LINQ to SQL也同样可以用查询语法。此时，你感觉就像是在代码中写SQL。我并不喜欢这种感觉，好容易通过ORM框架绕开了SQL，又把他写进了代码里。这也是我很少使用查询语法的另一个原因。

> Java由于没有表达式树，因而它的Stream编程也没有类似的表达式转换机制。

---

由于C# 3.0太重要了，我仍然用了较长篇幅去介绍。尤其针对LINQ，我反复强调了它与迭代器的关系，目的是加深大家的理解。事实上，纵观C#的发展历史，如此具有创新性和颠覆性的版本也是绝无仅有的。下一个具有划时代意义的C#版本会是5.0。

接下来，我们将继续C#的旅程，来看看C# 4.0的更新内容。

# C# 4.0 —— 独立发展

虽然没有C# 3.0那么的激动人心，4.0版本有着较为实用的改动。C#已经在自己的道路上独立发展了起来。后续的版本中，大部分语法特点已经无法在Java找到对照物了，因此后面篇幅中的对比部分将会明显减少。

C# 4.0的语法支持：

## 动态类型（Dynamic Type）

动态类型，可以算得上是C#这个强类型语言针对弱类型的优化。之前我们介绍var时说过，var只是自动进行类型推断，本质还是强类型的。而dynamic则真真切切地实现了一把准弱类型。

定义动态类型变量：

```c#
dynamic dyn = 1;
```

使用GetType获取动态类型的类型，将会得到它存储的实际数据的类型：

```c#
//接上例
Console.WriteLine(dyn.GetType().Name);  //输出 Int32
```

dynamic类型可以重新被赋值为其他类型而不会出错。重新赋值后，动态对象的类型也会改成实际的类型。

```c#
//接上例，重新给dyn赋值为string
dyn = "1";
```

dynamic作为一个类型，可以用在任何修饰数据类型的地方：

```c#
public class DynamicSampleClass
{
    static dynamic field;  //静态字段
    public dynamic Prop {get; set;} //属性
    public dynamic ExampleMethod(dynamic param) { ... } //作为方法返回类型、参数类型
}
```

动态类型具有以下特点：

- 动态类型对象可以赋值为任何类型，也可以赋值给任何类型（可能出错）。
- 动态类型被重新赋值时，可以改变类型。
- 动态类型进行运算、获取成员都不会进行编译器检查。但是可能会在运行时抛出异常。
    - 例如：赋值一个动态对象dyn为string类型，写下`dyn*3`这样的表达式编译器不会报错，但在运行时会抛出异常。

这里有必要将一个特殊的类型：**ExpandoObject**

ExpandoObject类的对象支持动态添加成员。因此不必预先定义，便可以使用`.`运算符来赋值、获取其属性。

```c#
dynamic dyn = new ExpandoObject();
dyn.Number = 10;  //动态添加Number属性，并赋值为10
dyn.Increment = (Action)(()=> dyn.Number++; );  //动态添加Increment，作为一个方法（委托）
Console.WriteLine(dyn.Number);  //输出为 10
dyn.Increment();  
Console.WriteLine(dyn.Number);  //输出为 11
Console.WriteLine(dyn.Nothing);  //获取Nothing属性，这里不会抛出异常，而是返回null
```

动态类型可以用于：

- 调用动态语言类型的库，如python编写的库
- 接收可变的数据，如json反序列化的数据
- 不必事先编写类定义，方便自上而下的代码编写，使开发者专注于逻辑。
- 偷懒省事儿

## 命名参数（Named Argument）

我们在进行方法调用时，传递给方法每个参数会按照声明的顺序排列。我们把这种按顺序传递的参数称作**位置参数**。

从C# 4.0开始，支持另一种传递参数的方式：显示的指明要传递的参数名称，而不必再遵守参数的位置顺序。我们把这种传递方式称为**命名参数**。

命名参数的语法为：`参数名:值`

```c#
public class Shop
{
    public void Sell(string userName, string goodsName, int amount) {...} //定义含有三个参数的方法
}

Shop shop = new shop();
shop.Sell("张三", "毛巾", 10);  //常规调用

shop.Sell(userName: "张三", goodsName: "毛巾", amount: 10);  //用命名参数语法调用
shop.Sell(amount: 10, userName: "张三", goodsName: "毛巾");  //调换命名参数的顺序
```

实际上，允许位置参数与命名参数的混用。但是只允许将位置参数放在前面（C#7.2后，这条限制被取消）

```c#
shop.Sell("张三", amount: 10， goodsName: "毛巾");
```

### 可选参数（Optional Argument）

可选参数的语法基于命名参数。它是针对有默认值的参数的。

在调用包含具有默认值参数的方法时，可以使用命名参数的语法指定含默认值参数的值。指定了值的，使用该指定值；未指定值的，使用默认值。

```c#
public class Student
{
    public void Study(string subject, int hours = 2, bool workHard = true) {...} //含有两个有默认值的参数
}

Student student = new Student();
student.Study("语文");  //常规调用，省略所有默认参数
student.Study("语文", 10);  //常规调用，省略最后一个默认参数
student.Study("语文", 2, false);  //常规调用，提供全部参数

student.Study("语文", workHard: false); //采用可选参数语法，并且只提供workHard参数的值，hours参数采用默认值
```

## 协变（Covariant）、逆变（Contravariant）

协变和逆变合称**变种**（Variant）。是指允许数组、泛型委托和泛型接口进行隐式类型转换的机制。

协变是指将元素类型变更为比原类型范围更大的类型（如父类型、接口等）。它用于获取数据，并按照更大范围的类型使用。

逆变是指将元素类型变更为比原类型更精确的类型（如子类型，实现此接口的类型等）。它用于在精确类型中调用作用于更大范围类型的方法。

听不懂？没关系！简答直观说来：

- 协变：子类型 -> 基类型，用于获取
- 逆变：基类型 -> 子类型，用于操作

变种的支持情况：

- 数组的变种（C#2.0）
- 委托的变种（C#4.0）
- 泛型接口的变种（C#4.0）

```c#
//数组的协变
Cat[] cats = { new Cat("阿喵"), new Cat("阿咪") };
Animal [] animals = cats;   //被赋值的数组元素右侧数组元素范围更大的类型（基类）

//接口的协变
IEnumerable<string> strings = new List<string>();   
IEnumerable<object> objects = strings;  //object比string的范围更大

//委托的逆变
Action<object> actObject = someMethod;
Action<string> actString = actObject;  //string比object的范围更小
```

具体分析，很好理解：

- 对于协变：
    - 因为子类型继承了父类型，因此子类型一定具有父类型属性、方法等成员。将数组、接口的子类型视作父类型，并**使用父类型拥有的成员进行操作一定不会出问题**。反之则不然。
    - 如果一个接口的泛型类型支持协变，必然要求在接口的方法内**不可以按照该类型来操作元素**。否则调用了此方法的使用者，传递协变类型给方法，方法中可能会调用不存在于该协变类型的成员，从而引发错误。
- 对于逆变：
    - 同样因为子类型继承了父类型，因此子类型的可操作成员多于父类型。如果一个委托原来是用来操作父类型的，那么**它的所有操作作用于子类型一定不会有问题**。反之则不然。
    - 如果一个接口的泛型类型支持逆变，必然要求在接口的方法中**不能以该类型作为返回**。否则调用了此方法的使用者，以逆变类型拿到返回的对象后，调用者以逆变类型操作对象，可能会调用对象中不存在的成员，从而引发错误。

定义泛型接口的协变类型，关键词为`out`。标记为out的类型仅能用于方法的返回，不可作为方法参数。但可以作为方法的泛型参数的泛型类型参数。

```c#
interface ICovariant<out R>
{
    R GetOne() { ... }  //OK
    void DoSomething(R r) { ... } //Not OK，R类型不能作为参数类型，编译器报错
    void DoSomething(Action<R> callback) { ... }  //OK R作为泛型的类型参数
}
```

定义泛型接口的逆变类型，关键词为`in`。标记为in的类型仅能用作方法的参数（一般参数和泛型类型参数），不可用于方法的返回。

```c#
interface IContravariant<int A>
{
    void SetOne(A a) { ... } //OK
    void DoSomething<T>() where T : A { ... }  //OK， 作为泛型方法的类型参数
    R GetOne() { ... } //Not OK，A类型不能作为方法返回类型，编译器报错
}
```

在同一个接口中，可以同时指定逆变和协变类型：

```c#
interface IVariant<out R, in A>
{
    R GetOne();  //OK
    void DoSomething(A a);  //OK
    R GetSomething(A a);  //OK
}
```

> Java没有与变种的精确对照物。与之有些相似的，是**泛型通配符**。
> Java允许给泛型添加通配符，以便执行编译时检查。
>
> ```java
> //==Java==
> List<?> listUnknown = new ArrayList<A>();  //无边界通配符，表示List元素可以是任意类型
> List<? extends A> listExtendsA = new ArrayList<A>(); //上界通配符，表示List元素类型必须是A或者A的子类
> List<? super A> listSuperA = new ArrayList<A>(); //下界通配符，表示List元素类型必须是A或者A的父类
> ```
>
> 使用泛型通配符也有PECS原则，这与变种有些类似
>
> - 如果要从集合中读取类型，并且不能写入，可以使用上界通配符；即生产者使用`extends`（Producer Extends，即PE）。 
> - 如果要从集合中写入数据，并且不需要读取，可以使用下界通配符；即消费者使用`super`（Consumer Super，即CS）。
> - 如果既要存又要取，那么就不要使用任何通配符

> 泛型通配符虽然与变种有些类似，但是它们是不同的东西：
>
> - 变种针对数组、委托是一律支持的；针对接口是给接口的泛型类型施加的限制条件；泛型通配符是给实例化的对象施加的限制条件。
> - 变种对于声明的接口具有永久约束；泛型通配符仅仅对声明的变量时有效，声明另一个变量可以更换约束。
> - 泛型的变种是由于C#“真”泛型带来的要求，变种过程中运行时类型发生了改变（因为封闭后的泛型类的类型不同）；而泛型通配符更像是语法糖，它仅在编译阶段起作用，在进入运行时后由于类型擦除便不再需要类型转变。
>     - 这么说主要为了便于理解。严格来说泛型通配符也不完全只是语法糖，对于用extends限定上界的通配符，编译器在做类型擦除时会擦除到上界类型，而非到Object。

# C# 5.0 —— 字数越少，事儿就越大

C#5.0的语法更新，只有2个。但这丝毫不影响它是一个跨时代语法创新。如果给C#语法的创新等级排个序的话，C#3.0排第一，C#5.0则排第二。

## 调用者信息（Caller Information）

有时为了调试或者诊断，开发者可能希望知道调用自己编写的类的方法的调用者是谁。调用者信息就能解决这个问题。

调用者信息通过几个预置特性标注方法参数来实现，具体说来：

1. 被调用者方法提供几个参数，用于接收调用者信息。这些参数都必须拥有默认值。
2. 对这几个参数标注预置的特性。
3. 调用者正常调用该方法，并且保持用于接收调用者信息的字段为默认值。
4. 方法在调用时，会自动将调用者的信息填入被特性标注的对应参数内。方法的编写者可以使用这些信息。

可用的调用者信息特性：

- CallerMemberNameAttribute：修饰string类型参数，用于填入调用者的成员名称（方法名、委托名等）。
- CallerFilePathAttribute：修饰string类型参数，用于填入调用者所在的源码文件路径信息。
- CallerLineNumberAttribute：修饰int类型参数，用于填入调用者所在源码中的行号。
- CallerArgumentExpressionAttribute（C#10.0引入）：修饰string类型参数，用于填入指定的方法参数在调用使用的表达式代码文本。（这个很高级，不过这里我们不举例，放到C#10.0再举例）

我们直接看例子：

```c#
public void TracedMethod(int param1, int param2, 
    [CallerMemberName] string methodName = null,
    [CallerFilePath] string sourceFilePath = null,
    [CallerLineNumber] int sourceLineNumber = 0)
{
    Console.WriteLine("该方法被“"+methodName+"”调用。调用位置：文件"+sourceFilePath+"，行号"+sourceLineNumber+"。");    
}

//调用
obj.TracedMethod(1,3);  //调用者信息参数会被自动填充。
```

## 异步编程（Asynchronous Programming）

可以这样说，任何CShaper，都绕不开异步编程。

C#支持的异步模型，有下面几种：

- 异步编程模型(Asynchronous Programming Model，APM)——通过暴露Begin和End方法来启动异步线程。这种模式在\.Net之前就已经存在，C# 1.0便提供了支持。现在不再推荐使用。
- 基于事件的异步模式(Event-based Asynchronous Pattern，EAP)——通过方法启动线程，通过事件注册回调。在方法完成时触发事件，执行回调。这种模式于\.NetFramework2.0引入，在之前的C#中普遍使用，现在不再推荐使用。
- 基于任务的异步模式(Task-based Asynchronous Pattern，TAP)——通过Task启动任务，并等待任务返回。

我们讲C#的异步编程，特指TAP，并且特指结合了async/await的TAP。它是一种全新的异步模型，而且是语法级别的。它的出现可以说是跨时代的。我们这一章只讲它，其他的模式在这里不做介绍。

如果你写过js，且用的ES6以上的语法，一定对async、await关键词和promise模型不陌生。这其实正是由\.NetFramework4.5（对应的正是C# 5.0）首创的。Task便是基于允诺模型的。C# 5.0的语法更新核心更是几乎完全围绕异步编程。异步的思想对之后诸多语言的发展都产生了深远的影响。

### 为什么要用异步

我们来看一个来自官网的例子：

假设有AB两台服务器，都只有5个线程可用，且都在处理请求。此时，这两个服务器都接收到6个并发请求。每个请求执行一个I/O操作。

未运行异步代码的服务器A，5个线程占满之后，会对第6个请求进行排队。因为IO操作在线程内被同步等待，A必须等到5个线程中的一个完成了I/O密集型工作并结束线程，才能继续处理第6个请求。而当这个条件达成时，服务器A实际已经收到了第20个请求，由于队列过长，服务器响应开始变慢。

运行有异步代码的服务器B，5个线程也在占用中，此时也需对第6个请求排队，但由于使用了异步，在I/O密集型工作开始时，正在等待I/O工作完成的线程控制权会得到释放，而无需等到I/O结束。因而，该线程可以转去处理其他请求。在收到第200个请求时，传入请求队列依然很小，服务器不会变慢。

### 如何理解异步和线程的关系

提到异步大家最容易想到的是多线程。但是在理解C#的异步时，不应等同于线程去思考。事实上在默认情况下，任务会在当前线程上执行，且会在适当的时候将工作委托给框架、CLR、操作系统（如int中断）。（参考JS，JS实际上是跑在单线程上的，但是也支持异步）

不过，开发者仍然可以显式的通过一个新的线程来启动一个任务。

异步编程适合下列场景：

- **I/O绑定**：代码会“等待”某些数据。例如：从Web服务下载数据。可用于提高线程利用率，避免线程因等待I/O任务而被空耗和引起排队。一般而言，它的代码形式为等待一个async方法，该方法返回Task或Task\<TResult>。
- **CPU绑定**：代码要执行开销巨大的计算。例如：游戏伤害计算。可用于避免占用大量CPU时间的代码卡死UI。一般而言，它的代码形式为等待一个由Task.Run启动的后台线程。

事实上：IO绑定的异步任务一般跑在当前线程上；CPU绑定的任务一般跑在新的线程上。

### Task、Task\<TResult>和异步方法

在\.NetFramework4.0(C#4.0)时已经引入Task类，但那时它还仅仅是\.Net的类库更新。虽然已经引入了新的TAP模式，但是还不支持async/await关键词。到了C#5.0，引入可等待方法后，异步不在需要回调的嵌套，可以自然的书写异步代码。这时才正式引爆了异步时代。

Task类和Task\<TResult>用来描述一个任务。其中，Task可描述任意返回类型的任务；Task\<TResult>则用于描述任务的执行结果返回TResult类型数据的任务。这两个类可以用于定义可等待方法和异步方法。任务允许被异步的执行，也可以允许在异步方法中被等待。

我们来看两个概念：

- **可等待方法**：是指返回值为Task、Task\<TResult>的方法。若未添加async关键词，该方法不是异步方法。非异步方法的主体不可以使用`await`运算符。但是，该方法在被调用时，依然可以被等待（即作为await运算符的操作数）。

- **异步方法**：是指在定义时添加了`async`关键词，返回值为Task、Task\<TResult>、void（不推荐）之一的方法。异步方法内可以使用`await`运算符，用于等待可等待方法的执行结果。异步方法如果返回不是void，那么它也是可等待方法。

异步方法名称，一般约定以Async结尾。

这里多说几句：在C#7.0以后，可等待方法不一定必须返回Task类，也可以是任何具有GetAwaiter方法的类，这也包括由扩展方法提供的GetAwaiter。

异步方法的工作原理是这样的：

代码执行至await运算符语句时，会将当前语句的执行挂起，把后续要执行代码注册成回调，并创建任务状态机，记录当前同步上下文以便在Resume时能够回到当前同步上下文中继续执行。同时它将控制权交出，还给调用方。等到await所等待的任务结束后，代码会Resume到await语句的位置，将任务的返回结果取出，继续执行剩下的代码。

这里稍微解释下await运算符，它的返回类型是被等待的任务的结果类型，已去除了Task外壳。如：对于Task\<int>类型的任务，await运算符等待该任务，返回的是int类型。

关于**同步上下文**，这里就不作介绍了，它在异步编程之前就已经存在。感兴趣的读者可以自行查阅资料。或者，在下面讲到异步的死锁问题时，会推荐一篇文章。

我们来看一个例子，这个例子依然来自官方文档：

```c#
[1]  public async Task<int> GetUrlContentLengthAsync()
[2]  {
[3]      var client = new HttpClient();
[4]      Task<string> getStringTask = client.GetStringAsync("https://docs.microsoft.com/dotnet");
[5]      DoIndependentWork();
[6]      string contents = await getStringTask;
[7]      return contents.Length;
[8]  }
[9]  void DoIndependentWork()
[10] {
[11]     Console.WriteLine("Working...");
[12] }
```

为了便于描述，我将上面的代码标上了行号。下面我们来看看异步方法的执行过程：

1. 调用者调用GetUrlContentLengthAsync方法，该方法以同步方式执行到\[4]。
2. \[4]的等式右侧为一个可等待的方法，它返回Task\<string>。该句会立刻返回。由于尚未等待该任务的返回，程序可以继续向下执行到\[5]。
3. \[5]处调用的DoIndependentWork为同步的方法，因而会继续同步执行\[9]方法，并打印“Working...”到屏幕。
4. 执行完DoIndependentWork后，继续同步执行到\[6]。此时，getStringTask可能还未返回。程序会挂起当前线程，并将剩下的语句\[6]和\[7]注册为getStringTask任务的回调，并创建任务状态机。然后程序会返回给GetUrlContentLengthAsync的调用者，交出线程控制权。
5. 等到getStringTask任务完成后，会触发回调。程序Resume到\[6]，并取出getStringTask的执行结果作为await表达式的值，继续执行剩下步骤。
6. 程序执行到\[7]，方法结束，返回contents.Length。
7. 调用者拿到GetUrlContentLengthAsync的返回值，并继续执行后续操作。

这里有个细节，所谓交出线程控制权并不是让操作系统将线程释放掉，而是将线程交还给调用者或者线程池，以便调用者可以继续其他工作或者线程池可以对线程进行重新分配。

### 使用新线程启动任务

可以使用`Task.Run`方法显式的使用新线程启动一个任务。

```c#
var task = Task.Run(() => 
{
    DoSomethingInANewThread();
    AndSoOn();
});
await task;
```

Lambda表达式所描述的方法将会在新的线程中执行。这种情况下，await语句会在线程执行结束时Rusume，并继续向下执行。

由于线程池的机制，可能并非所有任务都会立刻启动，有可能会排队。这具体要看线程池的使用情况。

### 等待多个任务

对于多个执行中的任务，如果要同时等待所有任务结束，可以使用`Task.WhenAll`方法。

```c#
var task1 = DoSomethingAsync();
var task2 = Task.Run(()=> Task.Delay(3000));
var task3 = Task.Run(()=> Task.Delay(1000));
await Task.WhenAll(task1, task2, task3); //同时等待所有任务结束
```

对于多个执行中的任务，如果要等待至少一个任务返回，可以使用`Task.WhenAny`方法。

```c#
var task1 = DoSomethingAsync();
var task2 = Task.Run(()=> Task.Delay(3000));
var task3 = Task.Run(()=> Task.Delay(1000));
await Task.WhenAny(task1, task2, task3); //等待至少一个任务返回
```

### 异步的优势

- 它是语言级别的异步编程模型。

    开发者不必费心于异步设计模式，以及类库对设计模式的支持问题。可以使用简洁的语法实现异步。

- 它自带线程池管理和线程复用，却不需要用户过多关心。

    它可以轻松地启动一个线程，也可以将线程从I/O等待中释放。它自带线程池管理，可以高效率的复用线程。

- 获取结果和捕获异常变得十分容易。

    利用await运算符，可以像获取同步方法的返回一样，轻松的获取异步方法的结果。并且，使用了await运算符的任务，会将未捕获的异常抛出至等待任务的方法中，可以像处理同步的异常一样处理它。

- 非常便于书写，避免回调的嵌套，使代码干净整洁。

    开发者可以像书写同步方法一样，按照逻辑顺序书写对异步方法的调用。尤其在一个方法内有多个异步调用的情况下，不用出现一堆回调的嵌套这样难看的代码。

### 异步的死锁（deadlock）问题

尽量不要混用await/async和`Task.Wait`，使用不当可能导致死锁问题。例如：你在某个方法中使用`Task.Wait`等待一个方法，该方法内使用`await`等待一个任务。

这是因为`Task.Wait`会导致在线程中同步等待，原始线程不会得到释放。而被启动的Task在结束后，又需要回到原始的同步上下文所在线程继续执行，也就是原始线程。因为原始线程还在同步阻塞中，所以导致死锁。

不仅`Task.Wait`。使用`task.Result`，`tast.GetAwaiter().GetResult()`也同样存在死锁问题。

推荐采用以下步骤避免死锁问题：

- 在调用第三方返回Task的方法时，如果你不确定对方的实现是否规范，而你又想使用Task.Wait时，请在Task.Wait之前调用`ConfigureAwaiter(false)`。
- 如果你在编写可能被广泛调用的异步方法类库，请在返回任务前、await某个任务时调用`ConfigureAwaiter(false)`。
- 如果你打算用async/await，建议一路async/await到底。

`ConfigureAwaiter(false)`的含义，简单说来就是：告诉Awaiter，在结束后不必回到调用它的原同步上下文所在线程中继续执行，而是可以任意选择一个线程继续执行。

另外，上述死锁问题仅存在于I/O绑定的情况。使用Task.Run启动的任务不会有死锁的问题。

希望深入了解的读者可以参考官方博客，[这篇](https://devblogs.microsoft.com/dotnet/configureawait-faq/)讲的非常清楚。

### 异步的Java对照

> 看到这里，很多熟悉Java的人应该联想起了`Future`接口。诚然，它的表现与async/await有些像，尤其在大名鼎鼎的第三方框架Spring提供了`@Async`注解后，可以很方便的给一个方法标注为异步方法，并返回一个Future。这使得调用异步方法可以同调用同步方法一样书写，也能方便的等待并获取Future的返回值。但是，它们与C#的任务编程模式并不等效：
>
> - 通过`@Async`标注的方法，一定跑在另一个线程上。这与Task默认跑在相同线程上不同。
> - 虽然也能比较方便的使用Future的get方法等待任务的返回结果，但是这将导致当前线程阻塞，直到Future所指示的线程返回后才能继续执行。当前线程并不会在运行到get时得到释放，它将始终被占用着。

> 事实上，Java没有与async/await一致的异步机制。
---

C#的核心大版本到5.0就告一段落了。从6.0开始，C#进入了小步快跑的阶段。更新速度明显加快，更新的点也越来越细致。

# C# 6.0 —— 语法糖机枪

从6.0起，C#跟随\.Net Core一同进入了敏捷开发时代。每个版本的更新点的数量会开始变多，更新内容也变得激进起来。不过大部分更新点也变得比较微小，描述它们的篇幅也将会明显减少。本文也会小步快跑起来。

## 异常筛选器

try-catch块中，可以在catch语句添加`when`条件

```c#
try
{
    doSomething();
}
catch (CustomException e) when (e.Message.Contains("数据库"))
{
    Console.WriteLine("数据库错误");
}
catch (CustomException e) when (e.Message.Contains("网络"))
{
    Console.WriteLine("网络错误");
}
catch (CustomException e)
{
    Console.WriteLine("出现错误");
}
```

## 属性初始化表达式

现在可以直接给属性初始化：

```c#
public string Name { get; set; } = "张三";
```

如果属性只读，现在也可以这样书写，此时属性只有getter，而不必提供setter：

```c#
public string Name { get; } = "张三";
```

## null传播运算符

C# 6.0引入两个用作于引用类型的运算符`?.`和`?[]`。

- `?.`的对应物是成员访问运算符`.`。
- `?[]`的对应物是索引器运算符`[]`。

它们的含义是：

- 如果a的计算结果为null，则`a?.x`或`a?[x]`的结果为null。
- 如果a的计算结果非null，则`a?.x`或`a?[x]`的结果为`a.x`或`a[x]`。

如果一个表达式中有多个连续的`?.`或`?[]`，它们采用最小化求值策略：从左侧开始，运算链中只要一个`?.`或`?[]`运算返回null，则链的其余部分不会执行。因而它们也叫Null传播运算符。

```c#
obj?[0]?.Property?.Method();  //从左到右，第一个遇到的null，会导致后面的运算符都不被计算，表达式直接返回null
```

常见的，我们可以这样调用委托方法

```c#
someDelegate?.Invoke(); //如果委托为null则不执行
```

## 字符串内插（String Interpolation）

`$`开头的字符串，可以实现字符串中插入表达式。方法是在字符串内通过{}包裹表达式。

基础用法示例：

```c#
$"你好，{name}！今天是星期{dayOfWeek}。天气：{weather}";
```

字符串内插还支持添加对齐方式和格式信息描述，语法为

```c#
{<内插表达式>[,<对齐方式>][:<格式字符串>]}
```

其中后面两部分都是可选的。

- 内插表达式就是可以包含`{}`的字符串，`{}`中为表达式，会自动计算ToString。特别的，如果`{}`中的值为null，会被视作string.Empty
- 对齐方式为整数。如果值为正，则为右对齐；如果值为负，则为左对齐。它的数值表示表达式字符串的最小字符数。等同于PadLeft和PadRight方法。
- 格式字符串为string，它用于描述格式。如果提供格式字符串，则表达式结果必须拥有ToString(string format)的方法。譬如DateTime类就有这种方法。表达式会自动调用该方法。

```c#
var date = DateTime.Now;
var dateString = $"今天是{date:yyyy年MM月dd日}";
```

> 字符串内插php、python等语言都支持。Java并不支持。

内插字符串中，如果含有花括号字符，需要使用两个相同花括号进行转义，即`{{`和`}}`

注意，如{}内表达式包含条件表达式`?:`，需要将整个表达式包裹在圆括号内。这是因为:在这里有语义，表示格式字符串的起始。

\$符号和@符号可以组合使用。在C#6中只能先`$`后`@`。而到了C#8，可以任意切换顺序。

```c#
var name = "张三";
var str1 = $@"哈哈哈\哈哈!\\{{{name}}}";  //合法，输出为 哈哈哈\哈哈!\\{张三}
var str2 = @$"哈哈哈\哈哈!\\{{{name}}}";  //在C#6.0中非法，在C#8.0以后合法
```

## nameof运算符

nameof表达式可用于取变量、类型或成员的名称，作为字符串常量。

需要注意：

- 类型下定义的非静态成员，也可以用`nameof(类型.成员)`来取名字。
- nameof针对变量、成员返回的是对象名称，而非类型名称。
- nameof是编译时求值，而非运行时。
- 如之前提到过的，`@`开头的变量，`@`并不是变量名的一部分

```c#
var name1 = nameof(System.DateTime); //值为 DateTime
var name2 = nameof(List<int>);  //类型名，值为 List
var name3 = nameof(List<int>.Count); //取类型的Count属性，Count不是静态的，这里合法，值为 Count
var name4 = nameof(List<int>.Add); //同理，取类型的Add方法，Add也不是静态的，值为 Add

var numbers = new List<int> { 1, 2, 3 };
var name5 = nameof(numbers);  //变量名，值为 numbers
var name6 = nameof(numbers.Count); //属性名，值为 Count

var @new = 5;
var name7 = nameof(@new); //@不是名字的一部分，值为 new
```

## 索引初始化表达式

初始化器得到了增强，可以在初始化器中使用索引。

```c#
var matrix = new Matrix
{
    [0, 0] = 1.0,
    [0, 1] = 0.2,
    [1, 0] = 1.1,
    [1, 1] = 3.3
};
var dict = new Dictionary<string, double>
{
    ["PI"] = 3.14,
    ["PHI"] = 0.618
};
```

甚至，可以跟属性一同初始化：

```c#
var mixed = new Mixed
{
    Title = "混乱",
    HelloWord = "侬好",
    [0] = 1,
    [1] = 1,
    [2] = 2,
    [3] = 3,
    Ok = false,
    ["Top", 1] = 8848
};
```

十分的方便。

## C# 6.0的其他改进

- **静态引用**（Static Using)：已在C# 1.0时介绍过。
- **表达式主体**（Expression-Bodied Member）：6.0支持的比较少，我们等到C# 7.0再一起讲。
- **Catch和Finally块中**，现在**支持使用await**运算符了。

# C# 7.0—— Python是个好东西

## out变量声明

out关键词在调用方法时现在可以同时声明变量。

以前必须这样写：

```c#
//Old写法
int intValue;
var success = int.TryParse("1", out intValue);
```

现在可以合并成：

```c#
var success = int.TryParse("1", out var intValue);
```

## 元组（Tuple Type）

元组是7.0中比较有趣的更新，我们稍微多花点时间讲一讲。

设想两个场景：

- 你发现需要定义一个类或结构，来封装几个变量。这个类的属性会很少，因此你懒得去定义。
- 你要编写一个方法，该方法需要返回不止一个值，你既不想专门定义一个类，又不想使用out关键词（你觉得out不够优美）。

此时，你当然可以考虑匿名类型。不过C# 7.0提供了更好的选择：元组。

元组，这里特指C# 7.0引入的ValueTuple。需要与\.Net Framework 4.0引入的Tuple类做区分。这里明显是借鉴了python中的元组语法。

元组的定义格式为圆括号，中间定义一组数据，用逗号分隔。

```c#
(double, int) tX = (1.0, 2);  //二元元组类型
(double, int, int) tY = (1.0, 2, 77);  //三元元组类型
(double, int, int, string) tZ = (1.0, 2, 77, "你好坏");  //四元元组类型
```

使用元组，可以很方便的将数个变量组合在一起：

```c#
var a = 1;
var b = 2;
var t = (a, b); //生成元组
```

元组可以分为**命名元组**和**未命名元组**

- 命名元组在定义时指定了元组内元素的名称，因而需要通过指定的名称访问元组内元素
- 非命名元组未指定元组内元素的名称，使用默认命名访问元组内元素。默认命名为`Item1`、`Item2`、`Item3`...

```c#
(int, int) t1 = (1, 2);  //未命名元组
var t1A = t1.Item1; 
var t1B = t1.Item2;

(int A, int B) t2 = (1, 2); //命名元组
var t2A = t2.A;
var t2B = t2.B;
```

命名元组还可以直接在赋值时指定名称：

```c#
var t3 = (A: 1, B: 2); //赋值并指定元素名称
```

元组也支持嵌套：

```c#
var t = (1, 2, (3, (4, 5)));
```

比较有趣的一点是，元组跟Tuple类的定义类似，最多只支持到8个泛型参数。为了实现多于8个元素的元组，第8个泛型参数会使用ValueTuple\<T>类型来实现。所以本质上是通过元组的嵌套来实现的。但是，编译器给我们变了个魔术，你可以定义圆括号内有超过8个元素的元组，并且可以直接使用`Item9`、`Item10`等访问它的元素，而不会有问题，编译器自动会把它转成嵌套的ValueTuple。

### 元组的赋值

看下面的例子：

```c#
(int, int) t1 = (1, 2);
(int A, int B) t2 = (3, 4);
t2 = t1;  //合法
(int C, int D) t3;
t3 = t2;  //也合法
```

可见，元组的元素名称并不重要。事实上，元组只有元素类型的顺序才是重要的。

### 元组的解构（Deconstruction）

元组支持解构语法。所谓解构，就是将元组拆成多个变量。

```c#
int left;
int right;
(left, right) = (1, 2); //解构语法，1和2分别赋值给left和right。
```

或者在元组的解构同时声明变量：

```c#
(var left, var right) = (1, 2);
```

还支持使用单独var对所有声明变量进行自动的类型推断：

```c#
var t = ("a", 1);
var (a, b) = t;  //a为string， b为int
```

### 自定义类的解构方法

任何一个类，都可以通过添加Deconstruct方法来解构成元组。

定义Deconstruct需要满足：

- 返回`void`
- 参数全部用`out`修饰
- 需要解构成几元元组，就提供几个参数。参数类型顺序就是元组元素类型的顺序。

```c#
public class Person
{
    //此处省略属性、构造器等

    public void Deconstruct(out string firstName, out string lastName)  //解构成二元元组
    {
        firstName = FirstName;
        lastName = LastName;
    }
    public void Deconstruct(out string firstName, out string lastName, out string province, out string city) //解构成四元元组
    {
        firstName = FirstName;
        lastName = LastName;
        province = Province;
        city = City;
    }
}

var person = new Person("张", "三", "江苏", "南京");
var (firstName, lastName, province, city) = person;  //自动调用类的解构方法
```

特别的，Deconstruct方法可以是扩展方法。

### 何时使用元组

从之前的介绍可见，使用元组十分灵活

- 既可以将多个变量拼装成一个元组
- 也可以通过解构将元组赋值给多个变量
- 还可以通过类的解构变成元组

语法十分灵活。

回顾之前C#的语言语法。现在，用于临时返回一个相对简单的数据结构组合体，我们有以下的方式：

- 使用匿名类型（C# 3.0引入）
- 使用Tuple类 （\.Net Framework 4.0引入）
- 使用ValueTuple结构（C# 7.0引入，也就是我们现在聊的元组）

怎样抉择呢？我们来看下面的表格：

| 类型 | 访问修饰符 | 类型 | 自定义成员名称 | 析构（终结器）支持 | 表达式树支持 |
| --- | --- | --- | --- | --- | --- |
| 匿名类型 | internal | class | ✔️ | ❌ | ✔️ |
| Tuple | public | class | ❌ | ❌ | ✔️ |
| ValueTuple | public | struct | ✔️ | ✔️ | ❌ |

推荐首选元组。如果需要表达式树支持，则改用匿名类型。

但是，如果你的数据需要序列化（如转成json），最好的做法是定义struct或者类，而非使用上述几种类型。

## C# 7.0的模式匹配（Pattern Matching）

模式（Pattern）其实更贴切的翻译应该是“范式”。即编写提供用于检查的范式。

C#的模式匹配在7.0、8.0、9.0中都有更新。7.0虽然已经很好用了，但是不是完全体。

模式匹配可以使用在以下语句中：

- is表达式
- switch语句
- switch表达式（C# 8.0引入）

模式匹配支持的类型：

- **声明模式**（Declaration Pattern）：用于检查表达式的运行时类型，如果匹配成功，则将表达式结果分配给声明的变量。（C# 7.0）
- **类型模式**（Type Pattern）：用于检查表达式的运行时类型。（C# 9.0）
- **常量模式**（Constant Pattern）：用于测试表达式结果是否等于指定常量。（C# 7.0）
- **关系模式**（Relational Pattern）：用于将表达式结果与指定常量进行大小关系的比较。（C# 9.0）
- **逻辑模式**（Logical Pattern）：用于测试表达式在多个关系模式的逻辑组合下是否匹配。（C# 9.0）
- **属性模式**（Property Pattern）：用于测试表达式的属性或字段是否与模式匹配。（C# 8.0）
- **元组模式**（Tuple Pattern）、**位置模式**（Positional Pattern）：用于解构表达式结果，并测试结果值是否与模式匹配。（C# 8.0）
- **var模式**（Var Pattern）：用于匹配任何表达式，并将其结果分配给声明的变量。（C# 7.0）
- **弃元模式**（Discard Pattern）：用于匹配任何表达式，并丢弃结果。（C# 8.0）

### 常量模式

```c#
if (book is null)
{
}

switch (book) //任何类型都可以switch了
{
    case null:
        break;
}
```

### 声明模式

```c#
if (book is ArtBook artBook) //如果匹配成功，则book被赋值给artBook，且artBook为ArtBook类型
{
}
switch (book)
{
    case ArtBook artBook:
        break;
}
```

> Java在14版本时，引入了预览的instanceof表达式模式匹配，并在Java 16变为正式语法。它相当于C#的is表达式模式匹配，并且仅支持声明模式。

> ```java
> //==Java==
> if (obj instanceof Cat cat){
>     System.out.println(cat.getName());
> }
> ```
> Java正式支持的模式匹配也就到这儿了。Java 17引入了switch的模式匹配不过还是预览版。Java支持模式种类太少，不够实用。

### var模式

```c#
if (book is var anyBook) //这将匹配任何情况
{
}
switch (book)
{
    case var anyBook:
        break;
}
```

注意一点：var模式匹配出来的变量，类型跟原始类型相同，而不是object。

### case的when子句

`switch`的`case`，现在支持`when`子句，用于提供附加条件。

```c#
switch (url)
{
    case string str when str.StartsWith("http://"):
        break;
    case string str when str.StartsWith("https://");
        break;
    case null:
        break;
    case var obj:
        break;
    default:   //由于有var模式在，它将匹配任何情况，因此default永远不会被执行。
        break;
}
```

剩下的模式，我们将在[C#8.0](#C#%208.0的模式匹配)和[C#9.0](#C#%209.0的模式匹配)中继续介绍。

## 本地函数（Local Function）

可以在方法体内的任意语句位置定义本地函数

- 本地函数可以使用当前上下文，包括局部变量。
- 本地函数仅在方法体内可见，无法在方法外使用。

```c#
public void Print()
{
    string Title = "这是标题";
    void PrintTitle() //定义本地函数
    {
        Console.WriteLine(Title); //使用方法内的局部变量
    }

    PrintTitle(); //调用本地函数
    Console.WriteLine("这是正文这是正文这是正文这是正文这是正文这是正文");
}
```

## 表达式主体（Expression-Bodied Member）

表达式主体在C# 6.0时候引入，C# 7.0进行了完善。

| 成员 | 开始提供支持的版本 |
| --- | --- |
| 方法 | C# 6.0 |
| 只读属性 | C# 6.0 |
| 属性 | C# 7.0 |
| 构造函数 | C# 7.0 |
| 终结器 | C# 7.0 |
| 索引器 | C# 7.0 |

所谓表达式主体，就是用表达式表述方法的主体。该方法只有表达式所描述的一句话，表达式的值可作为方法的返回值。是为了简化方法的定义。

表达式主体的语法，类似Lambda，也是用`=>`符号。由于主体内容变成了表达式，因而需要在表达式主体结束时添加语句结束符`;`：

```c#
public override string ToString() => $"{Name}是个好人";  //方法表达式主体
public string Name => name;  //只读属性的表达式主体，这个语法比较特殊，它将只具有getter
public string Name { get => name; set => name = value; }  //属性的表达式主体
public Person(string name) => Name = name; //构造器表达式主体
~Person() => Console.WriteLine($"{Name}完蛋了"); //析构方法（终结器）表达式主体
public string this[int i] { get => arr[i]; set => arr[i] = value; }; //索引器表达式主体
```

## ref返回值、ref局部变量

现在支持将值类型的引用，作为方法的返回。语法是加上`ref`关键词。倘若方法返回的是类的成员，则获得该返回的代码有可能直接修改该成员值。

注意：在方法定义返回值上、方法return时、调用方法时、接收方法结果的局部变量上，都需要添加`ref`关键词。倘若方法调用和最终接收的变量未使用`ref`，则获取的不是引用！！

```c#
public class RefSample
{
    int number = 3;
    public ref int GetNumber() => ref number; //返回number的引用
    public override string ToString() => number.ToString();
}

var sample = new RefSample();
ref var num = ref sample.GetNumber(); //获取引用，左右都要加上ref
num *= 2;  //将引起sample对象的number改变
var str = num.ToString();  //结果为 6 
```

## 弃元（Discard）

弃元符号是一个单独的`_`。

它用于丢弃任何计算结果，不受类型限制。使用弃元接收的值会被丢弃，因而无法获取弃元的值。

弃元用于丢弃方法返回：

```c#
_ = int.TryParse("1", out var intValue); //丢弃是否转换成功的结果
```

弃元用于丢弃out参数：

```c#
var success = int.TryParse("1", out _); //丢弃转换后的数值，仅仅测试是否可以转换
```

元组中使用弃元：

```c#
var (_, _, _, name, _, age) = GetPersonInfo("张三");  //这里获取的是六元元组，我们只对其中两个元素感兴趣，其余的使用弃元丢弃
```

需要注意：因为`_`也是合法的变量名。为了向下兼容，`_`仍然可以被定义为变量，并不会报错。但若如此定义，`_`会覆盖弃元定义，退化为普通变量。作为普通变量的`_`，可以正常获取其值，也无法忽略类型，且不可重复定义。

> Java没有弃元。不过这里还是要说两句：Java在9之前单个`_`也可以作为变量名，但是Java 9的语法更新禁止了单个`_`作为变量名。

## throw表达式

throw表达式，又叫引发表达式。是throw语句的表达式版本。因而可以嵌入更多场景中。

嵌入条件运算符`?:`中：

```c#
var arg = args.Length == 0 ? throw new Exception("必须提供参数") : arg[0];
```

嵌入null合并运算符`??`中：

```c#
this.Name = name ?? throw new Exception("名字不可以为null");
```

嵌入表达式主体：

```c#
public void DoSomething() => throw new NotImplementException();
```

## 更多的可等待类型

现在，你不仅可以等待Task和Task\<TResult>。

首先就是引入了新的结构体ValueTask和ValueTask\<TResult>，用于可立刻返回的任务，从而避免使用Task和Task\<TResult>那样会在堆上分配空间，造成性能的浪费。

```c#
//以前返回一个从表达式结果来的Task
public Task<int> GetOneAsync()
{
    return Task.FromResult(1);   //这会导致在堆上分配一个Task对象
}
//现在可以用下面的语句替换：
public ValueTask<int> GetOneAsync()
{
    return new ValueTask<int>(1);
}
```

其次，C# 7.0以后，允许你等待任何类的对象，只需要它实现GetAwaiter方法。

GetAwaiter方法返回一个INotifyCompletion或者ICriticalNotifyCompletion接口的对象，该接口用于实现通知回调。

此时你就成功的定义了一个**自定义可等待类**，该类也是可等待的。返回该类型的方法也是可等待方法，也可以使用async/await关键词升级为异步方法。

### 异步方法构建器

现在，你还可以定义一个类。这个类需要满足具有以下方法：

- 一个`static`的Create方法，返回该类的对象。
- 一个Start方法，传递IAsyncStateMachine接口类型的状态机引用参数。一个SetStateMachine方法用于设置状态机。
- SetException、SetResult方法用于设置异常、写入结果。
- AwaitOnCompleted、AwaitUnsafeOnCompleted方法用于描述执行到await语句之后应该怎么做，并在任务结束时调用Awaiter的对应方法，以及StateMachine的MoveNext方法。

此时，你就成功定义了一个**自定义异步方法构建器**。

你可以给你刚刚自定义的可等待类上添加特性AsyncMethodBuilderAtrribute，并在参数里指定使用`typeof(你定义的异步方法构建器)`。这样返回你定义的可等待类型的异步方法，会使用你定义的构建类替代系统默认的构建类，去完成异步方法的构建。

## C# 7.0的其他改进

- **二进制文本**：现在可以直接定义二进制常量，语法为0bxxxxxx。例如：`0b101011100`
- **数字分隔符**：数字之间可以用`_`分隔。`_`可以有任意多个，可以加在除了第一位、最后一位和小数点前后的任何位置，包括放在`_`旁。例如：`var n = 1_2__3___4____5_____6_______7;`，它等价于`var n = 1234567;`。

> Java引入二进制文本和数字分隔符要早得多，在Java 7便提供了支持。顺便说一句：C#至今还是不支持八进制文本，而Java和C++均支持。可能是八进制实在是用的太少了。

# C# 7.1、7.2、7.3 —— 小碎步

在C# 7.0的基础上，又推出了7.1、7.2、7.3。都不是太大的更新，但是内容不少。

## C# 7.1的改进

C# 7.1的更新如下：

- 异步Main方法：现在允许程序入口点的Main方法是异步的，从而CMD应用也可以async/await到底。
- default文本表达式：default运算符得到了进化，可以自动推断类型

    ```c#
    string def1 = default(string);  //以前的写法。
    string def2 = default;  //新的语法，自动推断类型。
    var def3 = default;  //NOT OK。报错，因为无法自动推断类型。
    ```

- 元组元素名称的自动推断：跟匿名类型一样，现在元组的元素名称也支持自动推断了。

    ```c#
    int n = 100;
    Cat cat new Cat { Name = "喵呜" };
    var tp = (n, cat.Name);   //元组的元素名称分别为 n、Name
    _ = tp.n;
    _ = tp.Name;
    ```

- 泛型参数的模式匹配：7.0的模式匹配不支持泛型参数的模式匹配，7.1支持了。例如，定义泛型方法`DoSomething<T>(IEnumerable<T> serial)`，在代码中可以对`serial`进行模式匹配，例如`if (serial is List<T>)`。

## C# 7.2的改进

C# 7.2我们还是需要展开来讲一讲，它包含一些和切片（Slice）有关的更新（切片显然又是借鉴了python），也为C# 8.0的索引、范围提供了基础。

### in参数、readonly struct、ref struct、ref readonly返回值、ref readonly struct

这一堆组合是不是看着眼花缭乱。事实上它们都是为了下面的Span\<T>做准备的。虽然这些修饰符都可以用于引用类型，但就其功能而言，一般还是被用作**修饰值类型**。我们一个一个说：

**in参数**：现在可以用in修饰方法的参数。表示：

1. 该参数在方法中会被以引用传递（同ref和out）。
2. 方法中不会修改该参数。

```c#
public void SampleMethod(in int number)
{
    number = 7;   //NOT OK， 会导致编译器报错
}
```

与ref和out不同，在调用含in参数的方法时，in关键词可以省略。

```c#
int n = 10;
SampleMethod(n); //OK
SampleMethod(in n);  //也OK
```

**readonly struct**：表明所定义的结构不可变。试图在初始化之后对结构本身和其中的任何字段重新赋值都会导致报错。使用该结构作为方法的参数传递时，推荐方法的参数用in修饰，以提示开发者该结构不可修改。定义在readonly struct中的字段、属性，都必须是readonly的：字段需要添加readonly修饰；属性则只能有getter，不能有setter（在C# 9.0之后，属性可以有init访问器）。

**ref readonly返回值**：用ref readonly来修饰方法的返回，表明方法的返回是该类型的引用，并且不允许被修改。

**ref struct**：是一种新的结构类型。该类型的结构仍**被分配到栈空间上**，却是引用类型的。它主要用来解决struct作为参数传递时会进行数据拷贝的问题，struct过大会导致性能开销。ref struct不允许实现接口。（当然，因为是struct，也不允许继承。）

ref struct有很多**限制**：

- 它不可以被装箱，因而无法赋值给object对象
- 它无法被赋值给接口类型对象，因为它无法实现接口
- 它不可以作为一般类或者结构的成员（但可以作为ref struct的成员）
- 它不可以用于Lambda表达式或者本地函数
- 它不可以用于异步方法

有了上面的一堆，自然就有了**readonly ref struct**，表示这个结构是分配在栈上的、引用类型的、不可修改的。

好了，到这儿为止，Span\<T>的准备工作都做好了。

### Span\<T>、ReadOnlySpan\<T>

Span\<T>、ReadOnlySpan\<T>是新增的只读引用结构（readonly ref struct）。它们是针对任意连续的内存区域的抽象。

它们可以指向各种内存区域：

- 指向托管内存（分配于堆空间）数组的全部或者一部分（切片）
- 指向栈空间的数组（stackalloc分配的数组）
- 指向原生（native）内存区域（如`int*`指针）

设计它们的目的有二：

1. 实现高性能的连续内存操作——它们真的非常的快。
2. 为支持切片（Slice）提供基础。

Span\<T>、ReadOnlySpan\<T>含Enumerator，可以用作`foreach`。它们也支持使用索引器。`foreach`和索引器返回的都是对元素的引用。因而允许使用`ref`变量接收，从而避免复制。

ReadOnlySpan\<T>与Span\<T>的唯一不同是：通过`foreach`或者索引器返回的引用变量，ReadOnlySpan\<T>是只读的，而Span\<T>是允许修改的。（Span\<T>返回的变量用`ref`修饰，而ReadOnlySpan\<T>的用`ref readonly`修饰）

需要注意，如果`foreach`时未使用`ref`变量接收，同样获取的不是引用，无法对它们进行修改。

Span\<T>、ReadOnlySpan\<T>允许直接使用`stackalloc`关键词进行分配，从而使得`stackalloc`关键词现在可以用于非unsafe的上下文中。

```c#
Span<int> span = length <= 1024 ? stackalloc int[length] : new int [length];  //指向栈或者托管堆空间，不必在unsafe上下文中使用stackalloc
```

Span\<T>和ReadOnlySpan\<T>类型支持切片方法：

```c#
Span<int> span2 = span.Slice(1, 3); //获取从序号1开始，长度为3的切片
```

### 新增了几种泛型约束类型

- Enum：用于约束泛型类型必须为枚举
- Delegate：用于约束泛型类型必须为委托
- MulticastDelegate：用于约束泛型类型必须为多播委托

```c#
public class SampleClass1<T> where T : Enum {}
public class SampleClass2<T> where T : Delegate {}
public class SampleClass3<T> where T : MulticastDelegate {}
```

### 命名参数不必跟在尾部

这是命名参数的语法改进，从前的命名参数必须跟随在位置参数的尾部。还是使用之前的例子：

```c#
public class Shop
{
    public void Sell(string userName, string goodsName, int amount) {...}
}

Shop shop = new shop();

shop.Sell("张三", goodsName: "毛巾", amount: 10);  //从前的语法。userName使用位置参数，另外两个参数使用命名参数。命名参数只能是尾部的参数。

shop.Sell(userName: "张三", "毛巾", amount: 10);  //现在可以这样写。支持在任意参数上使用位置参数，或者命名参数。此处goodsName使用位置参数。
shop.Sell(amount: 10, "毛巾", userName: "张三");  //还可以这样用，仍然是goodsName使用位置参数，其余使用命名参数
```

### C# 7.2的其他改进

- **`private protected`访问修饰符**：表示protect and internal，这个已经在C# 1.0的可访问性修饰符中介绍过了。
- **数值文字中的前导下划线**：C#7.0新增的数字下划线，不支持直接紧跟在0x或者0b的后面，例如`0x_8f7d`在之前是非法的，但是现在合法了。
- **条件ref表达式**：ref赋值语句，现在可以支持条件运算符`?:`。例如：`ref var r = ref (arr != null ? ref arr[0] : ref otherArr[0]);`。注意在条件表达式运算结果上还要加`ref`。

## C# 7.3的改进

### 元组的`==`和`!=`支持

元组现在可以直接用`==`和`!=`进行比较了。

对于元组t1和t2：

- `t1==t2`，相当于`t1.Item1 == t2.Item1 && t1.Item2 == t2.Item2 && ...`
- `t1!=t2`，相当于`t1.Item1 != t2.Item1 || t1.Item2 != t2.Item2 || ...`

同`&&`和`||`的特点一样，都是短路方式。上述`==`比较中，从左到右只要有一项不相等表达式就会返回false，从而跳过后面的比较；上述`!=`比较中，只要有一项相等就会返回false，从而跳过后面的比较。

注意，`==`和`!=`比较都不会考虑字段名，仅仅考虑顺序。

### 针对out变量声明的改进

对C#7.0引入的允许在调用含out参数方法时同步声明变量的语法进行了扩充。允许一些之前不允许使用该语法的地方使用该语法：

- 可以用在字段、属性的初始化表达式中使用
- 可以在构造器串联中使用
- 可以在查询子句中使用

举例：

```c#
public class A 
{
    public A(out int a) { a = 1; }
}
public class B : A
{
    public A A { get; set; } = new A(out var a);   //初始化表达式支持out变量声明
    public B()
        :base(out var a)    //构造器串联支持out变量声明
    {
        Console.WriteLine(a);
    }
}
```

当然，这可能没啥用。

### stackalloc初始化器

stackalloc现在支持初始化器（Initializer）语法：

```c#
Span<int> span1 = stackalloc int[4];  //OK
Span<int> span2 = stackalloc int[4] { 1, 2, 3, 4 };  //OK
Span<int> span3 = stackalloc int[] { 1, 2, 3, 4 };  //OK
Span<int> span4 = stackalloc[] { 1, 2, 3, 4 };  //OK，C# 8.0引入
```

### 特性可作用于自动属性的字段

特性现在可以指定作用于用于实现自动属性的支撑字段。方法是在属性前使用特性时，指明作用域为`field`。

```c#
public class Some
{
    [field:NotNull]  //作用于属性背后的字段
    public string Name { get; set; }
}
```

### 含in参数的方法的改进

定义含in和不含in参数的同名方法不会引起二义性了，可以并存。不过这种情况下，调用in方法必须带上`in`关键词。

```c#
//下面两个方法可以并存
public void Some(int x){}
public void Some(in int x){}

int x = 1;
Some(x);  //这将调用第一个方法
Some(in x); //这将调用第二个方法
```

### C# 7.3的其他改进

- **ref局部变量可再分配**：ref的变量之前只能赋值一次，现在可以在赋值后重新被赋值了。
- **泛型约束又新增了一种：`unmanaged`**。约束为非托管类型（值类型，并且如果是struct则每个字段都不能是引用类型，如果有struct嵌套，嵌套的struct也是）。例如：`public void Test<T>(T arg) where T : unmanaged {}`
- **基于模式的fixed语句**：从前的`fixed`只能用来固定数组或者string类型。由于现在新增了Span\<T>等类型，如果还按照之前的来则无法用`fixed`固定。现在，只要你的struct拥有一个方法：`ref [readonly] T GetPinnableReference()`，并且其中`T`是非托管类型的。该引用类型的struct就可以直接使用fixed语句固定。
- **访问fixed数组的索引可以不用fixed**：之前我们说过，unsafe的struct可以声明fixed的数组。现在如果某个指针想要指向该数组的某个元素，可以不用fixed块固定，但仍然需要使用unsafe上下文。例如`unsafe struct S`包含fixed的数组字段`public fixed int FixedField[100];`，则`int* ptr = s.FixedField[5];`语句不必使用fixed块。
- **对方法重载（Overload）的编译器解析改进**：对方法重载在各种情况下编译器如何解析做出了改进。这使得二义性错误变得更少发生。规则比较复杂，这里不多赘述。

# C# 8.0 —— 当语法升级成为日常

C# 8.0支持以下语法：

## readonly成员

针对struct，现在支持给属性、方法返回值添加`readonly`修饰符。表明属性、方法不会修改任何其他属性、字段的值。

```c#
public struct Sample
{
    private string name;
    public readonly string Name  //OK，该属性不会修改任何字段、属性
    {
        get
        {
            return name;
        }
    }

    public readonly void Set()  //NOT OK
    {
        name = "张三";  //编译器报错，readonly方法不允许修改成员
    }
}
```

特别注意：readonly成员只可用于struct，不支持用于class。

## 接口的默认实现

在从前，接口内的方法，不支持添加可访问性修饰符（如`public`，`private`），不支持声明为`static`，也不支持提供默认的实现。

现在这些限制都没有了。接口的方法可以指定修饰符，还可以提供默认实现。

对于实现接口的类，如果接口中有方法的默认实现，该类可以不必再提供此方法的实现，将继承接口的实现。

> 时隔这么久，终于又可以对比了。早在Java 8（2014年）时，为了引入函数式接口，以便支持Stream编程，就已经引入了接口的默认实现。而C#则足足等到C# 8.0（2019年）才引入。这比Java晚了5年。不过Java 8的接口方法不支持private，要到Java 9以后才支持。

## C# 8.0的模式匹配

激动人心的时刻到了。C# 8.0对模式匹配进行了增强，不过它仍然不是完全体。在C# 9.0会再次增强。C# 8.0的模式匹配支持：

### switch表达式

switch表达式可以说是switch语句块的表达式形式。它具有返回值。

switch表达式根据模式匹配的结果，从不同分支路径返回不同内容，每条路径上也都是表达式，且表达式的值都是同一种类型的，也就是整个switch表达式的返回类型。分支的表达式可以返回void，此时整个switch表达式也为void，不能赋值给变量。

switch表达式的语法较switch语句有所调整：将待判断的表达式前置，并且删去原来switch的圆括号。紧随其后的花括号中不再有case语句，取而代之是`模式=>表达式`的形式，并用逗号分隔。

看如下例子：

```c#
Animal animal = new Cat();
var name = animal switch
{
    Cat cat => "猫猫",
    Dog dog => dog.Name,
    var anything => "啥啊", //跟enum、初始化器一样，这里的逗号也是可删可不删
};
```

上例中，使用了之前提到的声明模式、var模式。

switch表达式中使用声明模式、var模式时，可以结合弃元，丢弃该声明：

```c#
var isStr = obj switch
{
    string _ => true,
    var _ => false
};
```

上述例子中，var模式用来接收所有其他情况，保证了表达式覆盖所有可能路径。不过，switch表达式有个有坑的设定：定义表达式时不必覆盖所有分支情况。如果你的分支无法覆盖所有情况，编译器会给出警告，但不会报错。但是这样做是有风险的：swtich表达式的值如果赋值给变量，在运行时如果找不到分支对应，会在抛出`SwitchExpressionException`异常。

```c#
object obj = 1;
var isStr = obj switch //未能覆盖所有情况，编译器给出警告
{
    string _ => true,  
};   //这将导致抛出异常

```

switch表达式也同样支持when子句：

```c#
public bool IsHttp(string url) => url switch    //在此例子中，方法使用了表达式主体，而主体正是swtich表达式
{
    string httpUrl when httpUrl.StartsWith("http://") => false,
    string httpsUrl when httpsUrl.StartsWith("https://") => true,
    var other => throw new Exception("不是HTTP(s)协议的地址") //这里使用了throw表达式
};
```

很显然，因为switch表达式是表达式，而它的分支也是表达式，因而，switch表达式是可以嵌套的：

```c#
var areYouOk = obj1 switch //R U OK? 
{
    string _ => obj2 switch
    { 
        Cat _ => obj3 switch
        {
            var _ => obj4 switch
            {
                var _ => true
            }
        },
    },  
};
//这个该死的表达式会在obj1为string，obj2为Cat的情况下返回true，其他情况下抛出异常。
```

实际项目中建议不要这么干。

> Java在12引入了增强switch的预览版；后在13支持了switch的返回值从而进化为switch表达式，同时支持在语句块内通过`yield`返回分支结果；最终在14放出正式版。但是，此时switch表达式仍不支持模式匹配。

> Java的增强switch/switch表达式可以分为两种：
>
> - 不将switch结果赋值给变量时，它是增强switch。分支内必须是语句。
> - 将switch的结果赋值给变量时，它是switch表达式，分支内必须是表达式，或者使用yield返回值的语句块。

> Java的增强switch/switch表达式语法跟C#的也是有些不同的，它更像原始的switch块：
>
> - 它的语序跟原来switch语句基本一致：`switch`关键词在前，待检测表达式在后，并且用圆括号包裹。分支使用`case`关键词。默认分支使用`default`关键词。
> - 它的分支，使用`->`符号，而不是`=>`。
> - 分支结束时用分号，这意味着分支主体是语句。这也为支持代码块提供了方便。
> - 每个分支是可以支持语句块的，方法是`->`后面使用花括号`{}`，可以在花括号内书写多行语句。作为表达式时，可以在合适的时机使用`yield 值`语句来返回该分支的值。
> - switch作为表达式时，要求必须有`default`分支，否则编译器会报错。这点比C#要严格。

> ```java
> //==Java==
> //作为增强switch
> switch (exp) {
>     case 1 -> System.out.println("命中"); //分支必须是语句
> }  //可以没有default分支
> 
> //作为switch表达式
> boolean rsl = switch (exp) {
>     case 1 -> true;      //分支是表达式，
>     case 2 -> false;     //但是仍然使用分号
>     case 3 -> {         //可以支持语句块
>         if (System.currentTimeMillis() % 2 == 0) {
>             yield true;   //语句块中通过yield返回该分支的值
>         }
>         else {
>             yield false;  //语句块内如果也有分支，所有分支都必须有yield
>         }
>     }
>     default -> false;  //必须有default分支，否则编译器报错
> };
> ```

> 到了Java 17，加入了switch语句和switch表达式的模式匹配预览版，但仍然非正式语法。因而截止至今日，Java仍没有正式支持switch的模式匹配。

### 弃元模式

新增了一种模式，叫弃元模式。对于switch表达式，它匹配任何情况，相当于switch块中的default。

还是之前的例子，可以写成：

```c#
var isHttps = url switch
{
    string httpUrl when httpUrl.StartsWith("http://") => false,
    string httpsUrl when httpsUrl.StartsWith("https://") => true,
    _ => throw new Exception("不是HTTP(s)协议的地址") //这里使用了throw表达式
};
```

var模式和弃元模式都可以匹配任何情况，区别是：弃元模式无法获取匹配值，而var模式可以。

### 属性模式

现在支持对属性的值进行匹配。

```c#
Cat cat = new Cat();
if (cat is { Name: "喵喵", Age: 13, Hobby: "爬高上低" })  //匹配对应的属性值相等
{
}
```

如果有嵌套呢？

```c#
Cat cat = new Cat();
if (cat is { Name: "喵喵", Looks: { Shape: "Fat", Color: Color.White } })  //类的嵌套
{
}
```

### 元组模式

对于元组，也可以使用模式匹配：

```c#
var value = (a, b) switch
{
    ("a1", "b1") => 1,
    ("a2", "b1") => 2,
    ("a1", "b2") => 3,
    ("a2", "b2") => 4,
    (_, "b3") => 5,
    (_, _) => -1
};
```

### 位置模式

位置模式类似于元组模式，对于支持解构的类，可以用类似元组模式的方式进行模式匹配：

```c#
public class Rect
{
    public double LeftTop{ get; set; }
    public double LeftBottom{ get; set; }
    public double RightTop{ get; set; }
    public double RightBottom{ get; set; }

    public void Deconstruct(out double leftTop, out double leftBottom, out double rightTop, out double rightBottom)
    {
        leftTop = LeftTop;
        leftBottom = LeftBottom;
        rightTop = RightBottom;
        rightBottom = RightBottom;
    }
}

var test = rect switch
{
    (1.0, 2.0, 3.0, 4.0) => true,
    (5.0, 6.0, 7.0, 8.0) => false,
    _ => throw new Exception()
};
```

## using声明

使用using进行自动释放的语法，现在多了一种。using可以直接作为一条语句，不用开启一个代码块了。使用using声明时，必须同步声明变量，同时需要去除using后面的圆括号，不再需要花括号，但是需要添加语句结束符号`;`。如果使用using声明，则会在当前语句所在代码块结束时自动释放，声明的变量的有效期也会持续到当前代码块结束。

```c#
public void DoWithUsing()
{
    using var file = File.Open("/root/1.txt", FileMode.Open);  //此处使用using声明，file变量的生存周期为方法体内，且方法结束时会自动释放file。用此语法必须同步声明变量，不能使用已有变量。

    //省略
}
```

由于此语法，现在多重using可以不必出现嵌套了：

```c#
public int Compute()
{
    using var a = new A();
    using var b = new B();
    using var c = new C();
    return a.Number + b.Number + c.Number;  
}  //方法体结束时会自动释放a、b、c
```

using声明可以有效避免多个using语句块的嵌套，使代码更简洁。

## 可null引用类型

这是一个重要的更新。它的出现，是为了彻底解决NullReferenceExcpetion的问题。

现在引用类型也支持在类型名后面加?了。这里需要注意，例如`string?`，是独特的“可null引用类型”语法，它跟值类型的`int?`等同于`Nullable<int>`不同，并不存在`Nullable<string>`这种类型。

启用了可null引用类型的代码被称为处于**可null上下文**（Nullable Context）中。处于可null上下文中时：

- 引用类型`T`的变量必须用非`null`值进行初始化，并且不能赋值为可能为`null`的表达式。否则会产生编译器警告。
- 引用类型`T?`的变量可以用`null`进行初始化，也可以被赋值为可能为`null`的表达式。但在取消引用（Dereference，即将`T?`赋值给`T`）之前，必须进行`null`检查。否则将生成编译器警告。
- 可以使用**null容忍运算符**`!`来阻止编译器生成警告，编译器会认为使用了该运算符的表达式必定不为`null`。

需要注意的是，可null上下文开启的是一系列编译器警告，但是不会引起编译器报错（那样的话多少有点BT了）。

为此，项目还新增了一个设置选项，用于设置可null上下文的感知等级。可用的感知等级有：禁用、启用、警告、注释。

具体区别如下表：

| 可null上下文感知等级 | 取消引用（Dereference）警告 | 赋值警告 | 引用类型 | ?后缀 | !运算符 |
| --- | --- | --- | --- | --- | --- |
| **禁用** | 禁用 | 禁用 | 均可null | 不可用 | 无效果 |
| **启用** | 启用 | 启用 | 不可null，除非使用?后缀 | 声明可null类型 | 当赋值可能为null时阻止警告产生 |
| **警告** | 启用 | 不适用 | 均可null, 但是在方法开始时，类的成员会被视作非null的 | 生成警告 | 当赋值可能为null时阻止警告产生 |
| **注释**（annotations） | 禁用 | 禁用 | 不可null，除非使用?后缀 | 声明可null类型 | 无效果 |

其中，“取消引用警告”是指T?赋值给T时的警告，“赋值警告”是指T赋值为可能为null的表达式时的警告。

```c#
//当开启可null上下文时
string str1 = "abcdefg"; //ok
string? str2 = null; //ok
string str3 = null;  //编译器产生警告
str3 = str2; //编译器产生警告
str3 = str2!; //使用null容忍运算符，编译器不会产生警告
```

除了项目设置之外，还可以通过`#nullable`预处理指令，来开启或者关闭可null上下文。

## 异步迭代器

C# 8.0支持异步的迭代器，可用于异步的流式处理。

定义异步迭代器方法，需要返回`IAsyncEnumerable\<T>`或者`IAsyncEnumerator\<T>`。

然后，你可以放心的给方法加上`async`。因此方法内可以使用`await`。同时方法内正常使用`yield`语句返回迭代值。

使用异步迭代器时，需要用`await foreach`。

```c#
public async IAsyncEnumerable<int> GetAll()   //该方法实现每隔100ms返回一个迭代值
{
    for (int i = 0; i < 100; i++)
    {
        await Task.Delay(100);
        yield return i;
    }
}

await foreach (var i in GetAll())
{
}
```

## 异步可释放

C# 还支持了异步可释放，方法是实现`IAsyncDisposable`接口。

实现此接口的类可以使用`await using`语句进行异步自动释放。

```c#
var asyncDisposableObject = new SomeAsyncDisposableClass();
await using (asyncDisposableObject) //异步自动释放
{
}
```

IAsyncDisposable接口拥有与IDisposable类似的释放模式。也可以通过IDE生成范式代码。

IAsyncDisposable和IDisposable接口可以同时实现，从而可以同时支持`using`和`await using`。这两者不冲突。

## 索引（Index）、范围（Range）

这又是一个值得絮叨一下的更新。

C# 8.0增加了两种新的数据类型，以及对应的新语法。

Index，表示索引。它分为正向索引和反向索引。

- 正向索引，就是直接给索引赋值一个int值，表示从左侧开始往右数的序号，从0开始。
- 反向索引，就是给索引赋值`^`符号+一个int值，表示从右侧开始往左数的序号，从Length开始。

```c#
Index idx1 = 0; //指代序号0
Index idx2 = ^0; //指代序号Length
```

Range，表示范围。它由两个Index组成，分别表示开始和结束的位置。语法是开始和结束的索引之间使用`..`符号连接。

范围中的索引可以省略。省略开始处的索引，表示从第一个开始；省略结束处的索引，表示到最后一个结束。

非常重要：范围是**左闭右开**的，它包含起始Index的位置，**不包含结束Index的位置**。这是为了应对数组、列表中下标从0开始，从而导致的长度会比最后一个元素的下标多1的问题。

```c#
Range rng1 = 1..3;   //1到2         （表示第2个到第3个元素）
Range rng2 = 3..^1;  //3到length-2  （表示第4个到倒数第2个元素）
Range rng3 = ..7;    //0到6         （表示第1个到第7个元素）
Range rng4 = 3..;    //3到length-1  （表示第4个到最后1个元素）
Range rng5 = ..;     //0到length-1  （表示全部元素）
```

好了，准备工作做好了，接下来它们要有点正经用途了：

### 索引定位

可以使用索引访问数组、string、Span\<T>、ReadOnlySpan\<T>的元素，实现索引定位。

```c#
var names = {
    "张三",
    "李四",
    "王五",
    "赵六",
    "宋七",
    "钱八",
};

var qian = names[^1]; //取length-1位置，也就是最后一个元素。注意不要跟范围混了！范围不包含结束位置，所以要取到最后一个元素需要使结束索引为^0；但是索引本身不存在这个问题，此处取最后一个元素还是用^1。
```

注意：使用索引取出来的是单个元素。

### 范围切片

可以使用范围对数组、string、Span\<T>、ReadOnlySpan\<T>进行切片。这就比较实用了。

```c#
var names = {
    "张三",
    "李四",
    "王五",
    "赵六",
    "宋七",
    "钱八",
};

var subNames1 = names[..];   //获取全部列表
var subNames2 = names[..4];  //获取从0号元素到3号元素，也就是“张三”到“赵六”
var subNames3 = names[4..];  //获取从4号元素到最后1个元素，也就是“宋七”到“钱八”
var subNames4 = names[^3..^0]; //获取倒数第3到最后1个元素，也就是“赵六”到“钱八”
```

注意，范围取出来的是切片，跟原来的类型保持一致。也就是仍是数组、string、Span\<T>或者ReadOnlySpan\<T>类型。

### 自定义类型支持索引和范围

除了上述系统预置支持索引和范围的类型外，我们仍可以通过一些手段让自己实现的类型支持索引和范围。

不过要注意：它们的效率要看具体的代码实现。官方支持的索引和范围处理效率是很高的，自己写的类型能否达到高效率就要看开发者的功底了。

#### 显式支持Index和Range

其实，因为你可以定义索引器，因而你完全可以在自己实现的类中定义key为Index和Range的索引器。这称为**显式支持**了索引和范围。

但对于使用者，需要注意：自定义的索引器是可以返回任意类型的。因而：

- 用Index拿到的未必是元素类型
- 用Range拿到的也未必是原序列类型
- 甚至用Index列表，Range返回单个对象也是允许的

使用者需要看清具体定义。

#### 隐式支持Index和Range

先看一个定义：

**可数类型**是指一个类型拥有可访问的、`int`类型的`Length`或者`Count`属性。

可数类型可以实现对Index和Range的隐式支持。

**隐式支持Index**，需要满足以下条件：

- 该类型是可数类型
- 该类型具有Key为`int`的索引器
- 该类型没有Key为单个`Index`的索引器定义（否则就是显式支持了）

这时，编译器会自动提供索引的支持，使用索引将实际调用
Key为int的索引器。

**隐式支持Range**，需要满足以下条件：

- 该类型是可数类型
- 该类型具有两个`int`参数的Slice方法
- 该类型没有Key为单个`Range`的索引器定义（否则就是显式支持了）

这时，编译器会自动提供范围的支持，使用范围将实际调用上述Slice方法。

## null合并赋值运算符

新增了`??=`运算符，用于判断并给可null类型赋值。运算符左侧必须是左值类型，即变量。

- 如果左侧变量值为null，则赋值为右侧值
- 如果则测变量值不为null，则保持左侧值不变

```c#
public void DoSomething(string word)
{
    word ??= "你好";  //如果传入的word为null，则赋值为 你好
}
```

## C# 8.0的其他改进

- **字符串内插增强**：同时存在`$`和`@`时，之前只能`$`在前，现在哪个符号在前都可以。
- **静态本地函数**：本地函数现在可以用`static`修饰。使用`static`修饰的静态函数无法获取当前上下文中的局部变量和当前类内的非静态字段、属性。
- **可释放的`ref struct`**：`ref struct`因为无法实现接口，所以之前无法实现IDisposable。现在，只需要`ref struct`实现Dispose方法，便可以使用using进行自动释放。这对`ref readonly struct`同样适用。
- **折叠的`stackalloc`初始化表达式**：之前已经提过，现在可以直接使用`stackalloc [] { 1, 2 }`的语法来初始化栈上数组。
- **非托管构造类型**：任何非托管类型的数组，现在都可以使用`stackalloc`分配了。

# C# 9.0 —— 新的征程

C# 9.0同\.Net 5一同发布。这是\.Net合并后的第一个版本，因而C#也开启了新的征程。

C# 9.0支持以下语法：

## init访问器

现在，属性除了getter和setter，增加了一种新的访问器。`init`访问器。

```c#
public string Name { get; init; }
```

拥有`init`访问器的属性，只能在初始化表达式或构造方法中赋值。之后，该属性变成只读，在其他位置不可再次赋值。

`init`访问器跟getter、setter一样，可以自动实现，也可以手动实现。

需要注意，`set`访问器和`init`访问器是冲突的，只能提供一个。

定义`init`访问器，是为了引入另一个重要的语法概念：记录。

## 记录（Record）

引入记录，也是在向函数式编程看齐。也是提升与F#的可交互性。

记录是一种新的类型。它是引用类型的。声明关键词为`record`。

记录中的属性默认带有`init`访问器，因而默认是不可更改的。

记录声明时，可以在两个地方定义属性：

- 圆括号：将记录的属性直接放在圆括号内，此时要求new的时候必须提供这些属性值。等同于记录的构造器。
- 花括号：通过花括号展开，在花括号内定义属性。这跟常规的属性定义类似。

如果不需要，圆括号和花括号都可以省略。当省略花括号时，必须在结束时加上`;`。

```c#
public record Person1(string FirstName, string LastName); //只有圆括号的语法，必须加上分号。它包含两个属性，它们默认带有init访问器。new时必须提供这两个值。

public record Person2  //只有花括号的语法，圆括号被省略。此时new便是无参的。它也包含了两个属性
{
    public string FirstName { get; init; }
    public string LastName { get; init; }
}

public record Person3 (string FirstName)   //结合了两种语法，new时必须提供FirstName的值。它也包含了两个属性。
{
    public string LastName { get; init; }
}
```

记录会由编译器自动生成Equals方法，并重载`==`运算符。它的**相等比较效率很高**。

比较有意思的一点是：C#并没有将记录限死为只读。你仍然可以声明记录内的属性具有`set`访问器。但是一般我们不会这么干，这违反了记录设计的本意。

记录跟类和结构一样，可以定义方法，也能实现接口。记录还支持从记录继承。

> Java在14版本引入了记录类型的预览，并在Java 16正式发布。

> Java的记录整体与C#的类似，都是为了给只读数据解构提供便利。Java也针对记录重写了equals方法，以实现更快的比对。Java也可以在记录内定义方法。

> 不过，它们的区别也不小：
>
> - Java的记录，所有字段只能定义在圆括号中，不允许定义在花括号内。C#记录的属性可以放在圆括号内，也可以放在花括号内。
> - Java的记录，会生成全字段的构造器。而C#会根据放在圆括号里的属性，生成只包含指定属性的构造器。
> - Java的记录定义时，花括号不可以省略。而C#在不需要花括号时，可以省略并替换为`;`。
> - Java的记录中的字段，获取不是用get方法，而是用与字段同名的方法。而C#记录的属性则跟普通属性没有任何区别。
> - Java的记录中的字段都是只读的。而C#虽然默认是只读的，但仍可以被声明为可写。
> - Java的记录不能继承类，也不能被继承。C#则可以继承其他记录，也可以被其他记录继承。（不过我觉得不让继承是对的，往下看就明白了。）
>
> 可见，Java也在向函数式编程靠拢。

### 记录的继承

记录支持继承。但是记录的继承有些奇怪。假设记录A继承了记录B，则：

- A的圆括号内的属性个数，不能少于B的圆括号内的属性个数
- A的圆括号内如果有与B内任意位置定义的属性相同名称的属性，则它们的类型也必须相同
- A的圆括号内如果有与B内任意位置定义的属性相同的属性，它会被B的属性覆盖。通过A获取该名称的属性时，实际获取的是B中该名称属性的值
- A的花括号内如果有与B内任意位置定义的属性相同的属性，则会将B的属性隐藏。这与一般的属性隐藏一致。可以考虑添加`new`关键词。
- 在书写A继承B的语法时，如果B有含参的构造器，则需要在B后面书写圆括号，并以A圆括号内的属性填充B的构造器，以表明应该如何初始化B

这段你可能已经看晕了，我来举例说明下，你一定会更晕的：

```c#
public record Person (string FirstName)
{
    public string LastName { get; init; }
}

//Person1用FirstName来初始化Person的FirstName，而LastName的值会被丢弃。
//Person的LastName覆盖了Person1的LastName。
//通过Person1的对像获取FirstName和LastName，实际获取的是Person的FirstName和LastName。其中FirstName未被初始化。
public record Person1(string FirstName, string LastName) : Person(FirstName);  

//这里我举了一个较为奇葩的例子。
//Person2的LastName的值会被用来给Person的FirstName赋值，而Person2提供的FirstName的值会被丢弃。
//通过Person1的对像获取FirstName和LastName，实际获取的是Person的FirstName和LastName。其中LastName未被初始化。
public record Person2(string FirstName, string LastName) : Person(LastName); 

//这个例子更为奇葩。
//使用Person3的LastName初始化Person的FirstName，但是Person的FirstName又被Person3的FirstName隐藏。
//此时，两个FirstName同时存在。
//对于Person3对象而言，FirstName和LastName都未被初始化；而Person的FirstName被成功初始化，然后被隐藏。
public record Person3(string LastName) : Person(LastName) 
{
    public new string FirstName{ get; init; }
}

//这个终于正常一点了
//Person3会使用FirstName初始Person的FirstName，并且自己包含一个新的属性NickName，也得到了初始化。
public record Person4(string FirstName, string NickName) : Person(FirstName);


//上述记录类型初始化结果：
var person = new Person("1");           //FirstName:1，LastName:null
var person1 = new Person1("1", "2");    //FirstName:1，LastName:null，2被丢弃了
var person2 = new Person2("1", "2");    //FirstName:2，LastName:null，1被丢弃了
var person3 = new Person3("2");         //FirstName:null，LastName:null，Person.LastName:2，但Person.LastName被隐藏，需要将类型转换为Person才可读取
var person4 = new Person4("1", "3");    //FirstName:1，LastName:null，NickName:3
```

咋样，是不是更晕了。

不过不用怕！现实开发中你一定不会这么用。如果你继承了一个记录，你会提供一模一样的圆括号属性，并且精确的用这些属性初始化被继承记录里的对应属性。然后再在它的基础上扩展属性。

### 记录与struct比较

记录设计为用于只读数数据结构的存储。这种轻量的数据结构，让我们联想到了struct。比较record和struct，它们有以下不同：

- struct不支持继承（它们是sealed），record支持继承。record只能从record继承，不可以从类继承。反之亦然。
- struct的相等操作效率比较低。它是使用反射，获取对象的所有字段后逐一比较。而record将由编译器自动生成Equals方法，并重载==运算符，比较效率很高。
- struct赋值会导致复制，因为其是值类型。record是引用类型，赋值只是复制引用地址（马上要讲的`with`表达式除外）。

### with表达式

记录支持使用with表达式进行赋值。使用`with`表达式时，将不再是复制对原记录的引用，而是生成一个新的副本。该副本其他属性不发生变化，仅`with`指定的属性发生变化（称之为**非破坏性变化**）。

如下示例：

```c#
Person3 person = new Person3("三") { LastName = "张" };
Person3 person2 = person with { FirstName = "六" };   //生成一个新的副本，且FirstName为 六，LastName为 张。

bool equal = person == person2;  //使用编译器生成Equals方法比较，效率很高
```

## 顶级语句

现在不需要Main方法了。在Program.cs中，你可以直接书写在任何类之外的代码。这被称为顶级语句。

```c#
//Program.cs
using System;
Console.WriteLine("Hello World");
```

需要注意，一旦使用顶级语句，即使再声明Main方法，Main方法也不再会被当做程序入口点，它变成了一个普通的方法。

## C# 9.0的模式匹配

激动人心的时刻又双叒叕到了。C# 9.0新增了几种模式支持，从而达到了完全体：

### 类型模式

在switch表达式中，可以直接使用类型，不必同步声明变量：

```c#
//以前需要这样写：
var isCat1 = animal switch
{
    Cat _ => true,
    _ => false
};

//现在可以这样写：
var isCat2 = animal switch
{
    Cat => true,
    _ => false
};
```

类型模式事实上是补齐了switch表达式相较于switch语句的短板。

### 关系模式

现在对于switch语句和switch表达式，可以使用`<`、`>`、`<=`、`>=`这几种关系模式：

```c#
public string Level(int score) => score switch 
{
    >= 80 => "良好",
    < 60 => "不及格",
    _ => "一般"
};
```

关系模式中，被比较的值只能是编译时常量值。

### 逻辑模式

可以通过`not`、`and`、`or`对关系模式、常量模式进行组合。并且，可以通过`(`和`)`来改变逻辑的优先级顺序。

```c#
if (obj is not null)
{
}

var season = month switch
{
    >= 3 and < 6 => "春",
    >= 6 and < 9 => "夏",
    >= 9 and < 12 => "秋",
    12 or (>= 1 and < 3) => "冬",
    _ => throw new Exception("月份不合法")
};
```

逻辑模式跟when子句的区别：

- 逻辑模式只能使用`<`、`>`、`<=`、`>=`来比较关系，并用`not`、`and`、`or`来组合关系；`when`子句可以使用任意返回`bool`的表达式。
- 逻辑模式只能比较常量值，`when`子句没这个限制。
- 它俩不冲突，逻辑模式中也照样可以用`when`子句。事实上任何模式都可以用`when`子句。

是不是感觉好像也没啥用？但是，它省事儿啊。对于上面的例子，用`when`子句是：

```c#
var season = month switch
{
    int m when m >= 3 && m < 6 => "春",
    int m when m >= 6 && m < 9 => "夏",
    int m when m >= 9 && m < 12 => "秋",
    int m when m == 12 || (m >= 1 && m < 6) => "冬",
    _ => throw new Exception("月份不合法")
};
```

好像用关系模式要短一点对吧。

### 模式匹配的总结

到了这里，C#的模式匹配算是完全体了。我们回顾一下，C#7.0、8.0、9.0，一共有哪些模式来着：

- 声明模式
- 类型模式
- 常量模式
- 关系模式
- 逻辑模式
- 属性模式
- 元组模式
- 位置模式
- var模式
- 弃元模式

这些模式已足够强大。而且很关键的，它们是可以混用的。例如：这些模式可以同时出现在同一个switch表达式里；甚至，这些模式的后面，也都可以带上`when`子句。

最后一个例子：

```c#
var season = month switch
{
    int m when m >= 3 && m < 6 => "春",          //声明模式+when子句
    >= 6 when month < 9 => "夏",                 //关系模式+when子句
    >= 9 and < 12 => "秋",                       //关系模式+逻辑模式
    12 => "冬",                                  //常量模式
    1 or 2 => "冬",                              //常量模式+逻辑模式
    int.MaxValue when 1 == 1 => "未知",          //常量模式+when子句
    var _ => throw new Exception("月份不合法"),  //var模式+弃元
    // _ => thrown new Exception()               //弃元模式，这里因为有var模式了，所以无法达到此分支。此处如果取消注释，编译器会报错。
};
```

上面这个让人看了哪哪都疼的例子，自然不会出现在实际项目中。但用它对模式做个总结还是很贴切的，这里面除了没有属性模式、元组和位置模式之外，其他的都提到了。

## 目标类型new表达式

与var隐式类型用于通过右侧类型推断左侧变量类型相反，目标类型new表达式是通过左侧变量类型推测右侧的`new`表达式类型。

具体说来，就是左侧如果是明确的类型，右侧`new`时可以省略类型。

这对参数传递也有效。

当目标类型new表达式结合初始化器时，圆括号不可以省略（否则就是匿名类型了）。

```c#
Cat cat = new();  //自动推测new的类型

Cat cat2 = new()   //自动推测，并结合初始化器
{
    Name = "喵"
};

person.Buy(new("毛巾"));  //Person类的Buy方法传递一个Goods类型的参数，这里new自动推测类型为Goods

//复杂一点的例子：
Dictionary<string, List<int>> dict = new ()   //自动推测类型为Dictionary<string, List<int>>
{
    { "分类1", new () { 1, 2, 3 } }  //自动推测类型为List<int>
};
```

## 协变返回类型

子类型在重写父类型方法时，现在不要求返回完全精确的相同返回类型。基类的方法返回可以作为协变返回类型，子类重写时只需要返回该返回类型的逆变类型即可。

```c#
public class Animal
{
    public virtual Animal Clone() { ... }
}
public class Cat : Animal
{
    public override Cat Clone() { ... } //OK 返回逆变类型
}
```

> Java早在5时便支持了该语法。

## Lambda的弃元参数

Lambda的参数，现在可以使用弃元，如果你在Lambda中不打算使用这个参数的话。

```c#
(_, _) => true;

(a, _) => 
{

}

delegate(int _, int b) { return 0; } //匿名方法中使用弃元
```

请注意，如果Lambda的参数只有一个，此时使用`_`不会被视作弃元。这是为了向下兼容，因为单独的`_`之前也被视作合法的变量名。单独的`_`作为Lambda参数可以正常获取其值。

```c#
Action<int> action = _ => Console.WriteLine(_);  //此处_会被视作普通变量，因而作为打印参数不会报错。
```

## 模块的初始化方法

现在可以通过ModuleInitializerAttribute特性来标注一个方法，这个方法必须满足：

1. 方法必须是`static`。
2. 方法必须是普通成员，不能是getter，setter，构造器，本地函数。
3. 方法必须无参数，且必须返回`void`。
4. 不能是泛型方法，也不能在泛型类中。
5. 可访问性必须是`public`或者`internal`。

这样修饰的方法，被编译器视作模块（Module）初始化方法。会在模块第一次被加载时自动执行一次。

它有以下特点：

- 它会在模块第一次被使用时调用，例如：访问静态字段，new一个模块内类型的对象。
- 它只会被精确自动调用一次。不过用户仍然可以通过代码调用它。
- 它的执行时机在所有其它方法之前，但它可以调用其他方法。

## 条件表达式的目标类型优化

针对条件表达式`?:`，如果它的2、3操作数没有公共类型、或者它们的公共类型中无法被隐式转换，现在将根据接收它的变量类型，对它进行隐式类型转换。

但这里引入一个新的问题：如果拥有多个同名方法重载，其重载的参数类型均能够由条件表达式进行隐式类型转换。使用条件表达式作为参数调用方法，编译器将如何选择调用哪个方法呢？

先看一个定义：

给定从表达式E转换为类型`T1`的隐式转换`C1`；从表达式E转换为类型`T2`的隐式转换`C2`。如果`E`不能精确匹配`T2`，并且至少满足以下一个条件：

- `E`精确匹配`T1`。
- `C1`不是条件表达式的转换，`C2`是条件表达式的转换。
- `T1`是比`T2`更优的转换目标，并且`C1`和`C2`都是条件表达式的转换，或者都不是条件表达式的转换。

我们称`C1`是比`C2`的**更优转换**。

编译器会采用参数类型为更优转换的类型的重载调用。

举例说明：

```c#
M(b ? 1 : 2);

void M(short);
void M(long);
```

M有两个重载，而条件表达式 `b ? 1 : 2`会根据更优转换的规则，选择调用`void M(long)`，因为`long`是比`short`更优的转换目标。

关于**更优转换目标**，那又是一个很长的规则了。这里不打算列举出来。

如果你实在不想费心记住更优转换目标的长篇规则，只需要简单的在调用方法时对整个条件表达式做一下强制类型转换就好了。省心又省力。

## C# 9.0的其他改进

- **`static`匿名方法**：现在匿名方法、Lambda，也支持设置为静态的了。静态的匿名方法跟静态的本地函数一样，无法访问当前语句所在上下文中的局部变量、类的非静态成员。
- **`foreach`的改进**：一个类的GetEnumerator方法现在即使是扩展方法，该类对象也可以使用`foreach`来遍历了。
- **本地函数的特性**：应用于方法、方法参数或泛型类型参数的特性，现在都可以应用于本地函数。与用在方法上具有相同含义。
- **本机大小的整数**：新增两个关键词`nint`和`nuint`，用于定义本机大小的整数。
- **函数指针**：在unsafe中支持函数指针，以便于更方便的调用C++写的库。方法是使用`delegate* <参数类型1,参数类型2,...,返回类型>`来定义。返回类型可以是void。
- **禁止发出localsinit标记**：C#不允许使用未赋初值的局部变量。初始化局部变量有两种方式：一种是直接赋值；另一种是给含有局部变量的方法发送localsinit标记。发送localsinit可用于初始化分配在栈上的数组，使它们在使用前所有内存元素被全部赋值成0。用过C++的小伙伴应该都知道，没有初始化的内存可能残余之前的数据，或者干脆是内存刚加电时的混乱状态，直接拿来使用是不安全的。所以使用前对内存区域进行初始化本没有毛病。但是，如果数组的大小较大，初始化可能带来额外的性能损失。C#现在提供了跳过初始化的选项，只需要在不希望给局部变量发送localsinit标记的方法上标注`SkipLocalsInitAttribute`特性即可。
- **分部方法的优化**：如之前提到过的，在这个版本中，partial的方法的限制（不能指定修饰符、不能返回`void`、不能带`out`参数）均被取消。但是要求必须提供实现。

# C# 10.0 —— 学无止尽

C# 10.0，在2021年的年末跟随\.Net 6和Visual Studio 2022发布了。它是目前最新的C#语言版本。

它支持以下语法：

## 记录结构（Record Struct）

有趣的很，刚刚提出了record，现在就开始嫌弃它了。原因竟然是：它是引用类型的。

于是，C# 10.0，推出了值类型版本的record。并取名为记录结构。

关键词为`record struct`，或者`readonly record struct`。

于此同时，为了呼应，原来的record类型，现在等同于`record class`。因此，在C# 10.0之后声明引用类型的记录，可以用`record`，也可以用`record class`

这里就不举例了。

## 属性模式的改进

模式匹配中的属性模式，在含有嵌套的时候，之前只能通过`{}`的嵌套实现，现在可以直接使用`.`运算符：

```c#
Cat cat = new Cat();
if (cat is { Name: "喵喵", Looks: { Shape: "Fat", Color: Color.White } })  //从前的嵌套
{
}
if (cat is { Name: "喵喵", Looks.Shape: "Fat", Looks.Color: Color.White })  //现在可以这样
{
}
```

## Lambda表达式的改进

- Lambda表达式从前是不支持声明类型的，现在支持了。这样便可以赋值给`var`定义的委托了。

    ```c#
    var parse = (string s) => int.Parse(s);  //指定参数类型
    var choose = object (bool b) => b ? 1 : "one";  //指明参数类型、返回类型
    ```

- Lambda现在也支持特性了：应用于方法、方法参数或泛型类型参数的特性，现在都可以应用于Lambda。与用在方法上具有相同含义。

    ```c#
    var parse = [SomeMethodAttrubite] ([SomeParamAttribute] string s) => int.Parse(s);  //指定参数类型
    var choose = [SomeMethodAttrubite] [return:SomeReturnAttrubite] object (bool b) => b ? 1 : "one";  //指明参数类型、返回类型
    ```

## const可以使用字符串内插

如果一个`const`字段是string类型，现在给它赋值可以使用字符串内插，条件是组成内插表达式的均是`const`的常量。

```c#
const string zhang = "张三";
const string li = "李四";
const string say = $"我叫{zhang}，不叫{li}"; //合法，因为zhang和li都是常量
```

## 元组解构声明的优化

我们在解构元组的时候，可以同步声明变量。但是之前所有变量必须一同声明。现在支持一部分在解构时声明，一部分则使用之前的变量。

```c#
int x = 0;
(x, int y) = (3, 4);   //合法，此处只在解构同时声明y，x使用之前的变量
```

## 调用者信息改进

调用者信息特性新增了一个成员`CallerArgumentExpressionAttribute`。它用来修饰string类型的有默认值的参数，可获取调用该方法时，某个参数传入的表达式的文本描述。

```c#
public void TracedMethod(int param1, 
    [CallerArgumentExpression("param1")] string argExpression = null)  //指示获取param1参数的表达式
{
    Console.WriteLine($"调用该方法时，传递的param1参数的表达式是{argExpression}");    
}

obj.TracedMethod(1 + 2 + 3);  //此时，方法内的argExpression参数会被填充为  1 + 2 + 3
```

是不是灰常高级？这在用于诊断、记录Log时会很有用。

## C# 10.0的其他改进

- **结构的改进**：
    - 结构现在可以声明无参构造器了
    - 结构现在也可以用with运算符来赋值了，之前只能用在record上
    - 针对匿名类型，现在也可以使用with运算符

- **内插字符串处理程序**：现在你可以不使用系统的内插字符串处理程序，而去自己定义一个内插字符串的处理程序。代码中的内插字符串会转交由你定义的类来处理。  
- **全局引用**：可以使用`global using`语句来引用命名空间。这样做时，当前编译环境下的所有待编译文件，默认都会using该命名空间。
- **文件范围的命名空间声明**：现在`namespace`的声明可以不必使用花括号`{}`将命名空间内的定义包裹起来，而是可以将namespace作为单独的语句声明。这样做时，namespace将会对当前文件生效。这样做可以减少缩进。这跟Java的package很像。例如：`namespace TestApp;`
- **记录类型**，现在可以在重写ToString时，标记为密封（sealed）
- **明确赋值的编译器改进**：在开启可null感知上下文时，编译器对某些场景的null判断做了优化，变得更加智能了。主要是在if判断中，如果if已经可明确推断某变量不为null时，不再会给出可能为null警告。
- **AsyncMethodBuilderAtrribute现在可以被添加到方法上了**，之前只能被添加到类上（C# 7.0，可以查看之前的介绍）。这样做可以单独指定某个方法采用特定的异步方法构建器，而不是所有返回该类型的异步方法都采用此构建器。
- **预处理指令\#line增强**：现在的语法支持`#line (起始行,起始列) - (结束行,结束列) 列偏移量 "文件名"`，不过一般用不上。

---

终于，C#的历程即将进入尾声了。C#和\.Net目前已经有了明确的时间表，未来会按照时间表迭代和推出新的版本。加之开源+MIT的许可协议，相信可以获得更多投资者的关注，也期望更多的优秀开源项目出现，填补生态的短板。

接下来，我们来聊点有意思的话题：

# 相顾回眸

作为CShaper或者Javaer，会发现C#和Java本同源，却走上了不同的发展道路。网上关于Javaer和CShaper的口舌战争实数不少，但是如果两群人可以相互张望一下，又会有什么趣事发生呢？

## 有什么是Java有但是C#没有的

这章是写给CShper的。（此章节中的对比部分，不会采用之前的格式。）

没有接触过Java的CShaper虽然耳闻C#是Java的改良品种，却不知道到底改良了些什么。通过上面的文章和其中的对比，相信已经能有所概念了。但是，Java难道就没有什么特性在C#中找不到对应的吗？

相信CShaper最想了解的就是这个了。

当然有了。其实大多数已经在之前提到过了，在这里再稍稍做个总结：

- 枚举

    Java的枚举本质是类，所以它可以定义多个字段、方法、私有构造器，还可以实现接口。C#如果要实现相同功能，大部分时候需要借助扩展方法。（不过在我所使用的大部分场景中，反而C#的会更好用一些。）

- 匿名内部类

    通过匿名内部类，可以很方便的提供一个接口的临时实现。而在C#中实现接口你不得不定义一个类。（不过C#也可以通过传递委托，而非接口作为参数的方式。大部分情况下也能解决问题。）

- throw声明

    当方法有可能throw出Exception时（未在方法内捕获），Java必须在方法定义上声明可能抛出的异常类型。这样做的好处是可以防止遗漏异常的捕获。C#没有这样的强制要求，你无法知道方法可能抛出什么异常，除非你在说明注释里描述出来。这就纯看类库的编写者了。（这点就是纯纯的不如）

好像，就这么多了……

## C# Style

这章是写给Javaer的。（此章节中的对比部分，不会采用之前的格式。）

我看到过很多第三方组件，因为需要提供各个语言版本的SDK，所以自然少不了有C#版本。可能因为人员有限，无法由原生的CShaper完成编写。这些C#的版本SDK，一眼便能看出是Javaer写出来的。作为CShper使用起来会觉得有些许别扭，因为它们“满满的Java气息，不够C# Style”。之所以有这样的差别，源于Javaer和CShaper的思维习惯不同。我把CShaper具有的思维风格称作C# Style。该风格体现在代码里就是：简约、自然、直观、规范（规范这点与Java是一致的）。

我们从一个例子来看看二者的风格究竟有什么差异。

POI是Apache的一个Java开源项目，它提供对Office文件的读写能力。

我们以Excel为例，看看怎么用它创建一个excel文档：

```java
//==Java==
public class ExcelUtil
{
    /**
    * 将行政区划存入excel格式，并通过byte[]返回
    * @param divisions 区域对象列表
    * @return Excel的字节数组
    * @throws IOException 写入内存异常
    */
    public static byte[] transformToExcel(List<Division> divisions) throws IOException {
        XSSFWorkbook workbook = new XSSFWorkbook();  //创建内存工作簿
        XSSFSheet sheet = workbook.createSheet();  //创建sheet
        //设置表头
        XSSFRow titlerRow = sheet.createRow(0);
        titlerRow.createCell(0).setCellValue("省");
        titlerRow.createCell(1).setCellValue("市");
        titlerRow.createCell(2).setCellValue("区");
        //填充表格
        for (int rowIndex = 1; rowIndex < divisions.size(); rowIndex++) {
            Division division = divisions.get(rowIndex);
            XSSFRow dataRow = sheet.createRow(rowIndex + 1);
            dataRow.createCell(0).setCellValue(division.getProvince());
            dataRow.createCell(1).setCellValue(division.getCity());
            dataRow.createCell(2).setCellValue(division.getDistrict());
        }
        //导出为byte[]
        ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
        workbook.write(outputStream);
        workbook.close();
        return outputStream.toByteArray();
    }
}

//使用
byte[] excelArr = ExcelUtil.transformToExcel(divisions);
```

后来该库被移植到了\.Net上，被命名为NPOI。然而，作为CShaper，其实非常用不惯这个库。为什么呢？我们来对比一下C#的库。

以EPPlus库举例，看看使用这个库，如何创建excel文档：

```c#
public static class ExcelTool
{
    /// <summary>
    /// 将行政区划存入excel格式，并通过byte[]返回
    /// </summary>
    /// <param name="divisions">区域对象列表</param>
    /// <returns>Excel的字节数组</returns>
    public static byte[] ToExcel(this List<Division> divisions)
    {
        using var package = new ExcelPackage();  //创建内存区域的Excel包
        var workbook = package.Workbook;  //获取工作簿
        var sheet = workbook.Worksheets.Add("sheet1"); //创建sheet
        //设置表头
        sheet.Cells[1, 1].Value = "省";
        sheet.Cells[1, 2].Value = "市";
        sheet.Cells[1, 3].Value = "区";
        //填充表格
        for (var rowIndex = 2; rowIndex < divisions.Count; rowIndex++)
        {
            var division = divisions[rowIndex];
            sheet.Cells[rowIndex, 1].Value = division.Province;
            sheet.Cells[rowIndex, 2].Value = division.City;
            sheet.Cells[rowIndex, 3].Value = division.District;
        }
        //导出为byte[]
        return package.GetAsByteArray();
    }
}

//使用
var excelArr = divisions.ToExcel();
```

从这个例子中，大伙儿应该已经感受到了两者风格的差异了。这里列举几点例子中的C#的代码的风格特点：

- 使用了属性，简化get、set书写
- 使用了索引器，简化get、set书写
- 定义了扩展方法，以便于可以使用`divisions.ToExcel()`的方式调用
- 方法名用大写开头、属性名也是大写开头

还没完。我们继续扩展一下，结合LINQ、模式匹配对Excel数据进行查询：

```c#
//查询成绩为中等的学生
var students = sheet.Cells["c1:c100"]
    .Where(c => c.Value is int i and > 60 and < 80)  //模式匹配
    .Select(c => new Student
    {
        Name = c.Offset(0, -1).GetValue<string>(),
        Score = c.GetValue<int>(),
        ScoreLevel = "中等"
    })
    .ToList();  //执行查询
```

这次差异更明显了。事实上，LINQ在数据查询的场景中被大量使用。

屏幕前的读者，如果你是一个Javaer，恰巧又不得不写一些C#版本的SDK封装。以下建议能帮助你写出更C# Style的代码：

### 怎样看起来像一个原生的CShaper

So，how to get一个CShaper的代码Style呢？如果你已经很熟悉Java了，现在因为看了我的文章跃跃欲试想上手写写C#的代码，或者因为生活所迫不得不写点C#的库，那么不妨按照下面的步骤试试，这能快速让你书写的C#代码看起来像原生的CShaper写的。

1. 命名空间的每一段都以大写开头，并且放弃com开头的习惯
2. 接口都加I前缀，接口的实现类去掉Impl后缀
3. 将所有方法名改成大写开头
4. 使用属性和索引器，替代get和set方法，属性也用大写开头
5. 公有的成员命名，无论多长，都是用英文全拼，不做缩写
6. 将所有左花括号另换一行写，而不是在同一行写
7. 占满屏幕的var
8. 使用\==来替代.Equals判断字符串相等。使用<、>等来判断时间先后，+、-来计算时间差。其他有运算符重载的类也一样
9. 使用初始化器来赋值，而不是new完之后挨个set和add
10. 对于null的判断，多用??、?.、?[]、??=运算符
11. 相信我，字符串内插你一定用得上
12. async和await该用就起来，既高大上又能提升性能。不过一旦使用，请一路async/await到底
13. 查询能LINQ则LINQ，能Lambda就Lambda
14. 写点自定义扩展方法，既能简化操作，又能提升可读性。再整整连缀，这就很LINQ Style了

做到这些，你已经八九不离十了。而且，你一旦开始了，我相信你也会逃不过真香定理的。

# 附录

## 参考资料

本文的主线主要是参考官方文档的一篇《C#发展历史》。文中的例子大都是我自己YY出来的，但是基本也都亲自跑过测试，以确保无误。偶尔也会引用下官方文档里的描述和例子，不过鉴于官网中文机翻的可读性几乎等于没有，所以也是参考英文版重新组织过语言的。虽然大部分是凭借既有知识编写，但是为了严谨，在遇到不确定的地方时，仍有查阅一些资料。

主要参考资料：

1. 微软官方文档 <https://docs.microsoft.com/en-us/dotnet/csharp/>，及其中文版本。其中特别参考了：C#的发展 <https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history>。请相信我，中文版本的文档根本看不懂。而且，文章还有错误！
2. 博客园的文章 <https://www.cnblogs.com/>，看到\.Net 6.0刚出没几天，网站版权的栏就变成了“Powered by .NET 6 on Kubernetes”，甚是狂喜。
3. CSDN的文章 <https://blog.csdn.net/>，这也是我开启博客之旅的地方。但是我很懒，几乎不怎么更新。
4. 我自己做的200多页的PPT。

这里再推荐一个有趣的地方：<https://github.com/dotnet/csharplang/discussions>，C#语言讨论区。最早也是在微软自家平台CodePlex上的，现在挪到Github上了。在这里你可以作为普通开发者给C#语言提建议。如果有幸被官方采纳，可能会出现在新的C#版本中。那感觉贼high。

## 作者按

近两年来，我在积极推进我司的微服务化改造。因此，我司的后端技术栈也逐渐差异化、并行了起来。在微服务框架下，差异化不仅是被允许的，而且还是最优的选择。每个语言、框架有它的优势领域和所擅长事务，选用合适工具完成合适任务是明智的原则。但是多技术栈带来的问题也很明显：常用的基础功能、协约类型定义、签名算法实现等诸多在不同服务间通用的组件，因语言不同也要分别实现，难以在多个服务间复用。

在多语种协同工作中，有时还会出现相互不理解的情况。Python玩家可能会不理解Java程序员实现一个简单的功能为什么需要敲这么多行代码；而Java开发者也可能不明白JS语言那变魔术一样花式的对象展开操作。因此，促进不同技术栈间的相互理解就显得尤为重要。所有编程语言都具有一些共性。作为开发者，不应当把自己局限于某个语言的追随者，而应当多学多知，触类旁通，在实际工作中根据场景的最优解选用最合适的语言。此外，对彼此配合的同事所使用的语言有所了解，也能有效得提高沟通顺畅度，提升协作效率。

基于此，近期我在我司内部组织了一波围绕我司主要技术栈Java与C#的语法特点交流会。在我分享的环节中，我以C#发展为主线，阐述了C#的语法特点，以及两种语言的一些差异。分享后，我思考：何不编撰成文。这样既能给我司人员提供随时可查的资料，又可分享给更多朋友。于是，此文应运而生。

本文原本打算命名为《C#和Java的爱恨情仇》，以突出本文包含大量两种语言的对比。但考虑此文仍是一篇以C#的发展为主线的介绍C#的文章，后决定命名为《C#的进化》。

经2月有余的打磨，本文终于完成。部分复杂章节经反复斟酌，修改不下10几稿。然而由于时间仓促，难免仍会有疏漏。对文中错误，欢迎大家留言批评指正。

作者欢迎大家分享本文。但请尊重作者的劳动成果和版权。**如需转载，请在显著位置标明出处。**
