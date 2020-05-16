# Multi-Key Dictionary Sorting

Take a file called `test.json` like the following:
```json
{"uid":10069,"message":"test 2","epochNs":873631220,"epochSec":1587729898}
{"uid":10069,"message":"test 3","epochNs":214531329,"epochSec":1587729899}
{"uid":10069,"message":"test 1","epochNs":116541029,"epochSec":1587729898}
```
We need to sort this list based on two keys, `epochSec` and then `epochNs` so it would then become:
```json
{"uid":10069,"message":"test 1","epochNs":116541029,"epochSec":1587729898}
{"uid":10069,"message":"test 2","epochNs":873631220,"epochSec":1587729898}
{"uid":10069,"message":"test 3","epochNs":214531329,"epochSec":1587729899}
```

To sort this, the following code works:
```python
import json
from operator import itemgetter 

j = []

try:
    with open("test.json") as f:
        json_lines = f.readlines()
except Exception as e:
    print("error: couldn't open file for reading: ", e)
    sys.exit(100)

# Read line-by-line, put into list
for json_object in list(json_lines):
    j.append(json.loads(json_object))

f.close()

print("Unsorted:")
print(j)

# now sort it "in place" using operator itemgetter()
j = sorted(j, key=itemgetter('epochSec', 'epochNs'))

print("Sorted:")
print(j)
```

More documentation available here:
* [https://stackoverflow.com/questions/1143671/python-sorting-list-of-dictionaries-by-multiple-keys](https://stackoverflow.com/questions/1143671/python-sorting-list-of-dictionaries-by-multiple-keys)