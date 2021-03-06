## Partner A: White Boarding

## Sorts

### Binary Search

Write a method that binary searches an array for a target and returns its
index if found. Assume a sorted array.

NB: YOU MUST WRITE THIS RECURSIVELY (searching half of the array every time).
We will not give you points if you visit every element in the array every time
you search.

For example, given the array [1, 2, 3, 4], you should NOT be checking
1 first, then 2, then 3, then 4.

def bsearch(array, target)
    return nil if array.empty?

    mid_idx = array.length / 2

    case target <=> array[mid_idx]
        when -1
            bsearch(array.take(mid_idx), target)
        when 0
            mid_idx
        when 1
            right_bsearch = bsearch(array.drop(mid_idx + 1), target)
            right_bsearch.nil? ? nil : right_bsearch + 1 + mid_idx
        end
    end
end


## Monkey Patching

### my_each

Write a method that calls a passed block for each element of the array

### dups

Write an array method that returns a hash where the keys are any element
that appears in the array more than once, and the values are sorted arrays
of indices for those elements.

class Array

    def duped_indices

        element_indices_hash = Hash.new { |hash, k| hash[k] = [] }

        self.each_with_index do |ele, idx|
            element_indices_hash[ele] << idx
        end

        elements_indices_hash.select { |k, v| v.length > 1 }
    end




    def my_each(&prc)

        i = 0
        while i < self.length
            prc.call(self[i])

            i += 1
        end

        self
    end

end


## Recursion

### Factorials

Write a method that recursively finds the first `n` factorial numbers
and returns them. N! is the product of the numbers 1 to N.
Be aware that the first factorial number is 0!, which is defined
to equal 1. The 2nd factorial is 1!, the 3rd factorial is 2!, etc.

def factorial_array(n)
    return [1] if n == 1

    facs_array = factorial_array(n - 1)
    facs_array << (n - 1) * facs_array[-1]

    facs_array

end


### Digital Root

Write a method, `digital_root(num)`. It should Sum the digits of a positive
integer. If it is greater than 10, sum the digits of the resulting number.
Keep repeating until there is only one digit in the result, called the
"digital root". **Do not use string conversion within your method.**

You may wish to use a helper function, `digital_root_step(num)` which performs one step of the process.

def digital_root(num)
    return num if num < 10

    output = digtial_root(num / 10) + (num % 10)

    output < 10 ? output : digital_root(output)
end



## Regular Methods

### Largest Prime Factor

Write a method that returns the largest prime factor of a number. We recommend writing a `is_prime?` helper method.


def largest_prime_factor(n)

    (n..2).each do |factor|
        return factor if is_prime?(factor)
    end

    nil 

end


def is_prime?(num)
    return false if num < 2

    (2...num).each do |factor|
        return false if num % factor
    end

    true

end


### Jumble Sort

Jumble sort takes a string and an alphabet. It returns a copy of the string
with the letters re-ordered according to their positions in the alphabet. If
no alphabet is passed in, it defaults to normal alphabetical order (a-z).

Example:

```rb
jumble_sort("hello") => "ehllo"
jumble_sort("hello", ['o', 'l', 'h', 'e']) => 'ollhe'

