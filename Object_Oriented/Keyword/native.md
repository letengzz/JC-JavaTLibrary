- 必须调用`Thread`实例的`start()`方法才能启动新线程，如果我们查看`Thread`类的源代码，会看到`start()`方法内部调用了一个`private native void start0()`方法，`native`修饰符表示这个方法是由JVM虚拟机内部的C代码实现的，不是由Java代码实现的。