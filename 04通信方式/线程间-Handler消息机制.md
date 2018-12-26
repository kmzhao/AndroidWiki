### 一，引入原因
Handler主要用于异步线程间的通信；Google规定，只有在主线程才可以更新UI,但是我们如果在主线程绘制复杂的耗时操作，很容易引起ANR。在Android中最常使用Handler的场景就是主线程调用子线程去进行网络访问，子线程在获取到网络访问的返回结果并处理数据之后，通知主线程去更新UI。

### 二，使用方式
#### 2.1 获取Handler

    public class TestActivity extends Activity{
        Handler mHandler = new Handler() {
          @Override
          public void handleMessage(Message msg) {
              switch (msg.what) {
                  case 0:
                      doSomething();
                      break;
                  default:
                      break;
              }
          }
        };
    }

#### 2.2 发送消息
##### 2.2.1 获取发送对象
> 获取消息包括Runnable对象和message对象两种，获取Message的方式包括：

- 1 直接new一个Message，设置what等参数（不推荐）
- 2 通过handler获取复用的Message（推荐）

        handler.obtainMessage()
        handler.obtainMessage(int what)
        obtainMessage(int what, Object obj)

##### 2.2.2 发送消息的相关方法

      post(Runnable)
      postAtTime(Runnable,long)
      postDelayed(Runnable long)
      sendEmptyMessage(int)
      sendMessage(Message) 将消息发送到消息队列
      msg.sendToTarget() 将消息发送到消息队列
      sendMessageAtTime(Message,long) 定时将消息发送到消息队列
      sendMessageDelayed(Message,long) 延迟一定时间后，将消息发送到消息队列

### 三，源码分析

### 四，注意事项

### 参考文章
