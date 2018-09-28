**文章地址：https://www.douban.com/group/topic/8223222/**

**自学教程：http://www.ccs.neu.edu/home/dorai/t-y-scheme/t-y-scheme.html **　 

　　不得不承认，我感谢Matthias Felleisen把我介绍进入了Scheme和高效编程的世界。感谢Matthia Flatt创造了舒适合用的MzSchema，然我能在这本书中作为示例语言，介绍给读者。 

　　第一章：开始Scheme之旅 

　　作为一个计算机的传统，一般第一条程序都是“Hello World”。那么赶快打开你最喜欢的文本编辑器，创建一个文本文件hello.scm 并且敲入以下内容： 

```
　　The first program 
　　(begin 
　　(display "Hello,World!") 
　　(newline)) 
```

　　第一行是一个注释。当Scheme编译器看到一个分号，就会忽略分号后面所有的内容。 

　　括号括起来的部分我们成为form（译者注：计算机语言的翻译一向都是一个争议的焦点，所以我就不翻译了。），在Scheme里面，通过begin- form开始，里面可以包括一系列的subform。在上述的程序中，有两个subform，第一个调用了display过程来输出它的参数（也就是字符串“Hello World”）到命令行（或者我们成为标准输出），接着调用newline过程，来输出一个换行。 

　　为了运行这段程序，首先需要调用你的Scheme解释器。一般在你的操作系统的命令行里面敲入Scheme的名称就可以了。比如，如果实用MzScheme，你可以在命令行里敲入 

　　mzscheme 

　　这样，就可以调用Scheme的解释器了（译者注：原文是listener，监视器），可以读入你的输入-&gt;执行-&gt;打印执行结果。然后等待更多的用户输入。这个过程就被称之为read-eval-print 循环。注意一点的是，它和你操作系统普通的命令行程序没有什么区别，都是读入命令然后执行最后等待更多的输入。和操作系统一样，Scheme解释器也有自己的输入等待符——一般这是“&gt;”，但是有时候也可能是其他的。

　　要在等待输入符下面装载hello.scm程序，可以通过一条Scheme语句来实现 

　　\(load "hello.scm"\) 

　　Scheme解释器就会执行hello.scm中的内容，输出Hello，World！和一个换行。然后返回到等待输入符，等待你的继续输入。 

　　既然你已经有了如此好用的一个解释器，其实你不用每次都在文本文件里面输入你的程序然后装载执行。更简单的办法是，直接在命令输入符里面输入： 

　　\(begin \(display "Hello,World!"\)\(new line\)\) 

　　接着，就可以看到执行结果 

　　Hello,World! 

　　事实上，更简单的办法，是在命令行下面直接输入“Hello,World!”，你也能马上看到执行结果 

　　 

　　"Hello,World!" 

　　 

　　因为这是解释器的返回值"Hello,World!"。 

　　第二种方式不同之处在于，结果值有一对双引号把结果括起来。最后两个程序的另外一个区别在于，第一个（就是以begin开始的那一个）不执行任何内容 ——Hello,World!不过是通过display调用，输出到标准的输出。第二个程序，form "Hello,World!"需要执行一个结果，这种情况下，返回和form中字符串一样的结果。 

　　 

　　作为一个约定，我们将实用标志=&gt;来表示一个执行结果，比如 

　　 

　　E=&gt;v 

　　 

　　比如： 

　　 

　　\(begin 

　　\(display "Hello,World!"\) 

　　\(newline\) 

　　\) 

　　=&gt; 

　　（比如nothing或者void返回值），虽然它有一个字符串输出 

　　 

　　Hello,World! 

　　 

　　到标准输出。另外一个方面 

　　 

　　"Hello,World!" 

　　=&gt;"Hello,World!" 

　　 

　　在任何情况下，我们可以通过输入 

　　 

　　\(exit\) 

　　 

　　来退出Scheme解释器。 

　　使用命令行解释器的交互环境是一个非常好的验证程序或者程序片段的手段，但是并不是必要的。你也许希望通过一句命令就能够执行你写的scheme程序，而不是是交互环境打交道。在MzScheme中，你可以这样来实现： 

　　 

　　mzscheme -r hello.scm 

　　 

　　这样就可以直接执行Scheme脚本，而不弹出命令行交互环境。就跟你直接输入 

　　 

　　echo Hello,World! 

　　 

　　一样。你甚至可以把hello.scm作为操作系统的命令行程序来执行（通过使用shell脚本或者批处理文件），不过我们到16章才会讨论这个问题。 

