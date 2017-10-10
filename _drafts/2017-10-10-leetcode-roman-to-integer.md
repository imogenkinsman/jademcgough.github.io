---
layout: post
title: LeetCode - Roman to Integer
date: 2017-10-10 09:58:00
---

Problem: [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

My first attempt is O(n), which I doubt I could beat in terms of complexity.

```ruby
def roman_to_int(s)
    answer = 0
    i_count = 0
    c_count = 0
    x_count = 0
    s.split('').each do |char|
        case char
        when 'M'
            answer += 1_000
            if c_count > 0
                answer -= c_count * 100
                c_count = 0
            end
        when 'D'
            answer += 500
            if c_count > 0
                answer -= c_count * 100
                c_count = 0
            end
        when 'C'
            c_count += 1
            if x_count > 0
                answer -= (x_count * 10)
                x_count = 0
            end
        when 'L'
            answer += 50
            if x_count > 0
                answer -= (x_count * 10)
                x_count = 0
            end
        when 'X'
            x_count += 1
            if i_count > 0
                answer -= i_count
                i_count = 0
            end
        when 'V'
            answer += 5
            if i_count > 0
                answer -= i_count
                i_count = 0
            end
        when 'I'
            i_count += 1
        end
    end
    answer + i_count + (c_count * 100) + (x_count * 10)
end
```

I hate how verbose that is, though. I can break this into smaller problems with recursion, which allows me to not have to track the individual counts.
