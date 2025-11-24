# NeetCode-150-Detailed-Sheet

Neetcode 150 Roadmap learnings


## Arrays and Hashing

### [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)

#### Bucket Sort

Create buckets based on the number of elements, the move elements between the buckets based on frequency.

```js
topKFrequent(nums, k) {
        const count = {};
        // frequency counter is the length of nums, filled with other empty arrays
        // Ex: nums.length = 7, freq = [[],[],[],[],[],[],[]]
        const freq = Array.from({ length: nums.length + 1 }, () => []);

        // genereates regular frequency counter in obj
        for (const n of nums) {
            count[n] = (count[n] || 0) + 1;
        }

        // pushes numbers (keys) from count based on their frequency (values)
        for (const n in count) {
            freq[count[n]].push(parseInt(n));
            //    ^freq of num      ^actual num 
        }

        const res = [];
        // goes through freq backwards (highest frequency at the end)
        for (let i = freq.length - 1; i > 0; i--) {
            // pushed the numbers in each bucket
            for (const n of freq[i]) {
                res.push(n);
                // stops when amount push is equal to k 
                if (res.length === k) {
                    return res;
                }
            }
        }
    }
```

### [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

#### Hash Set

Uses set and to organize numbers and make look up quick

```js
longestConsecutive(nums) {

    // create set with the numbers in nums
    const numSet = new Set(nums);
    // max streak saved
    let longest = 0;

    for (let num of numSet) {
        // if a number smaller then the current one exsists, skip the number
        if (!numSet.has(num - 1)) {
            let length = 1;
            // continue the streak if the next number exsists
            while (numSet.has(num + length)) {
                length++;
            }
            // check between the current streak and max and r
            longest = Math.max(longest, length);
        }
    }
    return longest;
}
```
