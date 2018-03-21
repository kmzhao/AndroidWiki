### 一，两种开启方式
startService和bindService;

### 二，startService
#### 2.1 生命周期：
- onCreate()--->onStartCommand()（onStart()方法已过时） ---> onDestory()
> 如果服务已经开启，不会重复的执行onCreate()， 而是会调用onStart()和onStartCommand()。、

#### 2.2 特点：
一旦服务开启跟调用者(开启者)就没有任何关系了。开启者退出了，开启者挂了，服务还在后台长期的运行。开启者不能调用服务里面的方法。

### 三，bindService
#### 3.1 生命周期
onCreate() --->onBind()--->onunbind()--->onDestory()
#### 3.2 特点：
bind的方式开启服务，绑定服务，调用者挂了，服务也会跟着挂掉。
绑定者可以调用服务里面的方法。
