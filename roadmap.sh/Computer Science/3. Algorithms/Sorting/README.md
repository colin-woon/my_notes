# Bubble Sort
**Complexity**: O(n²)
**Key Concept**: Basic idea of comparing and swapping elements. (Swaps)
```
void bubble_sort(int arr[], int size)
{
    int sorted_i = 0;
    while (sorted_i < size - 1) 
    {
        int unsorted_i = 0;
        while (unsorted_i < size - sorted_i - 1)
        {  // Compare adjacent elements
            if (arr[unsorted_i] > arr[unsorted_i + 1])
            {
                // Swap arr[unsorted_i] and arr[unsorted_i + 1]
                int temp = arr[unsorted_i];
                arr[unsorted_i] = arr[unsorted_i + 1];
                arr[unsorted_i + 1] = temp;
            }
            unsorted_i++;  // Move to the next pair
        }
        sorted_i++;  // After each pass, the largest element is in place
    }
}
```
# Selection Sort
**Complexity**: O(n²)
**Key Concept**: Finding the minimum (or maximum) element and placing it correctly. (Swaps)
```
void selection_sort(int arr[], int size)
{
    int sorted_i = 0;
    while (sorted_i < size - 1)
    {
        int min_i = sorted_i;  // Start with the current element as the minimum
        int unsorted_i = sorted_i + 1;
        
        while (unsorted_i < size)
        {  // Find the smallest element in the remaining array
            if (arr[unsorted_i] < arr[min_i])
                min_i = unsorted_i;  // Update min_i if a smaller element is found
            unsorted_i++;
        }
        // Swap the found minimum element with the first element
        int temp = arr[sorted_i];
        arr[sorted_i] = arr[min_i];
        arr[min_i] = temp;
        sorted_i++;  // Move to the next element in the unsorted part
    }
}
```
# Insertion Sort
**Complexity**: O(n²)
**Key Concept**: Inserting elements into their correct position by others to the right. (Shifts)
```
void insertion_sort(int arr[], int size) 
{
    int sorted_i = 1;  // Start with the second element (the first element is trivially sorted)
    
    while (sorted_i < size) 
    {
        int key = arr[sorted_i];
        int unsorted_i = sorted_i - 1;
  
        // Move elements of arr[0..sorted_i-1] that are greater than key to one position ahead
        while (unsorted_i >= 0 && arr[unsorted_i] > key) 
        {
            arr[unsorted_i + 1] = arr[unsorted_i];  // Shift element to the right
            unsorted_i--;
        }
        arr[unsorted_i + 1] = key;  // Insert the key into its correct position
        sorted_i++;  // Move to the next element
    }
}
```
# Merge Sort
**Complexity**: O(n log n)
**Key Concept**: Dividing the array into subarrays, sorting them, and then merging them back together.
# Quick Sort
**Complexity**: O(n log n) on average, but O(n²) in the worst case.
**Key Concept**: Partitioning and recursive sorting.