
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
- 01) 如果存在实例，则将它上面的Activity实例都出栈，然后回调启动的Activity实例的onNewIntent方法
- 02) 如果不存在该实例，则新建Activity，并入栈
#### 4.2 应用场景
singleTask适合作为程序入口点。
例如浏览器的主界面。不管从多少个应用启动浏览器，只会启动主界面一次，
其余情况都会走onNewIntent，并且会清空主界面上面的其他页面。
之前打开过的页面，打开之前的页面就ok，不再新建。

### 五，singleInstance
#### 5.1 总结
当activity使用该种启动模式时，会单为此activity开辟一个新的栈来存放此activity。这种模式相当于我们一个应用只有一个实例，其实就是单例模式；
