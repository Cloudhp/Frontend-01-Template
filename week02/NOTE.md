# 每周总结可以写在这里

课程笔记

1.编程语言通识与JavaScript语言设计

    语言按语法分类

        非形式语言
            中文，英文
        形式语言（乔姆斯基谱系）
            0型: 无限制文法
                等号左边不止一个 <a><b> ::= "c"
            1型: 上下文相关文法
                "a"<b>"c"::="a""x""c"
            2型: 上下文无关文法
                js, 大部分情况是上下文无关
            3型: 正则文法
                限制表达能力

    产生式(BNF)
    
        随堂练习：编写带括号的四则运算产生式

        <Number>::= "0" | "1" | "2" | ...... | "9"

        <DecimalNumber>::= ("0" | ("1" | "2" | ...... | "9") <Number>+)

        四则运算
        <PrimaryExpression>::= <DecimalNumber> |
            "(" <LogiclaExpression> ")"

        <MultiplicativeExpress>::= <PrimaryExpression> |
            <MultiplicativeExpression> "*" <PrimaryExpression> |
            <MultiplicativeExpression> "/" <PrimaryExpression>

        <AdditiveExpression>::= <MultiplicativeExpress> |
            <AdditiveExpression> "+" <MultiplicativeExpression> |
            <AdditiveExpression> "-" <MultiplictiveExpression>

        <LogicalExpression>::= <AdditiveExpression> |
            <LogicalExpression> "||" <AdditiveExpression> |
            <LogicalExpression> "&&" <AdditiveExpression>

    图灵完备性
        命令式——图灵机
            goto
            if和while
        声明式——lambda
            递归

    类型系统
        动态类型系统与静态类型系统
        强类型与弱类型
            String + Number
            String == Boolean
        复合类型
            结构体
            函数签名
        子类型
            逆变/协变

总结：对产生式BNF理解的不够好，还需多加练习。

2.JavaScript 词法，类型

    Unicode 中文字符
    可用String.fromCharCode(num)  '\'.codePoinAt()进行打印

        JavaScript如何处理emoji字符

        为什么不要用中文做变量名，如何更安全使用中文作为变量名

        "厉".codePointAt(0).toString(16)

        inputElement

            WhiteSpace: \v,\t,nbsp 无分词效果空格(/u00A0),zwnbsp-零宽nbsp

            LineTerminator

            Comment

            Token: 一切有效的东西

                Punctuator:符号，用于构成代码结构

                IdentifierName:标识符

                    变量名:不可与关键字重合，特例:get,undefined全局不可改变变量名

                    属性名:可与关键字重合
                
                Literal:直接量

                    NumericLiteral

                    StringLiteral
                
                Template

        Type

            Number:IEEE 754 Double Float

                浮点数比较: Math.abs(0.1 + 0.2 - 0.3) < Number.EPSION

                97.toString(2)

            String

                USC:U+000 ~ U+FFFF,unicode的BMP范围
                GB:国标
                存储方式:UTF8/UTF16
                    UTF8使用8位存储
                    UTF16使用18位存储

                引号内的特殊字符 \'"bfnrtv
            
            Boolean

            Null

            Undifined

            Symbol
            

总结：正则知识需要加强(https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)