### Down Dog Application Question
###### Applicant: Douglas Alan Webster
###### Email: douglas.alan.webster@gmail.com
###### LinkedIn: https://www.linkedin.com/in/dougweb/

#### Question: What is the sum of all the multiples of 4 or 7 under 2500?

#### Solution: 1,115,181

#### Explanation:

- There are *624.75* (i.e., *2499/4*) numbers in the interval `[1..2500)` which are divisible by *4*
- We can then scale each of numbers in the interval `[1..624]` by *k*, where *k* is the divisor (i.e., *4*)
- This will map each number in the interval `[1..624]` to a unique multiple of *4* in the interval `[1..2500)`
- We now have the following summation: `4(1) + 4(2) + 4(3) + ... + 4(623) + 4(624)`
- If we factor out the *4* we are left with `4(1 + 2 + 3 + ... + 623 + 624)`
- Since, the sum of the numbers in an interval `[1..n]` is *n((n+1)/2)*
- We can compute the sum of all the numbers divisible by *4* in the interval `[1..2500)` with the following formula: *k(n((n+1)/2))*
- Where *k* is the divisor and *n* is `floor(upperBound/divisor)` 

--

- The same logic can be used to compute the sum of all the numbers divisible by *7* in the interval `[1..2500)`

--

- The last thing we have to watch out for is the overlap between multiples of *4* and *7*
- For example, *28* would be double counted if we don't account for the overlap
- Therefore, we must subtract out all of the overlapping multiples so they are only counted once
- To do this we follow the same logic as before but apply it to the least common multiple
- In this case the least common multiple of *4* and *7* is *28*

- Taking all of this into consideration we can now compute the sum of all the multiples of *4* or *7* under *2500*
  
*Let,* 
- *k_1 = 4*      (divisor)
- *n_1 = 624*		(floor(2499/4))
- *k_2 = 7*		(divisor)
- *n_2 = 357* 	(floor(2499/7))
- *k_{common} = 28*	(least common multiple of 4 and 7)
- *n_{common} = 89*	(floor(2499/28))
        	
We must now calculate: 
`Sum of #'s div by 4` + `Sum of #'s div by 7` - `Sum of #'s div by 4 and 7`

*= k_1(n_1((n_1+1)/2)) + k_2(n_2((n_2+1)/2)) - k_{common}(n_{common}((n_{common}+1)/2))*

    
= *4(624((624+1)/2)) + 7(357((357+1)/2)) - 28(89((89+1)/2))*
= *780,000 + 447,321 - 112,140*
= *1,115,181*

#### Coded Solutions:
Naive Solutions:
```Kotlin
var sum: Int = 0
for(i in 1..2499) {
    if(i % 4 == 0 || i % 7 == 0) {
        sum += i
    }
}
```

```Kotlin
(1..2499).filter { it % 4 == 0 || it % 7 == 0 }.reduce { sum, element -> sum + element }
```

Solution Using Logic From Explanation:
```Kotlin
val numbersDivisibleBy4: Int = 2499/4
val numbersDivisibleBy7: Int = 2499/7
val numbersDivisibleBy4And7: Int = 2499/28
    
val sumOfNumbersDivisibleBy4: Int = 4 * ((numbersDivisibleBy4 * (numbersDivisibleBy4 + 1)) / 2)
val sumOfNumbersDivisibleBy7: Int = 7 * ((numbersDivisibleBy7 * (numbersDivisibleBy7 + 1)) / 2)
val sumOfNumbersDivisibleBy4And7: Int = 28 * ((numbersDivisibleBy4And7 * (numbersDivisibleBy4And7 + 1)) / 2)
    
val sumOfNumbersDivisibleBy4Or7 = sumOfNumbersDivisibleBy4 + sumOfNumbersDivisibleBy7 - sumOfNumbersDivisibleBy4And7 
```

*Using this logic we can expand further to support any range and multiples given to us.*
