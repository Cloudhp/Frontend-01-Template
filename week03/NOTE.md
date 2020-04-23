# 每周总结可以写在这里

## 预习内容：《重学前端》| JavaScript 执行（四）try里面放return，finally还会执行吗？

(```)
  function foo() {
      try {
          return 1;
      }
      finally {
          console.log("Hello");
      }
  }

  console.log(foo());
  // Hello
  // 1
(```)
这里return 1先执行，并将foo()函数的返回值设置为1。然后try执行完毕，接着执行finally。最后foo()函数执行完毕，console.log(...)显示返回值。


finally中的return会覆盖try和catch中return的返回值：
(```)
    function foo() {
        try {
            return 1;
        }
        finally {
            //没有返回语句，没有覆盖
        }
    }

    function bar() {
        try {
            return 1;
        }
        finally {
            // 覆盖前面的 return 1
            return;
        }
    }

    function baz() {
        try {
            return 1;
        }
        finally {
            // 覆盖前面的 return 1
            return "Hello";
        }
    }

    foo();  // 1
    bar();  // undefined
    baz();  // Hello
(```)


在一个函数中执行了两次return,这种怪异行为产生的原因是什么呢？
这一机制的基础正是JavaScript语句执行的完成状态，用一个标准类型表示：Completion Record (用于描述异常、跳出等语句执行过程)。

Completion Record表示一个语句执行完之后的结果，它有三个字段

    - [[type]] 表示完成的类型，有break continue return throw 和 normal几种类型；
    - [[value]] 表示语句的返回值，如果语句没有，则是 empty；
    - [[target]] 表示语句的目标，通常是一个 JavaScript 标签。