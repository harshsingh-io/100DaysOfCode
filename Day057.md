# Day 57

Date Completed: May 12, 2023 1:00 AM

Date Started: May 11, 2023 11:40 PM

Difficulty: ⭐⭐

Done: Yes

Languages: Java

Related to Progress (Days): 57%

Topic: Container With Most Water VS Trapping Rain Water Problem., Container With Most Water(2-Pointer Approach)

## What I Learned Today

- Difference In Container With Most Water and Trapping Rain Water Problem.
- Container With Most Water(2-Pointer Approach)

### Quick Links

---

[**Documentation**](https://www.geeksforgeeks.org/container-with-most-water/)

[**YouTube Video**](https://youtu.be/ZHQg07n_tbg)

## Key Concepts

**Problem Description:**
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute the area of water that it is able to trap after raining.

**Approach:**
The approach used in this problem is the Two Pointer Approach, where we take two pointers, one pointing to the left-most element of the array and the other pointing to the right-most element of the array. We then calculate the water area using these two pointers and update the maximum water area found so far. We then move the pointer that is pointing to the lesser height to the next position, since the amount of water that can be trapped is limited by the height of the shorter pointer.

**Pseudocode:**

```
storeWater2Pointer(height):
    maxWater = 0
    lp = 0
    rp = height.size() - 1
    while lp < rp:
        width = rp - lp
        ht = min(height[lp], height[rp])
        currWater = ht * width
        maxWater = max(maxWater, currWater)
        if height[lp] < height[rp]:
            lp++
        else:
            rp--
    return maxWater
```

**Code Explanation:**

1. The function **`storeWater2Pointer`** takes an ArrayList of heights as input and returns the maximum water area that can be trapped.
2. **`maxWater`** is initialized to 0, **`lp`** is initialized to 0, and **`rp`** is initialized to the right-most index of the ArrayList.
3. A while loop is executed until **`lp`** is less than **`rp`**.
4. The width of the container is calculated by taking the difference between the indices of the two pointers.
5. The height of the container is calculated as the minimum of the heights at the two pointers.
6. The current water area is calculated as the product of the width and height of the container.
7. The maximum water area found so far is updated.
8. The pointer with the shorter height is moved to the next position.
9. The final maximum water area is returned.

**Key Points:**

- The 2-pointer approach reduces time complexity to O(n) from O(n^2) in the Brute Force approach.
- The width of the container is calculated as the difference between the indices of the two pointers.
- The height of the container is calculated as the minimum of the heights at the two pointers.
- The pointer with the shorter height is moved to the next position, since the amount of water that can be trapped is limited by the height of the shorter pointer.
- The approach involves using two pointers, one at the start and the other at the end of the array.
- Repeat until the two pointers meet.

**Dry Run:**
Let's dry run the given code on the provided input:

**`height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`**

- **`maxWater`** is initialized to 0, **`lp`** to 0, and **`rp`** to 8.
- Since **`lp`** is less than **`rp`**, the following steps are executed:
    - The width is calculated as **`8-0=8`**.
    - The height of the container is calculated as the minimum of the heights at the two pointers: **`min(height[0], height[8])=min(1, 7)=1`**.
    - The current water area is calculated as **`1*8=8`**.
    - Since **`8`** is greater than **`0`**, **`maxWater`** is updated to **`8`**.
    - Since **`height[0]`** is less than **`height[8]`**, **`lp`** is incremented to **`1`**.
- The above steps are repeated until **`lp`** becomes equal to **`rp`**.
- The final **`maxWater`** is returned as answer

**Dry run on given values:** The final output will be 49.

- height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
- lp = 0, rp = 8
- width = 8 - 0 = 8
- ht = min(height[0], height[8]) = 1
- currWater = 8 * 1 = 8
- maxWater = 8
- lp = 1, rp = 8
- width = 8 - 1 = 7
- ht = min(height[1], height[8]) = 7
- currWater = 7 * 7 = 49
- maxWater = 49
- lp = 1, rp = 7
- width = 7 - 1 = 6
- ht = min(height[1], height[7]) = 3
- currWater = 6 * 3 = 18
- maxWater = 49
- lp = 2, rp = 7
- width = 7 - 2 = 5
- ht = min(height[2], height[7]) = 3
- currWater = 5 * 3 = 15
- maxWater = 49
- lp = 2, rp = 6
- width = 6 - 2 = 4
- ht = min(height[2], height[6]) = 6
- currWater = 4 * 6 = 24
- maxWater = 49
- lp = 2, rp = 5
- width = 5 - 2 = 3
- ht = min(height[2], height[5]) = 4
- currWater = 3 * 4 = 12
- maxWater = 49
- lp = 2, rp = 4
- width = 4 - 2 = 2
- ht = min(height[2], height[4]) = 5
- currWater = 2 * 5 = 10
- maxWater = 49
- lp = 3, rp = 4
- width = 4 - 3 = 1
- ht = min(height[3], height[4]) = 2
- currWater = 1 * 2 = 2
- maxWater = 49

### Difference In Container with most water and Trapping rain water problem.

Both "Container With Most Water" and "Trapping Rain Water" problems involve calculating the amount of water that can be trapped between bars of a given height. However, the main difference between the two problems lies in the way the bars are arranged.

In the "Container With Most Water" problem, we are given an array of n non-negative integers representing the height of bars placed horizontally. We are to find two bars that can hold the most amount of water between them. In other words, we are to find the maximum area of a rectangle that can be formed by two bars.

In the "Trapping Rain Water" problem, we are given an array of n non-negative integers representing the height of bars placed vertically. The bars can be imagined as buildings and the space between them as streets. The task is to calculate the amount of water that can be trapped between the buildings after it rains.

While both problems involve calculating the amount of water that can be trapped between bars, the way the bars are arranged is different, leading to different approaches to solving the problems.

## Code Snippets

```java
public static int storeWater2Pointer(ArrayList<Integer> height){
        int maxWater =0;
        int lp=0;
        int rp = height.size()-1;
        while (lp<rp){
            //calculate water area
            int width = rp-lp;
            int ht = Math.min(height.get(lp), height.get(rp));
            int currWater = ht*width;
            maxWater = Math.max(maxWater, currWater);
            // update pointer
            if (height.get(lp)<height.get(rp)){
                lp++;
            }else {
                rp--;
            }
        }
        return maxWater;
    }
```

## Challenges Experienced

Dry Run is necessary for this problem.

## Resources Used

Alpha, Youtube, ChatGPT, GeeksForGeeks
