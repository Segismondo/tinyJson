# Expected output

countEquals : 35308[µs] -> 45440 elements found
filterEquals : 70571[µs] -> 9650 elements left
getMax : 11[µs] -> MAX: 1179.86
filterEquals : 71066[µs] -> 34390 elements left
filterEquals : 213[µs] -> 10 elements left
getMin : 0[µs] -> MIN: 31.4
filterEquals : 67373[µs] -> 3620 elements left
getSum : 3[µs] -> SUM: 2707874300

# Output with iterators

countEquals : 36104[µs] -> 45440 elements found
filterEquals : 71853[µs] -> 9650 elements left
getMax : 11[µs] -> MAX: 1179.86
filterEquals : 71684[µs] -> 34390 elements left
filterEquals : 211[µs] -> 10 elements left
getMin : 0[µs] -> MIN: 31.4
filterEquals : 66931[µs] -> 3620 elements left
getSum : 3[µs] -> SUM: 2707874300

## Performance

Tried to replace the loops with iterators (code done in approachIterator branch). The intention with that approach (in case the performance would improve) was to use a find_if and lambdas to make it work faster because they are more "cache friendly". After several executions it showed that this approach did not improve the performance significantly so it was discarded.

Another discarded option was to create a vector of vectors (with fixed size) to avoid cache miss and I thought it could help with cache locality. 

On the .cpp file, there is a casting from double to float which could lead to a loss of precision (I understand that comparing two doubles can be complicated but a good approach could be to make the subtraction of both doubles and check if the result is lower than Epsilon).

Besides, while using the "Row e" inside the try/catch block (.cpp) it is just creating this to hold a temporary data an make a push_back to the vector so it is unnecessary. I have used the tool Godbolt to check that there is a loss of perfomance here. Related to this point, I would like to mention that a really good idea it would be to know the size of the document. This way the size of the vector could be "reserved" in advance and would provoke a boost in perfomance. By the way it is currently being done, everytime it runs out of space in the vector and we wanna make a push_back again, we have to reallocate the memory, that means that we have to move all the elements again which is a really bad idea. So, by knowing the size in advance we could avoid the reallocation of the memory which usually provokes poorer perfomance.

Connected with the question I made to Raul via e-mail; I think the best choice for this would be to use a hash table (unordered_map for example) which would improve the implementation. The problem here is that we do not know have anything unique that could help me following this approach.

At last, I wanted to try to use threads on the functions (e.g countEquals), to have more than one thread doing the calculations and then join the results and test the impact on the perfomance. Unfortunately I was already above the 3 hours of work and I did not have time to apply it. 

## Scalability 

Replace one of the structs (Storage) with a class (modern C++) since it is a bit more complex and it has few things inside. This would mean that in the future it could be easier to work with it on changes (and also on maintainability below). Also I wanted to point to the use of the keyword "public" at the beginning of the struct Row. By default, visibility in structs is public, so it is not need it to write it (by contrast with classes that use private as default)

## Maintainability

Related to maintainability I have few things to mention. 

The first one is the usage of a proper naming convention. If in the future (or even in the present) someone would read e.foo(), the name "e" does not mean anything, you cannot extract any information from that variable. It is always good to follow this and to avoid "magic numbers" and "magic variables" that are not good for anyone (Clean code).

The second one, typedefs. As Scott Meyers says: prefer alias declarations to typedefs. Since C++11 we have the option to use alias "using x = ..." One of the main reasons to use this is because alias declarations may be templatized so it can be useful for the future to stick to alias.

Usage of noexcept function whenever possible.

## Features

A nice feature for the project (which would improve the performance) it is the usage of a third party library that I have already used in the past. The library is called semi_index (github.com/ot/semi_index). The goal of this is to speed-up the processing of big (and multiple) JSON files by creating a semi_index file. It generates an auxiliary file that holds the structure of the JSON files, so when you want only a subset of the values in the document, the parser can be pointed to the positions of this values so you would not have to parse the whole document.

# Final thoughts

It was a really open task (and with a limit of 3 hours) so I focused into trying to explain different approaches that I could take to show my way of thinking based on the code that is already done, rather than just following one unique and long approach and applying it into the code which could take couple of hours without any positive results. 

Since the beginning I decided to work into the idea of improving the performance because in this type of code I think is a key area. However, as you could see above, I also mentioned other things that could be fixed/improved (in different areas) because those things were already present on the code and I wanted to express that perfomance is important, but small details are important too and it can make a difference.

