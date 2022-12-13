# log

## log分类

1、Log.v 的调试颜色为**黑色**的，任何消息都会输出，这里的v代表verbose啰嗦的意思，平时使用就是Log.v("","");

2、Log.d的输出颜色是**蓝色**的，仅输出debug调试的意思，但他会输出上层的信息，过滤起来可以通过DDMS的Logcat标签来选择.

3、Log.i的输出为**绿色**，一般提示性的消息information，它不会输出Log.v和Log.d的信息，但会显示i、w和e的信息

4、Log.w的意思为**橙色**，可以看作为warning警告，一般需要我们注意优化Android代码，同时选择它后还会输出Log.e的信息。

5、Log.e为**红色**，可以想到error错误，这里仅显示红色的错误信息，这些错误就需要我们认真的分析，查看栈的信息了。

## Log使用

(String tag, String msg）

tag为标签，msg为提示信息