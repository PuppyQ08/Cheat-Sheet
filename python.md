# Python usage cheat sheet.

# Read and Write files
- Any file type
```
With open("./test.dat") as f:
    lines = f.readlines() #lines is a list of each line in string
    lines[0].split() #split string by space 
    lines[0].split(",",3) #split by "," and only have former 3 split (rest will merge as one)

```
- For csv
```
import csv
with open('test.csv', newline='') as c: #newline is to let python do newline itself.
    reader = csv.reader(c,delimiter =' ')
    for row in reader:
        print(row[0])
```
# argparse

# python memoization
`@lru_cache(maxsize=128,typed=False)`
It will store the most recent call to this function then we can reuse.

# string operation
`firstoccurence,-1 = text.find(substring,startindex,endindex)` 
search the substring in the start and end period and return the first index,
`rfind` return the last index.

# custom sort
```python
l1 = [(3,'aaa'),(2,'bbb')]
sorted(l1,key = lambda x: (-x[0],x[1]))
# first sort by number in descending order then if equal sort by string in ascending order.
# it can be used to sort on list based on the other list
# but you need to zip(list1,list2) first

l1 = [1,2,3,4]
sorted(l1,key = lambda x: x**3)#sort in cubic value
```
