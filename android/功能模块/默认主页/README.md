## 默认主页
快速集成主页功能，默认底下会有四个tab，并且提供tab fragment。

### 特点
前面我们分别利用ViewPager和Fragment实现了Tab效果。但是使用Fragment实现的Tab不能够左右滑动。如果我们既想使用Fragment又想让Tab能够滑动。所以会重写 ViewPager 来拦截它的滑动事件，去阻止手动滑动，而只能通过点击 tab 来实现。