# Dictionaries

Declaration and how to add elements to corresponding keys in dictionary

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
```

- .items() → outputs everything in the dictionary *IMPORTANT*

# Hashsets and Arrays

- can use “in” keyword to check hashset
- A string can be treated as a set()
- use the .count(i) to quickly count + iterate the hashset to count each character (anagram)

### Special Commands (python)

.get() method: arr.get(keyname, value)

.count() method: [1, 2, 3,4] → arr.count(2) returns 1 (count a value)

.items() method: prints out the type of obj + its index + elements

numset = set(nums): can straight up key value map a list to a set 

Declaration + Contains Duplicate:

```python
#contains duplicate
hashset = set()

for n in nums:
	if n in hashset:
		return True
	hashset.add(n)

return False

```

using set in loops :

Valid Anagram:

```python
			string1, string2 = {}, {}
       if len(s) != len(t):
            return False
        for i in range(len(s)):
            string1[s[i]] = 1 + string1.get(s[i],0)
            string2[t[i]] = 1 + string2.get(t[i], 0)
        if string1 == string2:
            return True
        return False
```

Using keys and values to solve problem

Two Sum:

```python
prevMap = {}

for i, n in enumerate(nums)
	diff = target - n
	if diff in prevMap:
		return [prevMap[diff], i]
	prevMap[n] = i
return null
```

Group Anagram:

```
def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list) #map charCount to List

        for i in strs:
            count = [0] * 26 #a ... z
            for c in i:
                count[ord(c) - ord('a')] += 1#ascii order essentially confers to number
            res[tuple(count)].append(i) #list cant take [], make it tuple
        return list(res.values()) #retrn values not grouped
```

Top K Freq Elements:

```python
# use bucket sort, create list of values in an array that the index 
# maps to the count of the value (value = the integer that appears)
def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        hashmap = {}
        for n in nums:
            hashmap[n] = 1 + hashmap.get(n, 0)
        
        arr = []
        for i, n in hashmap.items():
            arr.append([n, i])
        arr.sort()
        res = []
        while len(res) < k:
            res.append(arr.pop()[1])
        return res
        
```

Valid Sudoku:

- create default dic for col, row, square
- Int division //3 for sudoku boxes

```python
def isValidSudoku(self, board: List[List[str]]) -> bool:
        cols = collections.defaultdict(set)
        rows = collections.defaultdict(set)
        squares = collections.defaultdict(set) #key = (r/3, c/3)

        for r in range(9):
            for c in range(9):
                if board[r][c] == ".":
                    continue #no num
                #check row -> row
                #check col-> col
                if (board[r][c] in rows[r]) or (board[r][c] in cols[c]) or(board[r][c] in squares[(r//3, c//3)]):
                    return False
                cols[c].add(board[r][c])
                rows[r].add(board[r][c])
                squares[(r//3, c//3)].add(board[r][c])
        return True
```

## String Manip w Python

- [i : j] aka Slice → [start: stop: step] step can be -1 so it decreases by 1 pre much (reverses)
    - continue the in range(start: stop: step) follows same syntax (range(len(nums) - 1, -1, -1)
- int() → converts value to an integer

Encode Decode:

```jsx
def encode(self, strs: List[str]) -> str:
        res = ""
        for s in strs:
            #length of s then delimiter (#) + s
            res += str(len(s)) + "#" + s
        print(res)
        return res
    def decode(self, s: str) -> List[str]:
        res, i = [], 0
        while i < len(s):
            j = i
            while s[j] != "#":
                j+=1
            length = int(s[i:j])
            res.append(s[j + 1: j + 1 + length])
            i = j+ 1 + length
        return res
```

Product Except Self:

- iterate through once multiplying each by prev then go back from length + 1

```python
def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1] * len(nums)
        prefix = 1
        for i in range(len(nums)):
            res[i] = prefix
            prefix *= nums[i]
        postfix = 1
        for i in range(len(nums) -1, -1, -1):
            #starts at last val + 1 (init 1)
            res[i] *= postfix
            postfix *= nums[i]
        return res
```

Longest Consecutive Sequence:

- no left neighbor = not start of seq
- put into set and check if there is a neighbor (i.e. n - 1 or n + 1)
- if no left neighbor begin counting up (1, 2, 3, 4, etc)
- then count the longest length sequence.

```python
def longestConsecutive(self, nums: List[int]) -> int:
        #conv to set directly
        numset = set(nums)
        longest = 0

        for i in nums:
            if (i-1) not in numset:
                length = 0
                while (i + length) in numset:
                    length += 1
                longest = max(length, longest)
        return longest
```
