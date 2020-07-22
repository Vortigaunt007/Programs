# Spiral Order Matrix

Input

```cpp
[ [1, 2, 3], [4, 5, 6], [7, 8, 9] ]
```

Output

```cpp
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```

Solution

```cpp
vector<int> Solution::spiralOrder(const vector<vector<int> > &A) {
    int m = A.size(), n = A[0].size();
    int T = 0, B = m - 1, L = 0, R = n - 1; // top, bottom ...
    int dir = 0;
    
    vector<int> ans;
    
    while (T <= B && L <= R) {
        if (dir == 0) {
            for (int i = L; i <= R; i++)
                ans.push_back(A[T][i]);
            T++;
            dir = 1;
        } else if (dir == 1) {
            for (int i = T; i <= B; i++)
                ans.push_back(A[i][R]);
            R--;
            dir = 2;
        } else if (dir == 2) {
            for (int i = R; i >= L; i--)
                ans.push_back(A[B][i]);
            B--;
            dir = 3;
        } else if (dir == 3) {
            for (int i = B; i >= T; i--)
                ans.push_back(A[i][L]);
            L++;
            dir = 0;
        }
    }
    
    return ans;
}
```

# Sorting Algorithms

## Insertion Sort Algorithm

> Time Complexity = O(N^2) / O(N)  
> Space Complexity = O(1)  
> Stable

1. The first step involves the comparison of the element in question with its adjacent element.
2. And if at every comparison reveals that the element in question can be inserted at a particular position, then space is created for it by shifting the other elements one position to the right and inserting the element at the suitable position.
3. The above procedure is repeated until all the element in the array is at their apt position.

**Example**

**25** 17 31 13 2   ->   {swap 17 and 25}  ->  **17** **25** 31 13 2  ->  **17** **25** **31** 13 2  ->  {swap 13 and 31; swap 13 and 25; swap 13 and 17}  ->  **13** **17** **25** **31** 2  ->  ...  ->  **2** **13** **17** **25** **31**

### Pseudocode

```
INSERTION-SORT(A)
   for i = 1 to n
   	key ← A [i]
    	j ← i – 1
  	 while j > = 0 and A[j] > key
   		A[j+1] ← A[j]
   		j ← j – 1
   	End while 
   	A[j+1] ← key
  End for 
```

### Implementation C++

```cpp
void insertionSort(int arr[], int length) 
{
    int i, j, key;
    for (i = 1; i < length; i++) 
    {
        key = arr[i];
        j = i - 1;
        
        while (j >= 0 && arr[j] > key) 
        {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
        
    }
}
```

### Implementation Python

```python
def insertionSort(arr):
    # Traverse through 1 to len(arr)
    for i in range(1, len(arr)):
        key = arr[i]
        # Move elements of arr[0..i-1], that are
        # greater than key, to one position ahead
        # of their current position
        j = i-1
        while j >=0 and key < arr[j] :
            arr[j+1] = arr[j]
            j -= 1
        arr[j+1] = key 
```

## Merge Sort Algorithm

> Time Complexity = O(NlogN)  
> Space Complexity = O(N)  
> Stable

1. Divide the unsorted list into n sublists, each containing one element (a list of one element is considered sorted).
2. Repeatedly merge sublists to produce new sorted sublists until there is only one sublist remaining. This will be the sorted list.

### Implementation C++

```cpp
void merge(int *Arr, int start, int mid, int end) {
	// create a temp array
	int temp[end - start + 1];
    
	// crawlers for both intervals and for temp
	int i = start, j = mid+1, k = 0;

	// traverse both arrays and in each iteration add smaller of both elements in temp 
	while(i <= mid && j <= end) {
		if(Arr[i] <= Arr[j]) {
			temp[k] = Arr[i];
			k += 1; i += 1;
		}
		else {
			temp[k] = Arr[j];
			k += 1; j += 1;
		}
	}

	// add elements left in the first interval 
	while(i <= mid) {
		temp[k] = Arr[i];
		k += 1; i += 1;
	}

	// add elements left in the second interval 
	while(j <= end) {
		temp[k] = Arr[j];
		k += 1; j += 1;
	}

	// copy temp to original interval
	for(i = start; i <= end; i += 1) {
		Arr[i] = temp[i - start]
	}
}

// Arr is an array of integer type
// start and end are the starting and ending index of current interval of Arr

void mergeSort(int *Arr, int start, int end) {

	if(start < end) {
		int mid = (start + end) / 2;
		mergeSort(Arr, start, mid);
		mergeSort(Arr, mid+1, end);
		merge(Arr, start, mid, end);
	}
}
```

