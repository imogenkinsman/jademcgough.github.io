Problem: [Two Sum](https://discuss.leetcode.com/category/9/two-sum)

I tackled this in a few ways. There's the standard O(n^2) solution, which takes a blazing 5.5 seconds to complete:

```ruby
def two_sum(nums, target)
    (0...nums.length).each do |i|
        start = i + 1
        (start...nums.length).each do |j|
            if nums[i] + nums[j] == target then return [i, j] end
        end
    end
end
```

Then, I tried using sorting (nlogn, with some additional n iterations), which was kind of a pain because I had to store the original array indices. This dropped the runtime by nearly two powers of ten (to 85ms):

```ruby
def two_sum(nums, target)
    i = 0
    j = nums.length - 1
    
    nums = nums.each_with_index.map{ |x,i| [x, i]}.sort
    while true do
        total = nums[i].first + nums[j].first
        if total == target
            return [nums[i].last, nums[j].last]
        elsif total > target
            j -= 1
        else
            i += 1
        end
    end
end
```

Lastly, I tried using a hash lookup (dropping the algorithm down to O(n)), which gave me a small but noticeable improvement to 69ms:

```ruby
def two_sum(nums, target)
    indices = {}
    nums.each_with_index do |x,i|
        indices[x] = i
    end
    
    answer = []
    nums.each_with_index do |x,i|
        j = indices[target - x]
        if  j && j != i
            answer = [i, j]
            break
        end
    end
    return answer
end
```
