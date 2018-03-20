
### 一，关于任务栈
当程序创建时就会创建一个任务栈，用于存储程序中的Activity.当同时创建一个Activity时，会创建多个实例，并按照先后顺序会进入栈内。
并且只有任务栈中的所有Activity全部清除后，任务栈才会被销毁。这样及其不合理。

> 所以有了Android的四种启动模式：
> standard singleTop singleTask singleInstance

### 二，standard 启动模式
每次跳转系统都会在task中生成新的Activity实例，并且放在栈顶的位置；当按back键时，依次退出。
这就是standard模式（默认启动模式），不管有么有已经存在的实例，都生成新的实例。

### 三，singleTop（栈顶服用模式）
#### 3.1 总结：
- 01) 如果新创建的Activity已经位于栈顶，那么这个Activity不会重复创建新的实例，同时会调用Activity中的onNewIntent()的方法；
- 02) 如果新创建的Activity不在栈顶或者栈内没有，同standard模式一样；
#### 3.2 应用场景
比如消息推送页面，当点击推送打开新的Activity时，可以设置为SingleTop，否则比如来5条，你每次打开都会新建Activity;

### 四，SingleTask (栈内复用模式)
#### 4.1 总结：
- 01)
- 02)
#### 4.2 应用场景