### Implementation Python

```python
def merge(Arr, start, mid, end) :

	# create a temp array
	temp[] = [0] * (end - start + 1)

	# crawlers for both intervals and for temp
	i, j, k = start, mid+1, 0

	# traverse both lists and in each iteration add smaller of both elements in temp 
	while(i <= mid and j <= end) :
		if(Arr[i] <= Arr[j]) :
			temp[k] = Arr[i]
			k += 1; i += 1
		else :
			temp[k] = Arr[j]
			k += 1; j += 1

	# add elements left in the first interval 
	while(i <= mid) 
		temp[k] = Arr[i]
		k += 1; i += 1

	# add elements left in the second interval 
	while(j <= end)
		temp[k] = Arr[j]
		k += 1; j += 1

	# copy temp to original interval
	for(i = start; i <= end; i += 1)
		Arr[i] = temp[i - start]


# Arr is an array of integer type
# start and end are the starting and ending index of current interval of Arr

def mergeSort(Arr, start, end) :

	if(start < end) :
		mid = (start + end) / 2
		mergeSort(Arr, start, mid)
		mergeSort(Arr, mid+1, end)
		merge(Arr, start, mid, end)
```

## Quick Sort Algorithm

> Time Complexity = O(NlogN)  
> Space Complexity = O(1)  
> Not stable

1. Pick an element, called a pivot, from the array.  
2. Partitioning: reorder the array so that all elements with values less than the pivot come before the pivot, while all elements with values greater than the pivot come after it (equal values can go either way). After this partitioning, the pivot is in its final position. This is called the partition operation.  
3. Recursively apply the above steps to the sub-array of elements with smaller values and separately to the sub-array of elements with greater values.

**Example**

12 18 15 21 19 30 4 17 -> 12 15 4 17 18 21 19 30 -> 4 15 12 and **17** and **18** **19** **21** **30** -> **4** **12** **15** and **17** and **18** **19** **21** **30**

### Pseudocode

```
quickSort(arr[], low, high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[pi] is now
           at right place */
        pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);  // Before pi
        quickSort(arr, pi + 1, high); // After pi
    }
}

```

### Implementation C++

```cpp
void swap(int *a, int *b)
{
	int temp; 
	temp = *a;
	*a = *b;
	*b = temp;
}
 
// Partitioning the array on the basis of values at high as pivot value.
int Partition(int a[], int low, int high)
{
	int pivot, index, i;
	index = low;
	pivot = high;
 
	// Getting index of the pivot.
	for(i=low; i < high; i++)
	{
		if(a[i] < a[pivot])
		{
			swap(&a[i], &a[index]);
			index++;
		}
	}
	// Swapping value at high and at the index obtained.
	swap(&a[pivot], &a[index]);
 
	return index;
}
 
// Random selection of pivot.
int RandomPivotPartition(int a[], int low, int high)
{
	int pvt, n, temp;
	n = rand();
	// Randomizing the pivot value in the given subpart of array.
	pvt = low + n%(high-low+1);
 
	// Swapping pivot value from high, so pivot value will be taken as a pivot while partitioning.
	swap(&a[high], &a[pvt]);
 
	return Partition(a, low, high);
}
 
int QuickSort(int a[], int low, int high)
{
	int pindex;
	if(low < high)
	{
		// Partitioning array using randomized pivot.
		pindex = RandomPivotPartition(a, low, high);
		// Recursively implementing QuickSort.
		QuickSort(a, low, pindex-1);
		QuickSort(a, pindex+1, high);
	}
	return 0;
}
```

### Implementation Python

