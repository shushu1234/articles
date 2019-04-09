# Sorting a HashMap In Java

> 在这篇文章中，我们将介绍如何对HashMap进行排序，我们将讨论如何通过键或者值对HashMap进行排序。

为了下面文章的演示，我们先构造一个HashMap

```java
@Data
@AllArgsConstructor
class Student{
    private Integer id;
    private String name;

    @Override
    public String toString() {
        return "{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}
HashMap<Integer,Student> map=new HashMap<>();

@BeforeMethod
public void constructHashMap(){
    map.put(1003, new Student(1003, "Sam"));
    map.put(1005, new Student(1005, "Joseph"));
    map.put(1001, new Student(1001, "Kate"));
    map.put(1002, new Student(1002, "Miranda"));
    map.put(1004, new Student(1004, "Peter"));
}
```

上面创建一个Student类并使用Lombok来构造Getter和Setter方法。

## 1. 通过TreeMap

因为TreeMap的内部是有序的，它默认的排序策略是根据key来进行排序，所以我们可以将HashMap中的元素放到TreeMap中来实现排序：

**1. 通过构造函数来创建**

```java
@Test
public void useTreeMap1() {
	TreeMap<Integer, Student> sortedMap = new TreeMap<>(map);
	System.out.println(sortedMap);
}
```

**2. 调用putAll()方法**

```java
@Test
public void useTreeMap2() {
	TreeMap<Integer, Student> sortedMap = new TreeMap<>();
	sortedMap.putAll(map);
	System.out.println(sortedMap);
}
```

输出结果为：

```java
{1001={id=1001, name='Kate'}, 1002={id=1002, name='Miranda'}, 1003={id=1003, name='Sam'}, 1004={id=1004, name='Peter'}, 1005={id=1005, name='Joseph'}}
```

## 2. 通过ArrayList

如果我们只想对key或者value进行排序，而不是对整个map进行排序，我们可以通过ArrayList。

```java
@Test
public void useArrayList() {
    List<Integer> mapKeys = new ArrayList<>(map.keySet());
    Collections.sort(mapKeys);
    System.out.println(mapKeys);

    List<Student> mapValues = new ArrayList<>(map.values());
    Collections.sort(mapValues, (s1, s2) -> s1.id.compareTo(s2.id));
    System.out.println(mapValues);
}
```

上面对key排序直接使用keySet()构造，但是如果要对value进行排序，那么我们Student需要基础Comparable接口，我们这里使用lambda表达式实现的，而不是采用继承接口。

## 3. 通过TreeSet

如果我们还打算避免在生成的键或值列表中出现任何重复，我们可以选择TreeSet：

```java
@Test
public void useTreeSet() {
    TreeSet<Integer> mapKeys = new TreeSet<>(map.keySet());
    System.out.println(mapKeys);
}
```

同样的，我们也可以对value使用TreeSet排序。

## 4. 通过Java8的Streams

使用Stream按key进行排序

```java
Map<Integer, Student> sortedMap = map.entrySet()
                                  .stream()
                                  .sorted(Map.Entry.comparingByKey())
                                  .collect(Collectors
                                    .toMap(Map.Entry::getKey,
                                           Map.Entry::getValue,
                                           (e1, e2) -> e1,
                                           LinkedHashMap::new));
```

如果要按value进行排序

```java
Map<Integer, Student> sortedMap = map.entrySet()
                                  .stream()
                                  .sorted(Map.Entry.comparingByValue())
                                  .collect(Collectors
                                    .toMap(Map.Entry::getKey,
                                           Map.Entry::getValue,
                                           (e1, e2) -> e1,
                                           LinkedHashMap::new));
```

如果我们要按逆序进行排序，则使用`Collections.reverseOrder()`

```java
 Map<Integer,Student> sortMapDesc= map.entrySet()
                .stream()
                .sorted(Collections
                        .reverseOrder(Map.Entry.comparingByKey()))
                .collect(Collectors
                        .toMap(Map.Entry::getKey,Map.Entry::getValue,(e1,e2)->e1,LinkedHashMap::new));
```

