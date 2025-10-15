"# CSCI6212-README.md"
# CSCI6212 Project2

## Finding Maximum in a Circularly Shifted Array
## Overview

This project implements and analyzes an O(log n) algorithm to find the maximum element in a sorted array that has been circularly (rotated) shifted.
The algorithm is a variation of binary search, which efficiently locates the pivot point — the position where the order “wraps around.” The element just before this pivot is the maximum value in the array.

## Algorithm Description
Given a sorted array that has been rotated to the right by an unknown number of positions, such as:
[35, 42, 5, 15, 27, 29]

The goal is to return the maximum element (42).
A naive approach would scan through the entire array in O(n) time.
Instead, this algorithm uses binary search logic to reduce the search space by half each iteration, achieving O(log n) time.
Steps
Set low = 0, high = n - 1.
Compute mid = (low + high) // 2.
If A[mid] > A[mid + 1], return A[mid] (maximum found).
Else if the left half is sorted (A[low] <= A[mid]), search in the right half (low = mid + 1).
Otherwise, search in the left half (high = mid - 1).
The loop continues until the pivot (maximum) is found.

## Code 
```python
def find_largest_element(arr):
    """
    Finds the largest element in a circularly shifted sorted array.

    Args:
        arr: A list of integers.

    Returns:
        The largest integer in the array.
    """
    n = len(arr)
    # Handle the case of a single-element array
    if n == 1:
        return arr[0]

    low = 0
    high = n - 1

    while low <= high:
        mid = low + (high - low) // 2

        # If the middle element is greater than its next element, it is the largest.
        # Use modulo for the next element to handle wrap-around.
        if arr[mid] > arr[(mid + 1) % n]:
            return arr[mid]

        # If the array is not rotated, the largest is the last element
        if arr[low] < arr[high]:
            return arr[high]

        # If the left half is sorted, the largest element must be in the right half.
        if arr[low] <= arr[mid]:
            low = mid + 1
        # Otherwise, the largest element is in the left half.
        else:
            high = mid
    
    return -1 # Should not be reached in a valid array

# Example usage
arr1 = [35, 42, 5, 15, 27, 29]
print(f"The largest element in {arr1} is: {find_largest_element(arr1)}")

arr2 = [27, 29, 35, 42, 5, 15]
print(f"The largest element in {arr2} is: {find_largest_element(arr2)}")

arr3 = [5, 15, 27, 29, 35, 42]
print(f"The largest element in {arr3} is: {find_largest_element(arr3)}")

arr4 = [42, 5, 15, 27, 29, 35]
print(f"The largest element in {arr4} is: {find_largest_element(arr4)}")

