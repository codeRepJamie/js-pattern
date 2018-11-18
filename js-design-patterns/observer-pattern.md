#观察者模式
> Observer Pattern

##实现一个小需求
1.  实现一个可以不断生成checkbox（check）的button(addNewObserver)
1.  实现一个checkbox(controlCheckbox)，可以控制页面上所有addNewObserver生成的check的状态

##知识点一：定义
***Subject*** （目标）
维护一个观察者列表，可以添加删除任意一个观察者

***Observer*** （观察者）
负责提供一个接口（当目标状态发生改变时候，具体要怎样做）

***ConcreteSubject*** （具体目标）
主要有两个职责：
1.  储存当前ConcreteSubject的状态
1.  状态发生改变时，向Observer发出通知

***ConcreteObserver*** （具体观察者）
主要有两个职责：
1.  储存一个指向ConcreteSubject的引用
1.  实现Observe的更新接口，实现自身状态和目标状态保持一致

##知识点二：具体实行代码
[source code](https://jsfiddle.net/jamiexTsang/s2dh19mu/5/#height=500&type=frame&tabs=js,html,result&theme=dark)

####分析代码
***Subject*** （目标）
即是当前的Subject类。它内置observers属性，透过它来负责管理一个ObserverList实例。它拥有添加（Subject.prototype.addObserver）、删除（Subject.prototype.removeObserver）一个观察者，通知观察者（Subject.prototype.notify）的能力。

***Observer*** （观察者）
即是Observer类，提供了状态改变时获得通知对象（check），提供一个名为update的接口

***ConcreteSubject*** （具体目标）
即本例里面的controlCheckbox，案例中职责分别为：
1.  透过执行extend( controlCheckbox, new Subject() );保存了目标实例
1.  当它被点击时候，向Observer发出通知，执行了controlCheckbox.notify( controlCheckbox.checked );

***ConcreteObserver*** （具体观察者）
即本例里面的check，案例中职责分别为：
1.  透过执行controlCheckbox.addObserver(check) 储存一个指向ConcreteSubject的引用
1.  通过覆写 check.update 实现自身状态和目标状态保持一致

##知识点三：发布订阅模式，及与观察者模式区别