```python
def partition(arr,low,high): 
	i = ( low-1 )		 # index of smaller element 
	pivot = arr[high]	 # pivot 

	for j in range(low , high): 

		# If current element is smaller than or 
		# equal to pivot 
		if arr[j] <= pivot: 
		
			# increment index of smaller element 
			i = i+1
			arr[i],arr[j] = arr[j],arr[i] 

	arr[i+1],arr[high] = arr[high],arr[i+1] 
	return ( i+1 ) 

# The main function that implements QuickSort 
# arr[] --> Array to be sorted, 
# low --> Starting index, 
# high --> Ending index 

# Function to do Quick sort 
def quickSort(arr,low,high): 
	if low < high: 

		# pi is partitioning index, arr[p] is now 
		# at right place 
		pi = partition(arr,low,high) 

		# Separately sort elements before 
		# partition and after partition 
		quickSort(arr, low, pi-1) 
		quickSort(arr, pi+1, high) 
```

## Selection Sort Algorithm

> Time Complexity = O(N^2) / O(N)  
> Space Complexity = O(1)  
> Not stable

1. Pick the minimum element from the unsorted subarray.  
2. Swap it with the leftmost element of the unsorted subarray.  
3. Now the leftmost element of unsorted subarray becomes a part (rightmost) of sorted subarray and will not be a part of unsorted subarray.

**Example**

5 2 6 7 2 1 0 3 -> **0** 2 6 7 2 1 5 3 -> **0** **1** 6 7 2 2 5 3 -> **0** **1** **2** 7 6 2 5 3 -> ...

### Pseudocode

```
\\ Time Complexity: O(n)
FindMinIndex(Arr[], start, end)    
        min_index = start    
        
        FOR i from (start + 1) to end:    
            IF Arr[i] < Arr[min_index]:    
                min_index = i    
            END of IF    
        END of FOR    
              
  Return min_index

\\ Time Complexity: (n-1) + (n-2) + ... + 1 = O(n^2)
SelectionSort(Arr[], arr_size):    
        FOR i from 1 to arr_size:    
            min_index = FindMinIndex(Arr, i, arr_size)    
        
            IF i != min_index:    
                swap(Arr[i], Arr[min_index])    
            END of IF    
        END of FOR
```

### Implementation C++

```cpp
int findMinIndex(vector<int> &A, int start) {  
    int min_index = start;  
  
    ++start;  
  
    while(start < (int)A.size()) {  
        if(A[start] < A[min_index])  
            min_index = start;  
  
        ++start;  
    }  
  
    return min_index;  
}  
  
void selectionSort(vector<int> &A) {  
    for(int i = 0; i < (int)A.size(); ++i) {  
        int min_index = findMinIndex(A, i);  
  
        if(i != min_index)  
            swap(A[i], A[min_index]);  
    }  
}  
```

### Implementation Python

```python
def findMinIndex(A, start):  
    min_index = start  
  
    start += 1  
  
    while start < len(A):  
        if A[start] < A[min_index]:  
            min_index = start  
  
        start += 1  
  
    return min_index  
  
def selectionSort(A):  
    i = 0  
  
    while i < len(A):  
        min_index = findMinIndex(A, i)  
  
        if i != min_index:  
            A[i], A[min_index] = A[min_index], A[i]  
          
        i += 1  
```

## Bubble Sort Algorithm

> Time Complexity = O(N^2) / O(N)  
> Space Complexity = O(1)  
> Stable

Repeatedly steps through the list, compares adjacent elements and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted.

### Pseudocode

```
bubbleSort( Arr[], totat_elements)
   
   for i = 0 to total_elements - 1 do:
      swapped = false
		
      for j = 0 to total_elements - i - 2 do:
      
         /* compare the adjacent elements */   
         if Arr[j] > Arr[j+1] then
            /* swap them */
            swap(Arr[j], Arr[j+1])		 
            swapped = true
         end if
         
      end for
      
      /*if no number was swapped that means 
      array is sorted now, break the loop.*/
      
      if(not swapped) then
         break
      end if
      
   end for
   
end
```

### Implementation C++

```cpp
void BubbleSort (vector<int> &arr, int n)
{
   for (int i = 0; i < n - 1; ++i)
   { 
      bool swapped = false;
      for (int j = 0; j < n - i - 1; ++j)
      {
         if (arr[j] > arr[j+1]) //check if adjacent element is
                      //not in order
         {
            swap(arr[j], arr[j + 1]);
            swapped = true;
         }
      }
      // Value at n-i-1 will be maximum of all the values below this index.

      if(!swapped)
         break;
   } 
} 
```

### Implementation Python

```python
def bubble_sort(arr):
    for i in range(len(arr) - 1):
        swapped = False
        for j in range(0, len(arr) - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        if not swapped:
            return
```
