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
