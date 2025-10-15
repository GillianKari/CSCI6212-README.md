# CSCI6212-README.md
CSCI6212 Project2

CSCI6212-Project2
Finding Maximum in a Circularly Shifted Array
Overview
This project implements and analyzes an O(log n) algorithm to find the maximum element in a sorted array that has been circularly (rotated) shifted.
The algorithm is a variation of binary search, which efficiently locates the pivot point — the position where the order “wraps around.” The element just before this pivot is the maximum value in the array.

Algorithm Description
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

import random, time

def find_max_in_rotated_array(A):
    """Return the maximum element in a rotated sorted array using O(log n) search."""
    low, high = 0, len(A) - 1

    # If array is not rotated
    if A[low] < A[high]:
        return A[high]

    while low <= high:
        mid = (low + high) // 2

        # Pivot condition
        if mid < len(A) - 1 and A[mid] > A[mid + 1]:
            return A[mid]
        elif A[mid] >= A[low]:
            low = mid + 1
        else:
            high = mid - 1

# --- Runtime Simulation ---
def simulate_runtime(n):
    """Generate a rotated sorted array of size n and measure search time."""
    arr = sorted(random.sample(range(1, n*5), n))
    # Random rotation
    k = random.randint(0, n - 1)
    rotated = arr[k:] + arr[:k]

    start = time.time()
    _ = find_max_in_rotated_array(rotated)
    end = time.time()
    return end - start

# Test for multiple input sizes
n_values = [10**3, 5*10**3, 10**4, 5*10**4, 10**5, 5*10**5]
for n in n_values:
    t = simulate_runtime(n)
    print(f"n={n:6d}, time={t:.8f}s, normalized={t / (math.log2(n)):.6e}")
