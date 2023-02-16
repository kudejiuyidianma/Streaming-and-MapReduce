# Streaming-and-MapReduce
## Background
- To implement prototypical streaming algorithms.
- To think through implementation of a novel streaming algorithm under the constraints of limited memory.
- To implement parts of a map reduce system in order to become familiar with what it must do behind the scenes.
- To implement an algorithm that can run in map reduce.

## Install
 ```
 pip install mmh3
 ```

## Part 1
### Task A: Mean RGB Values
Goal: Finding the mean of the rgb values at any point in the stream. 

Inputs are the color of a single sold cell phone case where the color is represented by a triple defining  (red, green, blue) with integers ranging from 1 to 1,000,000.
```
(r, g, b)
```

- Step1: Parsing rgb value into three integers when each stream element gets into the function.

- Step2: For each iteration, add rgb value to rsum, gsum and bsum.

- Step3: For each iteration, counter += 1

Thus, mean rgb value = rsum/cnt, gsum/cnt, bsum/cnt.

### Task B: Bloom Filter
Goal: Implement a bloom filter in order to find rgbs in the stream that match a given set of colors.

Req: Two triples of rgb values will be considered a match if each of the r, g, b values differ by less than 100.


- how to get the num of hashes?(false positive < 0.01)
The number of hashes required in a streaming algorithm to keep the false positive rate under 0.01 depends on several factors, such as the size of the data set and the chosen hash function. However, there is a general formula that can be used to estimate the number of hashes needed:

```
k = -log2(p) / log2(2）
```

where k is the number of hashes, p is the desired false positive rate (in this case, 0.01), and the denominator is the natural logarithm of 2.


- How to determine if two tuple rgb value are matched?
 
 
 
 ## Part 2: MapReduce System
 
    
    

