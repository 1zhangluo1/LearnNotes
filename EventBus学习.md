# EventBus学习

## 1.

​	EventBus能够在不同活动中给订阅该活动的活动发布一个事件，使得能够在不同活动中能够让别的活动中的方法得到实现，其功能类似于广播。

## 2.

EvenBus用法：

#### (1).

定义事件对象：

```java
public class MessageEvent {
    public String name;
}
public class MessageEvent {
    public MessageEvent(String name) {
        this.name = name;
    }

    public String name;
}

```

#### (2).

在接受活动的onCreate中注册并在onDestroy中注销事件：

```java
   @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EventBus.getDefault().register(this);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        EventBus.getDefault().unregister(this);
    }

```

#### (3).

订阅者接收事件：

```java
@Subscribe(threadMode = ThreadMode.MAIN)
    public void onMessageEvent(MessageEvent message) {
    //  DoSomething,放入需要调用的方法
}
```

#### (4).

发布事件：

发送事件是在需要调用另一个活动方法的活动中是实现的，通过EventBus中的Psot()方法发布事件，参数为上面自定义的MessageEvent，可以将携带的数据写入MessageEvent中，这里对象的类型要与接收事件的类型一致。

```java
EventBus.getDefault().post(new MessageEvent("接收到TwoActivity发送过来的事件啦"));

```

