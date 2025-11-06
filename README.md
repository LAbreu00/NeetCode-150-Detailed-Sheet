# NeetCode-150-Detailed-Sheet

Neetcode 150 Roadmap learnings


## Arrays and Hashing

### Top K Frequent Elements

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
