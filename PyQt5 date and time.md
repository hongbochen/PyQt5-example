PyQt5的这部分教程展示了如何使用PyQt5的日期和时间模块。

### QDate,QTime,QDateTime

PyQt5使用`QDate,QDateTime,QTime`类来操作日期和时间。`QDate`是一个以标准阳历的形式来操作日期的类。他有一些方法用来决定日期，比较或者是控制日期。`QTime`类操作时间。他提供了一些方法用来比较时间，决定时间和其他一些控制时间的方法。`QDateTime`是一个绑定`QDate`和`QTime`对象为一个对象的类。

### 当前日期和时间

PyQt5有`currentDate(),currentTime()`和`currentDateTime()`方法来决定当前日期和时间。

```

	#! /usr/bin/python3
	# -*- coding : utf-8 -*-
	
	from PyQt5.QtCore import QDate,QTime,QDateTime,Qt
	
	now = QDate.currentDate()
	
	print(now.toString(Qt.ISODate))
	print(now.toString(Qt.DefaultLocaleLongDate))
	
	datetime = QDateTime.currentDateTime()
	
	print(datetime.toString())
	
	time = QTime.currentTime()
	
	print(time.toString(Qt.DefaultLocaleLongDate))

```
上面的示例以不同的格式打印了当前的日期，当前的日期和时间，还有时间。

```
now = QDate.currentDate()
```

函数`currentDate()`返回当前的日期。

```
print(now.toString(Qt.ISODate))
print(now.toString(Qt.DefaultLocaleLongDate))

```

通过传递给`toString()`函数参数`Qt.ISODate`和`Qt.DefaultLocaleLongDate`来打印不同的日期格式。

```

datetime = QDateTime.currentDateTime()

```

`currentDateTime()`返回当前的日期和时间。

```

time = QTime.currentTime()

```

最后，`currentTime()`方法返回当前时间。


下面是最终的输出：

```

python current_date_time.py
2017-10-29
2017年10月29日
周日 10月 29 22:05:20 2017
22:05:20

```

### UTC时间

我们的星球是一个球体，它绕着它的轴旋转。地球从左向右转，所以，太阳从不同的地方在不同的时间升起。地球转一圈大约需要24个小时。因此，世界被分成了24个时区。在每一个时区，都有一个不同的本地时间。本地时间经常由于日光节约进一步修改。

有一个全球时间是一个实际的需求。一个全球时间能够帮助避免关于时区和日光节约时间的误解。UTC(协调世界时)被选用作为基本的时间标准。UTC被用于航空，天气预报，航班计划，航空交通控制审核和地图中。不像本地时间一样，UTC不会随着季节的变化而变化。

```

	#UTC
	
	now = QDateTime.currentDateTime()
	
	print("Local datetime: ", now.toString(Qt.ISODate))
	print("Universal datetime: ", now.toUTC().toString(Qt.ISODate))
	
	print("The offset from UTC is: {0} seconds".format(now.offsetFromUtc()))


```

上面的例子程序确定了当前的国际和本地日期和时间。

```

	print("Local datetime: ", now.toString(Qt.ISODate))

```
`currentDateTime()`方法返回表达为本地时间的当前日期和时间。我们可以使用`toLocalTime()`来讲国际事件转换为一个本地时间。

```

	print("Universal datetime: ",now.toUTC().toString(Qt.ISODate))

```
我们使用`toUTC()`方法从日期时间对象中来获得国际时间。

```

	print("The offset from UTC is: {0} seconds".format(now.offsetFromUtc()))

```
`offsetFromUtc()`以秒的形式给出了国际时间和本地时间的差距。
 
下面是该一小段代码的输出：

```

	Local datetime:  2017-11-02T01:11:40
	Universal datetime:  2017-11-01T17:11:40Z
	The offset from UTC is: 28800 seconds

```

### 天数

在某个月的天数是由`daysInMonth()`方法返回的，在某年的天数是由`daysInYear()`方法返回的。


```

	#!/usr/bin/python3
	
	from PyQt5.QtCore import QDate,Qt
	
	now = QDate.currentDate()
	
	d = QDate(1945,5,7)
	
	print("Days in month: {0}".format(d.daysInMonth()))
	print("Days in year: {0}".format(d.daysInYear()))

```

这个例子打印出了在被选择日期的一个月和年的天数。

下面是输出：

```

	Days in month: 31
	Days in year: 365

```

### 日期之间的差

`daysTo()`方法返回了从一个日期到另外一个日期的天数。

```

	#!/usr/bin/python3
	
	from PyQt5.QtCore import QDate
	
	xmas1 = QDate(2016,12,24)
	xmas2 = QDate(2017,12,24)
	
	now = QDate.currentDate()
	
	dayspassed = xmas1.daysTo(now);
	print("{0} days hace passwd since last XMas".format(dayspassed))
	
	nofdays = now.daysTo(xmas2)
	print("There are {0} days until next XMas".format(nofdays))


```

这个例子计算了从上一个XMas过去的天数和直到下一个XMas还有多少天。

下面是这个例子的输出：

```

	313 days hace passwd since last XMas
	There are 52 days until next XMas

```

### 时间计算

我们经常对一个时间值增加或减去天数，秒数或年数。

```

	#!/usr/bin/python3
	
	from PyQt5.QtCore import QDateTime,Qt
	
	now = QDateTime.currentDateTime()
	
	print("Today:",now.toString(Qt.ISODate))
	print("Adding 12 days: {0}".format(now.addDays(12).toString(Qt.ISODate)))
	print("Substracting 22 days: {0}".format(now.addDays(-22).toString(Qt.ISODate)))
	
	print("Adding 50 seconds: {0}".format(now.addSecs(50).toString(Qt.ISODate)))
	print("Adding 3 months: {0}".format(now.addMonths(3).toString(Qt.ISODate)))
	print("Adding 12 years:{0}".format(now.addYears(12).toString(Qt.ISODate))

```

该例子程序确定了当前时间增加或减去天数，秒数，月数和年数的值。

下面是该程序的输出：

```

	Today: 2017-11-02T01:55:42
	Adding 12 days: 2017-11-14T01:55:42
	Substracting 22 days: 2017-10-11T01:55:42
	Adding 50 seconds: 2017-11-02T01:56:32
	Adding 3 months: 2018-02-02T01:55:42
	Adding 12 years:2029-11-02T01:55:42

```


