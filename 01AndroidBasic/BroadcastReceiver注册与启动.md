### 一，注册方式
#### 1.1 动态注册方式

      // 1.1.1 定义广播
      public class MyBroadCastReceiver extends BroadcastReceiver   
      {  
         @Override  
         public void onReceive(Context context, Intent intent)   
         {   
            //get data
         }   
      }

      // 1.1.2 注册
      MyBroadCastReceiver yBroadCastReceiver = new MyBroadCastReceiver();
      IntentFilter intentFilter = new IntentFilter("android.provider.Telephony.SMS_RECEIVED");
      myContext.registerReceiver(smsBroadCastReceiver,intentFilter,"android.permission.RECEIVE_SMS", null);

#### 1.2 静态注册

        // 1.2.1 定义广播
        public class MyBroadCastReceiver extends BroadcastReceiver   
        {  
           @Override  
           public void onReceive(Context context, Intent intent)   
           {   
              //get data
           }   
        }

        <!-- 1.2.1  清单文件中注册 -->
        <receiver android:name=".MyBroadCastReceiver">  
            <!-- android:priority属性是设置此接收者的优先级（从-1000到1000） -->
            <intent-filter android:priority="20">
            <actionandroid:name="android.provider.Telephony.SMS_RECEIVED"/>  
            </intent-filter>  
        </receiver>


### 二，发送广播
- 通过mContext.sendBroadcast(Intent)或mContext.sendBroadcast(Intent, String)发送的是无序广播(后者加了权限)；
- 通过mContext.sendOrderedBroadcast(Intent, String, BroadCastReceiver, Handler, int, String, Bundle)发送的是有序广播。
