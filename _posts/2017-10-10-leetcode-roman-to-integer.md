---
layout: post
title: LeetCode - Roman to Integer
date: 2017-10-10 09:58:00
---

Problem: [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

My first attempt is O(n) (runs in 182ms), which I doubt I could beat in terms of complexity.

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

```ruby
def roman_to_int(s)
    chars = s.split('').reverse
    get_total(char_value(chars.first), chars.drop(1))
end

def get_total(sum, chars)
    return sum if chars.length == 0

    val = char_value(chars.first)
    if val <= (sum / 5)
       get_total(sum - val, chars.drop(1))
    else
       get_total(sum + val, chars.drop(1))
    end
end

def char_value(char)
    case char
    when 'M' then 1000
    when 'D' then 500
    when 'C' then 100
    when 'L' then 50
    when 'X' then 10
    when 'V' then 5
    when 'I' then 1
    end
end
```

This is also O(n), and ran in the same amount of time. It's a bit cleaner, but perhaps more clever as well.

Something I didn't pick up on initially (guess I haven't used roman numerals in a while) is that there's only ever going to be one "decrementer" character (i.e. 9 is IX but 8 is VIII). That lets us do a single pass (other than the split/map) and just check the next character.

```ruby
def roman_to_int(s)
    total = 0
    values = s.split('').map{ |v| char_value(v) }
    values.each_with_index do |val, i|
        if values[i + 1] && val < values[i + 1]
            total -= val
        else
            total += val
        end
    end
    total
end

def char_value(char)
    case char
    when 'M' then 1000
    when 'D' then 500
    when 'C' then 100
    when 'L' then 50
    when 'X' then 10
    when 'V' then 5
    when 'I' then 1
    end
end
```

Same runtime, a bit less hacky and more readable.
