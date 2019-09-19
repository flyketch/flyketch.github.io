## java 中将时间增加一分钟

### first
```
Date date = new Date();

Date newDate = new Date(date.getTime() + 60000);

```

### second
```
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
Date now = new Date();
System.out.println("当前时间：" + sdf.format(now));

Calendar nowTime = Calendar.getInstance();
nowTime.add(Calendar.MINUTE, 6);
System.out.println(sdf.format(nowTime.getTime()));
```