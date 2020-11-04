# Algorithms

## Array Shift, Unshift, Push, Pop, Splice

```javascript
Array.prototype.new_shift = function() {
    let value = this[0]
    for (let i = 0; i < this.length-1; i++) {
        this[i] = this[i+1]
    }
    this.length--
    return value
}
let numbers = [1,2,3]
numbers.new_shift()
console.log(numbers) // [ 2, 3 ]

Array.prototype.new_unshift = function(...values) {
    let val_length = values.length
    for (let i = this.length+val_length-1; i > 0; i--) {
        this[i] = this[i-val_length]
    }

    for (let i = 0; i < val_length; i++) {
        this[i] = values[i]
    }    
}
let numbers = [1,2,3]
numbers.new_unshift(4, 5)
console.log(numbers) // [ 4, 5, 1, 2, 3 ]

Array.prototype.new_push = function(...values) {
    for (let i = 0; i < values.length; i++) {
        this[this.length] = values[i]
    }    
}
let numbers = [1,2,3]
numbers.new_push(4, 5)
console.log(numbers) // [ 1, 2, 3, 4, 5 ]

Array.prototype.new_pop = function() {
    return this[this.length--]
}
let numbers = [1,2,3]
numbers.new_pop()
console.log(numbers) // [ 1, 2 ]

Array.prototype.new_splice = function(...values) {
    // TBD
}
```

## Hash Map

```javascript
function hashMap(queryType, query) {
    let hashMap = new Map()
    let getSum = 0
    for (let i = 0; i < queryType.length; i++) {
        switch (queryType[i]) {
            case "insert":
                hashMap.set(query[i][0],query[i][1])
                break
            case "get":
                if (hashMap.get(query[i][0]))
                    getSum += hashMap.get(query[i][0])
                break
            case "addToKey":
                let tempHashMap = new Map()
                for (entity of hashMap) {
                    tempHashMap.set(entity[0] + query[i][0], entity[1])
                    hashMap.delete(entity[0])                                     
                }              
                hashMap = tempHashMap  
                break
            case "addToValue": 
                for (entity of hashMap) {
                    hashMap.set(entity[0], entity[1] + query[i][0])
                }
        }        
    }
    return getSum    
}

let queryType = ['insert','insert','addToKey','addToKey','addToValue','get']
let query = [[-1, 5],[-2, 5],[1],[1],[1, 5],[1]]
let res = hashMap(queryType,query)
console.log(res)
```

## Sudoku

1) We have a pull of sudoku numbers.
2) Create three groups of pools.
3) Pull for 1 horizontal line.
4) Pull for 9 vertical lines.
5) Pull for 9 squares 3x3.
6) For each cell, check if sudoku numbers have already been used in the pools related to this cell? 
We check the horizontal pool, one vertical pool and one square 3x3 pool. 
If used, then remove this value from our pool of sudoku numbers.
7) If there are no numbers left in the pool of sudoku numbers, then we need to erase the entire line, clear the related pools and recreate the line.
8) If attempts to rearrange the numbers do not help (usually this is the 6th line), then we are trying to recreate the entire table.
9) If there are numbers in the pool of sudoku numbers, then we take a random number from these numbers and put it in the table.
10) We also add the selected used number to three pools: a horizontal pool, one vertical pool and one square pool.

```javascript
function Sudoku() {
    function Generator() {
        const numbers = [1,2,3,4,5,6,7,8,9] // 1)
        let tab = [], yl = [], sq = []

        for (let i = 0; i < numbers.length; i++) {
            tab[i] = []
            let xl = new Map() // 2), 3)
            let rebuild_iterator = 0
            
            if (!sq[Math.floor(i / 3)])
                sq[Math.floor(i / 3)] = []

            for (let j = 0; j < numbers.length; j++) {

                if (!yl[j])
                    yl[j] = new Map() // 2), 4)

                if (!sq[Math.floor(i / 3)][Math.floor(j / 3)])
                    sq[Math.floor(i / 3)][Math.floor(j / 3)] = new Map() // 2), 5)

                let sud_pull= [...numbers] // copy one dimention array, let sud_pull = digits - is a link

                for (let k = sud_pull.length - 1; k > -1; k--) { // 6)
                    if (xl.has(sud_pull[k])) {           
                        sud_pull.splice(k, 1)
                    } else if (yl[j].has(sud_pull[k])) {
                        sud_pull.splice(k, 1)
                    } else if (sq[Math.floor(i / 3)][Math.floor(j / 3)].has(sud_pull[k])) {
                        sud_pull.splice(k, 1)
                    }
                }                

                if (sud_pull.length == 0) { // 7) if our string is wrong, clean values and start xl from begin
                    if (rebuild_iterator++ == 30) // 8)
                        return []
                    
                    j-- // current j is not set yet so we move counter to previous
                    while (j > -1) {                
                            yl[j].delete(tab[i][j])
                            sq[Math.floor(i / 3)][Math.floor(j / 3)].delete(tab[i][j])
                            delete tab[i][j]
                        j--
                    }                
                    xl.clear()
                    continue
                } else {        
                    let digit = sud_pull[Math.floor(Math.random() * (sud_pull.length))] // 9)
                    tab[i][j] = digit // 9)
                    xl.set(digit,1) // 10)
                    yl[j].set(digit,1) // 10)
                    sq[Math.floor(i / 3)][Math.floor(j / 3)].set(digit,1) // 10)
                }
            }
        }
        return tab
    }

    let tab = []
    while (!tab.length) {
        tab = Generator()
    }
    return tab
}

const tab = Sudoku()
for (let entites of tab) {
    console.log(String(entites))
}
```
