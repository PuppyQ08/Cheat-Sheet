# array and list

## List

```java
List<Integer> List = new ArrayList<Integer>();
List.add(num);
List.add(index,num);
List.remove(index);
List.set(index,num);// replace 
List.size();
List.get(index);
List.subList(start,end);//end not included
```

## Array slicing

```java
import java.util.Arrays;

int [] slice = Arrays.copyOfRange(arr, start, end);
//{1,2,3,4,5} s = 1, e = 3,-> {2,3,4} so it is different from python[s:e]!!!
```
