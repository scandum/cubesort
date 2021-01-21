Intro
-----
This document describes a stable partitioning comparison sort named cubesort.

Binary Cube
-----------
Cubesort sorts data by storing data in a [binary cube](https://github.com/scandum/binary_cube), multidimentional balanced array.

Binary Search
-------------
In order to sort 1 element, 3 [monobound binary searches](https://github.com/scandum/binary_search) are performed to pin point the bucket where the element should be stored.

Overflow
--------
Once a bucket overflows it is sorted by [quadsort](https://github.com/scandum/quadsort) and the content is split between two buckets.

Finish
------
Once all elements have been inserted into the cube, all unsorted buckets are sorted. Since the buckets are already in order the sort is finished.

Big O
-----
|     Name | Best | Average |   Worst | Stable | Partitioning | Memory |
| -------- | ---- | ------- | ------- | ------ | -------------| ------ |
| cubesort |    n | n log n | n log n |    yes |          yes |      n |

Cubesort makes n comparisons when the data is already sorted or reverse sorted.

Benchmarks
----------
The following benchmark was on WSL gcc version 7.4.0 (Ubuntu 7.4.0-1ubuntu1~18.04.1).
The source code was compiled using g++ -O3 -w -fpermissive bench.c. Each test was ran
100 times and only the best run is reported.

|      Name |    Items | Type |     Best |  Average | Repetitions |     Distribution |
| --------- | -------- | ---- | -------- | -------- | ----------- | ---------------- |
| std::sort |   100000 |  i32 | 0.005530 | 0.005565 |           1 |     random order |
|  gridsort |   100000 |  i32 | 0.004708 | 0.004736 |           1 |     random order |
|           |          |      |          |          |             |                  |
| std::sort |   100000 |  i32 | 0.000943 | 0.001046 |           1 |  ascending order |
|  gridsort |   100000 |  i32 | 0.000275 | 0.000280 |           1 |  ascending order |
|           |          |      |          |          |             |                  |
| std::sort |   100000 |  i32 | 0.003193 | 0.003216 |           1 |    ascending saw |
|  gridsort |   100000 |  i32 | 0.001570 | 0.001583 |           1 |    ascending saw |
|           |          |      |          |          |             |                  |
| std::sort |   100000 |  i32 | 0.002931 | 0.002965 |           1 |    generic order |
|  gridsort |   100000 |  i32 | 0.001830 | 0.001851 |           1 |    generic order |
|           |          |      |          |          |             |                  |
| std::sort |   100000 |  i32 | 0.000739 | 0.000774 |           1 | descending order |
|  gridsort |   100000 |  i32 | 0.000251 | 0.000257 |           1 | descending order |
|           |          |      |          |          |             |                  |
| std::sort |   100000 |  i32 | 0.002765 | 0.002775 |           1 |   descending saw |
|  gridsort |   100000 |  i32 | 0.001139 | 0.001200 |           1 |   descending saw |
|           |          |      |          |          |             |                  |
| std::sort |   100000 |  i32 | 0.003713 | 0.003729 |           1 |      random tail |
|  gridsort |   100000 |  i32 | 0.001385 | 0.001398 |           1 |      random tail |
|           |          |      |          |          |             |                  |
| std::sort |   100000 |  i32 | 0.004755 | 0.004782 |           1 |      random half |
|  gridsort |   100000 |  i32 | 0.002541 | 0.002558 |           1 |      random half |

Source code
-----------
Coming soon-ish.
