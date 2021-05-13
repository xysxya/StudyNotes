# Calender 类

Calendar类即日历类，常用于进行“翻日历”，比如下个月的今天是多久

## Calender 与 Date 转换

```java
package date;

import java.util.Date;
import java.util.Calendar;

public class TestDate {
    public static void main(String[] args) {
        Calendar c=Calendar.getInstance();
        System.out.println(c);
        Date d=c.getTime();
        System.out.println(d);
        Date d2=new Date(0);
        System.out.println(d2);
        c.setTime(d2);
        System.out.println(c);
    }
}
```
运行结果
```
java.util.GregorianCalendar[time=1619404582250,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2021,MONTH=3,WEEK_OF_YEAR=18,WEEK_OF_MONTH=5,DAY_OF_MONTH=26,DAY_OF_YEAR=116,DAY_OF_WEEK=2,DAY_OF_WEEK_IN_MONTH=4,AM_PM=0,HOUR=10,HOUR_OF_DAY=10,MINUTE=36,SECOND=22,MILLISECOND=250,ZONE_OFFSET=28800000,DST_OFFSET=0]

Mon Apr 26 10:36:22 CST 2021
Thu Jan 01 08:00:00 CST 1970

java.util.GregorianCalendar[time=0,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="Asia/Shanghai",offset=28800000,dstSavings=0,useDaylight=false,transitions=31,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=1970,MONTH=0,WEEK_OF_YEAR=1,WEEK_OF_MONTH=1,DAY_OF_MONTH=1,DAY_OF_YEAR=1,DAY_OF_WEEK=5,DAY_OF_WEEK_IN_MONTH=1,AM_PM=0,HOUR=8,HOUR_OF_DAY=8,MINUTE=0,SECOND=0,MILLISECOND=0,ZONE_OFFSET=28800000,DST_OFFSET=0]


```

## 翻日历

add方法，在原日期上增加年/月/日

set方法，直接设置年/月/日

```java
package date;

import java.util.Date;
import java.util.Calendar;
import java.text.SimpleDateFormat;

public class TestDate {
    //values
    private static SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

    //methods
    private static String format(Date time){
        return sdf.format(time);
    }
    public static void main(String[] args) {
        Calendar c=Calendar.getInstance();
        Date now=c.getTime();

        //Current Date
        System.out.println("Current Date :\t"+ format(c.getTime()));

        //Today next month
        c.setTime(now);
        c.add(Calendar.MONTH,1);
        System.out.println("Today next month:\t"+format(c.getTime()));

        //In last year's today
        c.setTime(now);
        c.add(Calendar.YEAR,-1);
        System.out.println("In last year's today:\t"+format(c.getTime()));


    }
}
```
运行结果
```
Current Date :	2021-04-26 10:52:38
Today next month:	2021-05-26 10:52:38
In last year's today:	2020-04-26 10:52:38
```