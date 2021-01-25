---
title: Collection集合操作
date: 2021-01-25 21:07:04
tags:
---

# List
## 迭代器使用lambda表达式实现删除
由于List列表中for循环删除多个元素会报错，如将一个列表和一个字符串比较，删除列表中不存在的元素，下列代码将会报错：
```java
List<String> list = new ArrayList<String>(Arrays.asList("1","2","3","4","5","6"));
String numbers = "1|2|3";
for(String str : list){
    if(!numbers.contains(str)){
        list.remove(str);
    }
}
```
这是由于每次删除元素时，list中的元素会向前移动，导致取下一个元素时会报错。
解决方式：
```java
for(int i = 0; i < list.size(); i++){
    String str = list.get(i);
    if(!numbers.contains(str)){
        list.remove(i);
        i--;
    }
}
```
或者采用方向遍历方式：
```java
for(int i = list.size()-1; i >= 0; i--){
    String str = list.get(i);
    if(!numbers.contains(str)){
        list.remove(i);
    }
}
```
或者采用迭代器方式：
```java
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()){
    String next = iterator.next();
    if(!numbers.contains(next)){
        iterator.remove();
    }
}
```
如果采用lambda表达式，只需1行代码即可搞定：
```java
list.removeIf(next->!numbers.contains(next));
```

