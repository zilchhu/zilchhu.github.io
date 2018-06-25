---
layout: post
title: Core concepts of RxJava2
---
Rxjava2的核心理念是“观察者模式"，即"观察者"观察"被观察者"。举一个简单的例子：
{% highlight java %}
Observable<Time> clock =
        Observable.create(emitter -> {
            Time time = getTime()
            emitter.onNext(time)
})
{% endhighlight %}
时钟作为一个被观察者，源源不断地产生时间。
{% highlight java %}
DisposableObserver<Time> you =
        clock.subscribeWith(new
                DisposableObserver(Time) {
                    @override
                    public void onNext(Time time) {
                        youDoSomething(time) or
                        seeSomebodyDoSomething(time)
                    }
})
{% endhighlight %}
你作为一个观察者，订阅时钟，获得时间。你根据时间做着自己该做、想做的事，或者看着别人做他或他们该做、想做的事。
最后的最后
{% highlight java %}
if(youAreDying()) {
    if(you != null && !you.isDisposed) {
        you.disposed()
    }
}
{% endhighlight %}
当你离开这个世界，时间对你已毫无意义，你取消订阅，与时钟断开联系。