　　第二章 数据类型 

　　一个数据类型，是一系列相互关联的值的结合。这些集合本身是不可分的，并且经常被具有一定的结构层次关系。Scheme拥有一些列丰富的数据类型：一些是简单数据类型（不可见的），另外一些通过组合其他的数据类型组成了复杂数据类型。 

　　 

　　2.1 简单数据类型 

　　简单数据类型包括了布尔类型、数字类型、字符类型和符号类型。 

　　 

　　2.1.1布尔类型 

　　 

　　Scheme的布尔类型，通过使用\#t来代表true，\#f来代表false。并且通过内置方法boolean?来判断其后面的参数类型是否是布尔型。 

　　 

　　\(boolean? \#t\) =&gt; \#t 

　　\(boolean? "Hello,World!"\) =&gt; \#f 

　　 

　　过程not 用来对参数值取反。 

　　 

　　\(not \#f\) =&gt;\#t 

　　\(not \#t\) =&gt;\#f 

　　\(not "Hello,World!"\) =&gt;\#f 

　　 

　　关于最后一句Scheme脚本的解释是：在一个需要布尔类型的上下文环境中，Scheme把所有不是\#f的值转化为true。 

　　2.1.2数字类型 

　　Scheme语言中的数字类型可以是整数（比如，42），分数（22/7），实数（3.1416）或者复数（2+3i）。而且整数本身是一个分数，分数是一个实数，实数是一个复数。可以用以下的方法来检测数据类型： 

　　\(number? 42\) =&gt;\#t 

　　\(number? \#t\) =&gt;\#f 

　　\(complex? 2+3i\) =&gt;\#t 

　　\(real? 2+3i\) =&gt;\#f 

　　\(real? 3.1416\) =&gt;\#t 

　　\(real? 22/7\) =&gt;\#t 

　　\(real? 42\) =&gt;\#t 

　　\(rational? 2+3i\) =&gt;\#f 

　　\(rational? 3.1416\) =&gt;\#t 

　　\(rational? 22/7\) =&gt;\#t 

　　\(integer? 22/7\) =&gt;\#f 

　　\(integer? 42\) =&gt;\#t 

　　Scheme的整数不需要特殊指定而使用十进制的格式。当然，你也可以通过在数字前面加上前缀“\#b”来表示你要使用二进制格式。因此，\#b1100就是十进制里面的12。同样的，8进制使用前缀“\#o”，16进制使用\#x或者\#d。 

　　通过使用通用操作符 eqv，可以测试两个数字是否相等。 

　　\(eqv? 42 42\) =&gt;\#t 

　　\(eqv? 42 \#f\) =&gt;\#f 

　　\(eqv? 42 42.0\) =&gt;\#f 

　　更进一步来说，如果你知道相比较的两个参数都是数字类型，那么使用“=”操作符，则更加合适。 

　　\(= 42 42\) =&gt;\#t 

　　\(= 42 \#f\) --&gt;ERROR!!! 

　　\(= 42 42.0\) =&gt;\#t 

　　其他的数据比较操作符包括&lt;、&lt;=、&gt;、&gt;=。 

　　\(&lt; 3 2\) =&gt;\#f 

　　\(&gt;= 4.5 3\) =&gt;\#t 

　　算术过程 +, -, \*, /, 等都有跟我们想象一致的含义： 

　　\(+ 1 2 3\) =&gt;6 

　　\(- 5.3 2\) =&gt;3.3 

　　\(- 5 2 1\) =&gt;2 

　　\(\* 1 2 3\) =&gt;6 

　　\(/ 6 3\) =&gt;2 

　　\(/ 22 7\) =&gt;22/7 

　　\(expt 2 3\) =&gt;8 

　　\(expt 4 1/2\) =&gt;2.0 

　　对于单一参数操作符，“-”和“/” 分别返回负数或者倒数。 

　　\(- 4\) =&gt;-4 

　　\(/ 4\) =&gt;1/4 

　　过程语句“max”和 “min”则返回不定长参数里面最大的和最小的值。 

　　\(max 1 3 4 2 3\) =&gt;4 

　　\(min 1 3 4 2 3\) =&gt;1 

　　过程语句“abs”则返回绝对值。 

　　\(abs 3\) =&gt;3 

　　\(abs -4\) =&gt;4 

　　当然，我这里的介绍只是冰山一角。Scheme提供了一个巨大的而且足够复杂的数学和三角函数库。比如 atan、exp和sqrt分别返回正切、对数以及平方根。如果你想了解更多内容，请参考R5RS \[23\] 

　　2.1.3字符类型 

　　Scheme的字符类型通过使用前缀\#\来定义。因此，\#\c是字符c，另外有一些不能显示的字符需要更多的名字来描述，比如\#\newline,\#\tab，空格则可以用\#\ 来表述或者\#\space来表示。 

　　字符串类型可以通过前缀 char？ 来判断： 

　　\(char? \#\c\) =&gt;\#t 

　　\(char? 1\) =&gt;\#f 

　　\(char? \#\;\) =&gt;\#t 

　　注意，分号字符串在这里就不能标记一个注释了。字符串数据类型通过如下一组操作符来进行比较：char=?,char?,char&gt;=?。 

　　\(char=? \#\a \#\a\) =&gt;\#t 

　　\(char=&gt;\#t 

　　\(char&gt;=? \#\a \#\b\) =&gt;\#f 

　　如果要比较的时候不区分大小写，在比较操作时则使用char-ci而不使用char： 

　　\(char-ci=? \#\a \#\A\) =&gt;\#t 

　　\(char-ci=&gt;\#t 

　　字符大小写转换则使用char-downcase或者char-upcase： 

　　\(char-downcase \#\A\) =&gt;\#\a 

　　\(char-upcase \#\a\) =&gt;\#\A 

　　2.1.4符号 

　　我们前面看到的哪些简单的数据类型被称为“自我求值（self-evaluation）”的数据类型。如果你吧这些数据类型的对象敲到解释器里面，结果值会被解释器立马算出来——当然和你敲进去的值是一样的 

　　\#t =&gt;\#t 

　　42 =&gt;42 

　　\#\c =&gt;\#\c 

　　但是，符号（Symbol）就不一样了。这是因为符号在Scheme编程中被称为变量标识。因此求值结果是变量本身所代表的。不过，符号仍然是一种简单的数据类型，并且符号可以代表Scheme所支持的所有类型，比如字符、数字或者其他类型。 

　　为了区分符号和其他的类型，你应该使用关键quote来表示一个符号。 

　　\(quote xyz\) 

　　=&gt;xyz 

　　这应该是Scheme里面最最正式的用法了，但是另外一种简略的办法似乎使用的人更多 

　　'E 

　　其含义为 

　　\(quote E\) 

　　Scheme符号呗一系列字符串来命名，唯一的限制在于不能够与其他的数据类型混淆，比如字符串类型、布尔类型、数字类型或者混合数据类型。举个例子： 

　　this-is-a-symbol、i18n、&lt;=&gt;甚至$!\#\*都可以作为符号的名字，而16、-i（复数）、\#t、"this-is-a-string"以及\(barf\)则不是。检测的方法是使用关键字 symbol?： 

　　\(symbol? 'xyz\) =&gt;\#t 

　　\(symbol? 42\) =&gt;\#f 

　　Scheme symbols are normally case-insensitive. Thus the 

　　symbols 

　　Calorieand calorieare identical: 

　　Scheme符号一般是大小写不敏感的，也就是说stephen和Stpehen是相同的。 

　　\(eqv? 'Stephen 'stephen\) 

　　=&gt;\#t 

　　通过define关键字，我们可以把一个xyz的符号定义为一个全局变量： 

　　\(define xyz 9） 

　　也就是说把数值9储存到变量xyz中去了，如果你用解释器来查看xyz的值，则会如下显示： 

　　xyz 

　　=&gt;9 

　　要改变变量的值，则必须使用表单关键字 set!： 

　　\(set! xyz \#\c\) 

　　现在 

　　xyz 

　　=&gt;\#\c 

　　2.2 复杂数据类型 

　　所谓复杂的数据类型，就是通过基本类型组合而成。 

　　2.2.1 字符串 

　　字符串就是一系列字符的序列（这里跟符号不一样，符号只是字符序列的组合作为名字来标识）你可以通过双引号来定义个字符串。字符串也是自求值的。 

　　"Hello, World!" 

　　=&gt;"Hello, World! 

　　可以通过 string 过程来把一系列的字符连接 起来组成一个字符串。 

　　\(string \#\h \#\e \#\l \#\l \#\o\) 

　　=&gt;"hello" 

　　让我们定义一个全局的字符串变量： 

　　\(define greeting "Hello; Hello!"\) 

　　注意，在这个里面的分号就不再作为注释的开始了。 

　　另外，对于熟悉命令式编程语言的人来说，把字符串作为一个数组来处理也是一个很有意思的特性。在Scheme里面我们依然可以这么做，需要使用一个叫做string-ref的方法。 

　　\(string-ref greeting 0\) 

　　=&gt;\#\H 

　　通过string-append方法，可以把几个字符串连接在一起。 

　　\(string-append "E " 

　　"Pluribus " 

　　"Unum"\) 

　　=&gt;"E Pluribus Unum 

　　你甚至能够特定长度的字符串，并且在你喜欢的时候填上你所希望的字符。用make-string方法。 

　　\(define a-3-char-long-string \(make-string 3\)\) 

　　The predicate for checking stringness is string?. 

　　和你所预期的一样，检测字符串类型的方法是 string? . 

　　通过string-set! 方法，我们可以改变特定索引下字符串字符的内容。 

　　\(define hello \(string \#\H \#\e \#\l \#\l \#\o\)\) 

　　hello 

　　=&gt;"Hello" 

　　\(string-set! hello 1 \#\a\) 

　　hello 

　　=&gt;"Hallo" 

　　2.2.2 向量 

　　Vectors are sequences like strings, but their elements can 

　　be anything, not just characters. Indeed, the elements can 

　　be vectors themselves, which is a good way to generate 

　　multidimensional vectors. 

　　也许你用过Java来写自己的程序。那么Vector也许你也对其有所了解咯。在Scheme里面，Vector和字符串类似，但是储存的内容就不仅仅是字符了，可以是各种Scheme中的数据类型，包括Vector本身——这样我们就可以很容易的建立起多维度的向量。 

　　下面这个例子我们建立了一个由五个整数组成的向量。 

　　\(vector 0 1 2 3 4\) 

　　=&gt;\#\(0 1 2 3 4\) 

　　Note Scheme's representation of a vector value: a \# 

　　character followed by the vector's contents enclosed in 

　　parentheses. 

　　注意Scheme显示向量的方式，以\#开头，并把向量内容放在一个圆括号里面。 

　　和make-string很类似，通过make-vector可以来生成一个特定长度的向量。 

　　\(define v \(make-vector 5\) 

　　同样道理，通过vector-ref和vector-set!可以访问并修改向量对象中特定的值。通过vector？来检测数据类型。 

　　（译者插话：大家可以试试字符串是不是一个特殊的向量？） 

　　2.2.3 点对（dot pair）和列表 

　　（译者又插话了：其实翻译这篇文档很早就开始了，不过中间间断了很长一段时间，在这段时间内，我囫囵吞枣的看了Haskell,O'Caml还有Python,熟悉这些语言的大虾一定知道点对或者列表在函数式编程概念中所占的重要的地位了） 

　　一个点对是一个复合类型的数据类型。由任意两种数据类型按顺序组成。其实第一个元素我们称为 car （不是汽车哈，呵呵），第二个元素我们称为 cdr。组合这两个元素的操作 为 cons 

　　\(cons 1 \#t\) 

　　=&gt;\(1 . \#t\) 

　　Dotted pairs are not self-evaluating, and so to specify 

　　them directly as data \(ie, without producing them via 

　　a cons-call\), one must explicitly quote them: 

　　点对数据类型不是自求值的数据类型。所以不想使用cons方法来构造一个点对的话，必学用quote方法强制求值。 

　　（ 

　　还记得我们的qutoe方法吗？ 

　　（quote E）或者 ‘E 

　　我也不是太清楚 quote以及symbol的要义，现放在这里，下次再好好想想。 

　　） 

　　'\(1 . \#t\) =&gt;\(1 . \#t\) 

　　\(1 . \#t\) --&gt;ERROR!!! 



　　访问内部元素的方法分别为 car和cdr: 

　　\(define x \(cons 1 \#t\)\) 

　　\(car x\) 

　　=&gt;1 

　　\(cdr x\) 

　　=&gt;\#t 

　　同样的道理，也可以通过set-car!和 set-cdr!来设定每个元素的值： 

　　\(set-car! x 2\) 

　　\(set-cdr! x \#f\) 

　　x 

　　=&gt;\(2 . \#f\) 

　　点对数据类型也可以作为元素被另外的点对数据所包含。 

　　\(define y \(cons \(cons 1 2\) 3\)\) 

　　y 

　　=&gt;\(\(1 . 2\) . 3\) 

　　通过调用car结果的 car方法可以得到第一个元素，通过调用car结果的cdr方法可以得到第二个元素，等等…… 

　　\(car \(car y\)\) 

　　=&gt;1 

　　\(cdr \(car y\)\) 

　　=&gt;2 

　　Scheme支持一种简单的缩写来实现上述功能，比如，通过caar来代替“在car的结果上调用car”,cdar来代替（在car的结果上调用cdr），等等 

　　\(caar y\) 

　　=&gt;1 

　　\(cdar y\) 

　　=&gt;2 

　　这种c...r风格的缩写，最多允许四层套嵌，因此，cadr,cdadr,cdaddr都是可以使用的，而cdadadr则可能无法使用。 

　　如果总是在第二个元素做套嵌的话，Scheme倒是可以使用一点点特殊的方法来标记结果： 

　　\(cons 1 \(cons 2 \(cons 3 \(cons 4 5\)\)\)\) 

　　=&gt;\(1 2 3 4 . 5\) 

　　比如 \(1 2 3 4 . 5\)就是\(1 

　　. \(2 . \(3 . \(4 . 5\)\)\)\)的缩写. 在这个表达式上最后一个元素是5。 

　　更进一步的，Scheme提供了一个更加简单的缩写，如果——如果cdr最后一个元素是一个空的列表（对了，我们这里开始使用一个新的词汇，空列表）——通过\(\)来表示。插一句，和点对一样，列表也不能够自求值。也必学使用quote来强制求值。 

　　'\(\) =&gt;\(\) 

　　让我们回到主题，于是\(1 

　　. \(2 . \(3 . \(4 . \(\)\)\)\)\)就可以缩写成 

　　\(1 2 3 4 

　　这种特殊的点对集合，就是我们常说的列表\(list\)。上述列表有四个元素，可以通过如下的方法来定义： 

　　\(cons 1 \(cons 2 \(cons 3 \(cons 4 '\(\)\)\)\) 

　　但是Scheme同样提供了一个过程，叫做list来更方便的定义列表。如下： 

　　\(list 1 2 3 4\) 

　　=&gt;\(1 2 3 4\) 

　　更进一步的，我们甚至可以用quote方法，来更加简单的定义一个已知元素的list 

　　'\(1 2 3 4\) 

　　=&gt;\(1 2 3 4\) 

　　列表元素可以通过索引来访问 

　　\(define y \(list 1 2 3 4\)\) 

　　\(list-ref y 0\) =&gt;1 

　　\(list-ref y 3\) =&gt;4 

　　\(list-tail y 1\) =&gt;\(2 3 4\) 

　　\(list-tail y 3\) =&gt;\(4\) 

　　list-tailreturns the tailof the list 

　　starting from the given index. 

　　list-tail方法根据索引返回一个列表的尾（tail） 

　　和前面所介绍的一样，通过pair?，list？和null?方法，可以判断相关的数据类型： 

　　\(pair? '\(1 . 2\)\) =&gt;\#t 

　　\(pair? '\(1 2\)\) =&gt;\#t 

　　\(pair? '\(\)\) =&gt;\#f 

　　\(list? '\(\)\) =&gt;\#t 

　　\(null? '\(\)\) =&gt;\#t 

　　\(list? '\(1 2\)\) =&gt;\#t 

　　\(list? '\(1 . 2\)\) =&gt;\#f 

　　\(null? '\(1 2\)\) =&gt;\#f 

　　\(null? '\(1 . 2\)\) =&gt;\#f 

　　2.2.4 数据类型的转化 

　　Scheme offers many procedures for converting among 

　　the data types. We already know how to convert between 

　　the character cases using char-downcaseand 

　　char-upcase. Characters can be converted into 

　　integers using char-&gt;integer, and integers can be 

　　converted into characters using integer-&gt;char. 

　　\(The integer corresponding to a character is usually 

　　its ascii code.\) 

　　Scheme提供了一系列的方法用以处理出具类型之间的转化。我们已经知道怎样通过char-downcase和char-upcase来在字符类型进行转化（译者注：似乎这个例子跟我们的主题并不恰当）。字符类型还可以通过char-&gt;integer方法来转化成整数类型。而且整数类型也可以通过interger-&gt;char来转化成字符类型（整型和字符类型的转化主要是依据ASC码来做的）。 

　　\(char-&gt;integer \#\d\) =&gt;100 

　　\(integer-&gt;char 50\) =&gt;\#\2 

　　字符串类型可以通过以下的方法转化成字符列表。 

　　\(string-&gt;list "hello"\) =&gt;\(\#\h \#\e \#\l \#\l \#\o\) 

　　其他的类型转化方法包括list-&gt;string, vector-&gt;list以及list-&gt;vector。数值能够转化成字符串，比如： 

　　\(number-&gt;string 16\) =&gt;"16" 

　　Strings can be converted to numbers. If the string 

　　corresponds to no number, \#fis returned. 

　　字符串也能够转化成数值类型，如果字符串不是一个合法的数值，则返回一个布尔值\#f。 

　　\(string-&gt;number "16"\) 

　　=&gt;16 

　　\(string-&gt;number "Am I a hot number?"\) 

　　=&gt;\#f 

　　string-&gt;number 还可以使用一个可选参数，即进制根（radix）。 

　　\(string-&gt;number "16" 8\) =&gt;14 

　　因为基于8进制来说16对应的十进制数值是14。 

　　Symbol也能转化成字符串类型。 

　　\(symbol-&gt;string 'symbol\) 

　　=&gt;"symbol" 

　　\(string-&gt;symbol "string"\) 

　　=&gt;string 

　　2.3 其他的数据类型 

　　Scheme contains some other data types. One is the 

　　procedure. We have already seen many procedures, eg, 

　　display, +, cons. In reality, these are 

　　variables holding the procedure values, which are 

　　themselves not visible as are numbers or characters: 

　　Scheme还包括了其他的一些数据类型。其中一个是过程（procedure），或者可以翻译为方法。我们已经见过很多过程了，比如：display，+，cons。事实上，这些都是过程数据类型的变量——与数值或者字符类型是完全不一样的。 

　　cons 

　　=&gt; 

　　我们目前所看到的过程，都被称为原始（primitive）定义的过程，可以看做是全局的。用户也能够自己定义过程变量（一定要记住，过程也是变量的一种）。 

　　另外一个数据类型我们称为端口（port）。一个端口，可以看做是一个数据输入输出的通道。端口一般用在跟文件或者命令行有关的地方。 

　　在我们的“Hello,World”程序中，我们使用了一个过程叫做display来向控制台打印一段字符串。其实display可以使用两个参数，一个是要打印的内容，一个是就是输出端口。 

　　在我们的程度中，display的第二个参数是隐式的，使用默认端口为标准的输出端口。我们可以通过调用过程current-output-port来得到当前标准输出的端口，也就是说我们可以显示的来表达这个含义： 

　　\(display "Hello, World!" \(current-output-port\)\) 

　　2.4 S表达式 

　　以上讨论的所有的数据类型，都可以归类在一起，也就是可以认为是一个完整的Scheme语句（也就是一个完整的括号包围的内容）——我们称为s表达式（s-expression），也就是说 

　　42, \#\c, \(1 . 2\), \#\(a 

　　b c\), "Hello", \(quote xyz\), 

　　\(string-&gt;number "16"\), 和\(begin 

　　\(display "Hello, World!"\) \(newline\)\) 

　　都是S表达式。 

　　



赞

“喜欢”升级啦

觉得内容不错，点个赞吧；

想Mark，收藏到豆列是最好的选择

我知道了

回应 转发 赞 收藏 只看楼主

\[已注销\]

\[已注销\] 2009-10-06 01:23:21

　　Scheme自学教程 2 

　　第三章 代码块（Forms） 

　　读者也许注意到了，在前面那些Scheme的例子中列举了如此多的S表达式，其中隐藏的事实是：程序就是数据。因此，＃\c就是一个程序，或者我们可以称为代码块（Forms）。以后，我们会使用更加正式的词汇form来代替程序片段这个说法。scheme执行form \#\c从而得到一个值\#\c，因为\#\c是可以自我求值的。并不是所有的S表达式都是可以自我求值的，比如说，对于symbol的s表达式 xyz来说，其求值的是xyz本省或代表的变量。而列表s表达式（string-&gt;number "16"）求值结果是数字16。 

　　并不是所有的s表达是都是有效的程序。如果你写如下的代码（1 . 2），则不会通过编译。Scheme运行一个列表样式的form，首先检查第一个元素，或者说检查head，如果head被执行为一个过程（procedure），那么剩下的则被认为是head元素的参数。这个过程就被应用（apply）于这些参数上 

　　如果form的head是一个特殊的form，就会以一种特殊的方式来处理，这样的特殊的form，我们见过的包括begin,define和 set！,begin就意味着它的子form按顺序执行，整个form的返回值就是最后一个子form的返回值，define定义并给一个变量赋值，set!改变变量绑定的值。 

　　译者废话：这段话翻译的真的是很费劲，你看懂了吗？我是大概理解了，如果不理解的话，欢迎与我联系 

　　3.1 过程 

　　We have seen quite a few primitive Scheme procedures, 

　　eg, cons, string-&gt;list, and the like. Users 

　　can create their own procedures using the special form 

　　lambda. For example, the following defines a 

　　procedure that adds 2to its argument: 

　　我们已经看到了好多Scheme内置的过程，包括cons,string-&gt;list等等。其实用户还可以通过著名的标志性的语句lambda自己来定义过程。比如说，下面这个例子就定义了一个自动 加2的过程：

　　\(lambda \(x\) \(+ x 2\)\) 

　　The first subform, \(x\), is the list of parameters. 

　　The remaining subform\(s\) constitute the procedure's 

　　body. This procedure can be called on an argument, 

　　just like a primitive procedure: 

　　第一个子语句 （x），定义了过程的参数。剩下的所有的子语句就是过程体了，定义完毕后，这个过程就可以像内置的过程那样被使用了。 

　　\(\(lambda \(x\) \(+ x 2\)\) 5\) 

　　=&gt;7 

　　当然，当然，如果我们要多次调用这个函数的话，不用这么麻烦的，记住：函数是第一公民，和整数，字符串一样，所以我们可以用一个变量来代表这个函数。 

　　\(define add2 

　　\(lambda \(x\) \(+ x 2\)\)\) 

　　从此以后事情就变得简单了： 

　　\(add2 4\) =&gt;6 

　　\(add2 9\) =&gt;11 

　　3.1.1 过程参数 

　　lambda-过程的参数是在它的第一个子form中被定义的（就是符号lambda之后的第一个form），add2是一个只有一个参数——官方的说法叫做一元参数——的过程。所以他的参数列表是只有一个元素的列表 （x）还记得列表吗？这和我们熟悉的命令式语言基本一样，有一点，所有的变量x都是局部的。 

　　同样我们可以定义两元或者多元参数的过程： 

　　\(define area 

　　\(lambda \(length breadth\) 

　　\(\* length breadth\)\)\) 

　　注意，这里我们其实可以有一个更加投机取巧的办法： 

　　\(define area \*\) 

　　3.1.2 变参 

　　学过JavaScript的，PHP的或者Python的同学一定对可变参数很熟悉了。学过Java或者C\#的同学，我们很同情你们必学写很多重载来模拟这个过程。为了实现这一点。参数列表必学使用一个特殊的符号来标记（又是特殊符号，不过相对很多语言来说，Scheme里面的特殊符号或者所谓的语法糖已经很少了）这个特殊的符号就代表着将要被调用的参数。 

　　一般来说，我们用\(x ...\)来表示变参。一个符号，或者说一个点对类型的form （x ... . z），在点对类型点前面的那部分在过程调用的时候与调用的参数进行匹配。点后面的变量，则把剩下的参数作为一个list存下来 

　　说实话，这段话我也不太理解，主要是没有例子,附上原文，大家参考 

　　In general, the lambdaparameter list can be a list 

　　of the form \(x ...\), a symbol, or a dotted pair of 

　　the form \(x ... . z\). In the dotted-pair case, all 

　　the variables before the dot are bound to the 

　　corresponding arguments in the procedure call, with the 

　　single variable after the dot picking up all the 

　　remaining arguments as one list. 

　　3.2应用\(apply\) 

　　Scheme通过使用过程 apply 来调用一个过程（第一个参数），并把这个过程应用到第二个参数的列表元素上（其实就是把第二个参数列表元素作为第一个参数过程的参数） 

　　\(define x '\(1 2 3\)\) 

　　\(apply + x\) 

　　=&gt;6 

　　一般来说，apply后面跟一个参数作为所要调用的过程，在后面跟着数量不一的所要使用的其他参数。而最后一个必须是一个列表。其构造方法就是先应用过程和最后一个参数，计算出结果，然后结合其他的参数作为这个过程调用的新的参数。 

　　\(apply + 1 2 3 x\) 

　　=&gt;12 

　　我理解其背后的机制应该是： \(+ 1 2 3 \(+ 1 2 3\)\) 

　　3.3 顺序 

　　We used the beginspecial form to bunch together a 

　　group of subforms that need to be evaluated in 

　　sequence. Many Scheme forms have implicit 

　　begins. For example, let's define a 3-argument procedure that 

　　displays its three arguments, with spaces between 

　　them. A possible definition is: 

　　我们可以通过begin这个特殊的form来组织一系列的子form从而让他们可以按照一定的顺序来执行。许多Scheme的form都要求必须以begin来开始，比如如果我们要定义一个过程，按顺序 

　　\(define display3 

　　\(lambda \(arg1 arg2 arg3\) 

　　\(begin 

　　\(display arg1\) 

　　\(display " "\) 

　　\(display arg2\) 

　　\(display " "\) 

　　\(display arg3\) 

　　\(newline\)\)\) 

　　在Scheme中，lambda的函数中默认使用begins，所以在我们下面定义的display3中间并不需要显示的使用begin，当然使用了也没有什么坏处，不用只会让事情更简单。 

　　\(define display3 

　　\(lambda \(arg1 arg2 arg3\) 

　　\(display arg1\) 

　　\(display " "\) 

　　\(display arg2\) 

　　\(display " "\) 

　　\(display arg3\) 

　　\(newline\)\)\) 

　　&gt;&gt; 

　 



回应赞

\[已注销\]

\[已注销\] 2009-10-06 01:25:50

和所有的语言一样，Scheme也支持条件语句，最基本的用法是使用if: 



\(if test-expression 



then-branch 



else-branch\) 



和你所能想象的一样，如果test-expression执行结果是\#t（即任何不是\#f的值），就执行then语句中的分支，否则就执行else分支。当然，else分支是可选的。 



\(define p 80\)\(if \(&gt; p 70\) 



'safe 



'unsafe\) 



=&gt; safe 



\(if \(&lt; p 90\) 



‘low-pressure\) ;no “else” branch 



=&gt; low-pressure 



Scheme也通过我们在第8章将要介绍到的宏来实现了一些更加便利的方法。 



4.1 when和unless 



when和uless就是这样一些便利的宏——当条件判断语句只有一个分支的时候。 



\(when \(&lt; \(pressure tube\) 60\) 



\(open-valve tube\) 



\(attach floor-pump tube\) 



\(depress floor-pump 5\) 



\(detach floor-pump tube\) 



\(close-valve tube\)\) 



这段代码是很好理解的额如果tube的压力低于60了，就会执行后面的5个语句。如果使用if语句则需要如下定义： 



\(if \(&lt; \(pressure tube\) 60\) 



\(begin 



\(open-valve tube\) 



\(attach floor-pump tube\) 



\(depress floor-pump 5\) 



\(detach floor-pump tube\) 



\(close-valve tube\)\)\) 



注意，当使用when的时候，不用输入begin，而使用if的时候，如果分支里面有多条语句的话，就必须使用begin。同样的道理，我们还可以使用unless语句： 



\(unless \(&gt;= \(pressure tube\) 60\) 



\(open-valve tube\) 



\(attach floor-pump tube\) 



\(depress floor-pump 5\) 



\(detach floor-pump tube\) 



\(close-valve tube\) 



并不是所有的Scheme实现都支持when或者unless语句的，不过scheme的魔力也在于此，你可以很容易的通过macro来定义一个。（见第八章） 



4.2 cond 



类似与命令是编程中的case语句，在Scheme中，也提供了cond语句来实现这种用法： 



\(if \(char&lt;? c \#\c\) -1 



\(if \(char=? c \#\c\) 0 



1\)\) 



可以表示为： 



\(cond \(\(char&lt;? c \#\c\) -1\) 



\(\(char=? c \#\c\) 0\) 



\(else 1\)\) 



cond语句被称为多重条件语句，具体的含义我就不多说了。最后跟一个else相当与case语句中的default，另外，不用写begins 



4.3 case 



当然前面的cond语句的判断逻辑必须跟在每一个分支上，然而，Scheme中也提供了正宗的case语句。 



\(case c 



\(\(\#\a\) 1\) 



\(\(\#\b\) 2\) 



\(\(\#\c\) 3\) 



\(else 4\)\) 



=&gt; 3 



分支语句中第一个元素就是C的判断结果。 



4.4 and和or 



Scheme也提供了一系列的特殊子form来进行一些逻辑运算，这里面包括and和or，但是不包括not，not是一个过程名。 



小实验： 



（define myOp and\) 



=&gt; Error 



\(define myOP not\) 



=&gt;\[success\] 



\(and 1 2\) =&gt; 2 



\(and \#f 1\) =&gt; \#f 



and返回第一个为\#f的元素，如果没有就返回最后一个元素（即全为true） 



\(or 1 2\) =&gt; 1 



\(or \#f 1\) =&gt; 1 



or返回第一个为\#t的元素。 



所有的and和or都是从左往右执行，而且一点遇到可以确定的元素，后面的元素都将被忽略，不以计算。 



\(and 1 \#f \(/ 1 0\)\) 



=&gt; \#f 



\(and 1 \(/ 1 0\) \#f \) 



=&gt; \[Error!\]

