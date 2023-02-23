# Streaming-and-MapReduce
# Background
- To implement prototypical streaming algorithms.
- To think through implementation of a novel streaming algorithm under the constraints of limited memory.
- To implement parts of a map reduce system in order to become familiar with what it must do behind the scenes.
- To implement an algorithm that can run in map reduce.

## Install
 ```
 pip install mmh3
 ```

# Part 1
## Task A: Mean RGB Values
Goal: Finding the mean of the rgb values at any point in the stream. 

Inputs are the color of a single sold cell phone case where the color is represented by a triple defining  (red, green, blue) with integers ranging from 1 to 1,000,000.
```
(r, g, b)
```

- Step1: Parsing rgb value into three integers when each stream element gets into the function.

- Step2: For each iteration, add rgb value to rsum, gsum and bsum.

- Step3: For each iteration, counter += 1

Thus, mean rgb value = rsum/cnt, gsum/cnt, bsum/cnt.

## Task B: Bloom Filter
Goal: Implement a bloom filter in order to find rgbs in the stream that match a given set of colors.

Req: Two triples of rgb values will be considered a match if each of the r, g, b values differ by less than 100.


- how to get the num of hashes?(false positive < 0.01)
The number of hashes required in a streaming algorithm to keep the false positive rate under 0.01 depends on several factors, such as the size of the data set and the chosen hash function. However, there is a general formula that can be used to estimate the number of hashes needed:

```
k = -log2(p) / log2(2）
```

where k is the number of hashes, p is the desired false positive rate (in this case, 0.01), and the denominator is the natural logarithm of 2.


- How to determine if two tuple rgb value are matched?
 
 
 
 # Part 2: MapReduce System
 ## Basic Algorithm
 Step1: The following two lists are shared by all processes in order to simulate the communication
 ```
 # Two array
 #stores the reducer task assignment and each key-value pair returned from mappers in the form: [(reduce_task_num, (k, v)), ...]
 namenode_m2r = Manager().list()
 
 #stores key-value pairs returned from reducers in the form [(k, v), ...]
 namenode_fromR = Manager().list()
 ```
 
 Step2:  Divide up the data into chunks accord to num_map_tasks, launch a new process for each map task, passing the chunk of data to it. 
  - Runs the mappers on each record within the data_chunk and assigns each k,v to a reduce task
  - Assign each kv pair to a reducer task
  
 Step3: Join map task processes back
 
 Step4: "send" each key-value pair to its assigned reducer by placing each into a list of lists, where to_reduce_task[task_num] = [list of kv pairs]
 
 Step5: Launch the reduce tasks as a new process for each. 
 
 Step 6: Join the reduce tasks back
  ```
 mapped_kvs = [] // used to store key-value pairs after map task
 ```
 
 For each key-value pair in data_chunk, 1) mapping, 2) get chunk_kvs, 3) store in the mapped_kvs
 
 ## Task A: Word Count MapReduce System
 Goal: Assign the key_value pair to the specific reduce task based on the reduce_task_num of the elements.
 
 Format of elements in namenode_m2r: [[reduce_task_num, (word_key, word_count)], [], [], ...]
 
 ## Task B: Mean RGB MapReduce System
 Goal: Implement map and reduce function to calculate the mean value of r, b, g.
 
 In the map task, we assign the value of red, blue and green a different key. This key indicates which reduce task will handle this key-value pair.
 
 In the reduce task, get the mean value for all red, blue and green individually.
 
 
 ## Task C: Matrix Multiplication MapReduce System
 Goal: Implement reduce function to implement matrix multiplication.
 
 Step1: separate m and n, keyed by j
 
 Step2: sum product of m and n js

