# Introduction

In this assignment, you'll write a program that willget you familiar with writing
multi-threaded programs in Rust.

## Learning Outcomes

```
● Write simple programs in Rust (Module 9, MLO 2)
● Compile, debug, manage and run Rust programs (Module9, MLO 3)
● Explain the facility for threads provided by Rust(Module 10, MLO 2)
```
# Map Reduce

According tothe Wikipedia article on MapReduce

```
(Links to an external site.)
```
MapReduce is a programming model and an associatedimplementation for processing
and generating big data sets with a parallel, distributedalgorithm on a cluster.

A MapReduce program is composed of a map procedure,which performs filtering and
sorting (such as sorting students by first name intoqueues, one queue for each name),
and a reduce method, which performs a summary operation(such as counting the
number of students in each queue, yielding name frequencies).

# Instructions

For this assignment, we are providing you with asingle-threadedRust program


```
(Links to an external site.)
```
that processes input numbers to produce a sum. Theprogram contains extensive
comments that explain the functionality and give directionson what parts of code you
are allowed to change (look for comments startingwith CHANGE CODE).

Here is a description of the program: currently themain()function does the following

```
● Generates data for the rest of the program
○ Callsgenerate_data()to generates a vector of numbersthat
serves as input for the rest of the program.
● Partitions the data
○ Callspartition_data_in_two()which partitions theinput
numbers into two partitions
● Performs the map step
○ Callsmap_data()for each of the two partitions, which returns the
sum of all the numbers in that partition.
● Performs the reduce step
○ Gathers the intermediate results produced by eachcall to
map_data()
○ Callsreduce_data()that sums up the intermediateresults
produced by the map step to produce the final sumof all the input
numbers.
```
You have to modify the program to accomplish the followingtasks:

```
● Modify the program to create 2 threads, each of whichconcurrently runs the
map_data()function on one of the two partitions createdby the program
given to you.
● Add code for the functionpartition_data()to partitionthe data into
equal-sized partitions based on the argumentnum_partitions
○ In case num_elements is not a multiple of num_partitions,some
partitions can have one more element than other partitions
● Add code to the functionmain()to
○ Partition the data into equal-size partitions
```

```
○ Create as many threads as the number of partitions and have each
thread concurrently run themap_data()function toprocess one
partition each
○ Gather the intermediate results returned by each thread
○ Run the reduce step to process the intermediate resultsand
produce the final result
```
See detailed comments in the provided program to seehow you can go about making
the required changes.

# Example Usage

Here are some example executions of the program.

An execution of the program with 5 partitions and150 elements.

```
● Since the number of elements is a multiple of thenumber of partitions, it is
required that each partition should have the samenumber of elements.
● However, there is no requirement about which elementis put into which
partition. Thus the intermediate sums in your solutioncan be different from
what is shown below.
```
./main 5 150

Number of partitions = 2

```
size of partition 0 = 75
```
```
size of partition 1 = 75
```
Intermediate sums = [2775, 8400]


## Intermediate sums = [435, 1335, 2235, 3135, 4035]

- Sum =
- Number of partitions =
   - size of partition 0 =
   - size of partition 1 =
   - size of partition 2 =
   - size of partition 3 =
   - size of partition 4 =
- Sum =
- ./main An execution of the program with 6 partitions and150 elements.
- Number of partitions =
   - size of partition 0 =
   - size of partition 1 =


Sum = 11175

Number of partitions = 6

```
size of partition 0 = 25
```
```
size of partition 1 = 25
```
```
size of partition 2 = 25
```
```
size of partition 3 = 25
```
```
size of partition 4 = 25
```
```
size of partition 5 = 25
```
Intermediate sums = [300, 925, 1550, 2175, 2800, 3425]

Sum = 11175

An execution of the program with 5 partitions and153 elements.

```
● In this example the number of elements is not a multipleof the number of
partitions.
● Based on the requirement that some partitions canhave one element more
than other partitions, in this case 3 partitions musthave 31 elements and 2
partitions must have 30 elements.
● In the example shown below, the 3 partitions with31 elements are at position
0, 1 and 2 in the vector of partitions, and the 2partitions with 30 elements are
at position 3 and 4 in that vector. However, thereis no requirement about the
order in which partitions that have one more elementthan other partitions
```

```
appear in the vector of partitions. Thus, the order of the partitions in your
solution can be different from what is shown below.
```
./main 5 153

Number of partitions = 2

```
size of partition 0 = 76
```
```
size of partition 1 = 77
```
Intermediate sums = [2850, 8778]

Sum = 11628

Number of partitions = 5

```
size of partition 0 = 31
```
```
size of partition 1 = 31
```
```
size of partition 2 = 31
```
```
size of partition 3 = 30
```
```
size of partition 4 = 30
```
Intermediate sums = [585, 1486, 2387, 3135, 4035]

Sum = 11628


# Hints

```
● The functionthread::spawn()
● (Links to an external site.)
● returnsJoinHandle<T>where T is the type of thereturn value of the
function the thread runs. This means that
○ Becausemap_data()returns an integer of typeusize
○ If you spawn a thread that runsmap_data()
○ thread::spawn()will return a value of typeJoinHandle<usize>
```
# What to turn in?

```
● Required: Upload one filemain.rswith all of yourcode.
○ When you resubmit a file in Canvas, Canvas can attacha suffix to
the file, e.g., the file name may becomemain-1.rs.Don't worry
about this name change as no points will be deductedbecause of
this.
● Optional: If you have any meta-comments about theprogram, create a file
README.txt with these comments, and upload it withyour submission as a
separate file (i.e., don't zip up the two files together).
```
# Grading Criteria

```
● This assignment is worth 8% of your final grade. Thebreakup of points is
given in the grading rubric.
● The grading will be done on os1.
● To test your program, we will compile the code asfollows
```
rustc main.rs

```
● We will run the program as follows
```

./main num_partitions num_elements

E.g.,

./main 5 150


