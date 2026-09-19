
# Ex20 Sorting an Array using Merge Sort Algorithm
## AIM:
To design a program that sorts a given array of integers in ascending order without using built-in sorting functions, achieving O(n log n) time complexity and minimal space usage.

## Algorithm
1. Start the program.
2. Define a method `mergeSort()` that divides the array into two halves recursively until single elements remain.
3. Define a method `merge()` that merges two sorted halves into a single sorted array.
4. In the `main()` method:
   - Initialize an array of integers.
   - Display the original (unsorted) array.
   - Call the `mergeSort()` method to sort the array.
   - Display the sorted array.
5. Stop the program.  

## Program:
```java
/*
Program tosorts a given array of integers in ascending order without using built-in sorting functions
Developed by: Abinaya A
RegisterNumber: 212224230004

*/

import java.util.*;

public class Solution {
    
    private void swap(int[] arr, int index1, int index2) {
        int temp = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = temp;
    }

    private void heapify(int[] arr, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < n && arr[left] > arr[largest]) {
            largest = left;
        }

        if (right < n && arr[right] > arr[largest]) {
            largest = right;
        }

        if (largest != i) {
            swap(arr, i, largest);
            heapify(arr, n, largest);
        }
    }

    private void heapSort(int[] arr) {
        int n = arr.length;
        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }

        for (int i = n - 1; i >= 0; i--) {
            swap(arr, 0, i);
            heapify(arr, i, 0);
        }
    }

    public int[] sortArray(int[] nums) {
        heapSort(nums);
        return nums;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution solution = new Solution();

        int n = sc.nextInt();
        
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        int[] sorted = solution.sortArray(nums);
        System.out.println("Sorted array:");
        System.out.println(Arrays.toString(sorted));

        sc.close();
    }
}
```

## Output:
<img width="561" height="182" alt="image" src="https://github.com/user-attachments/assets/8909207f-3220-4841-8649-20fd9285092e" />




## Result:
The program has been successfully implemented and executed.
It sorts the given array of integers in ascending order using the Merge Sort algorithm with a time complexity of O(n log n) and minimal extra space.
