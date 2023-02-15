# Expected output

countEquals : 35308[µs] -> 45440 elements found
filterEquals : 70571[µs] -> 9650 elements left
getMax : 11[µs] -> MAX: 1179.86
filterEquals : 71066[µs] -> 34390 elements left
filterEquals : 213[µs] -> 10 elements left
getMin : 0[µs] -> MIN: 31.4
filterEquals : 67373[µs] -> 3620 elements left
getSum : 3[µs] -> SUM: 2707874300

## Performance
Tried to replace the loops with iterators. The intention with that approach (in case the performance would improve) was to use find_if and lambdas to make it work faster. After several executions it showed that this approach did not improve the performance significantly so it was discarded.

## Scalability 
Utilizar clases en lugar de structs para poder tener jerarquias y tener un codigo escalable (y mantenible tambien)

## Maintainability


## API refactors


## Features

