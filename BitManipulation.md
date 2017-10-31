# Bit Manipulation

## Binary (base 2)
------------------

- it is only 0 and 1 so how do we keep counting?
 ```
  Base 10 
  digits: 0-9
  counting : increment digits in one place until you can't anymore, then add
  a digit to the next place.

  Example: 20 10 00
                 01
                 02
                 03....09

  Base 2
  digits: 0,1
  counting: increment digits in one place until you can't anymore, then add a 
  digit to hte next place

  Example: 
    0   10  100 1000   1100
    1   11  101 1001   1101
            110 1010   1110
            111 1011   1111
               
 ```


## Converting into Binary
- Need to brush up on powers of two

    - Lets say you want to convert 27 to binary, then you need to ask yourself
which power of 2 can I reach without going over the number that I want to convert?

    - In based 10, we have units, tens, hundreds, thousands, and so on. In binary, 
we our places come from the power of two, ones, twos, fours, eights, sixteens.


- Memorized the placement of 2
    - 2^0 = 1
    - 2^1 = 2
    - 2^2 = 4
    - 2^3 = 8
    - 2^4 = 16
    - 2^5 = 32
    - 2^6 = 64
    - 2^7 = 128
    - 2^8 = 256
    - 2^9 = 512
    - 2^10 = 1024

- Number in base 10 will always end in 0 when they're converted to binary.
- Even number are divisible by two which you will never have an extra
remainder of 1 when you breaking down your number into powers of two.

## Converting out of binary
===========================
- If we want to convert from base 10 to binary you can see each position based
on the power of 2, so you times 2^(position) to 1 or 0 based on what position
and keep adding down.
- If there is a 1 in the place, multiply the power of two for that 
place by 1 ( and then keep doing that until you've gone through all the places!)


- Bit: binary digit 
- 8 bit = 1 byte ( a unit of computer memory) 
    - Single byte can represent 256 different combinations

- Different computer can process different number of bits at a time. An 8 bit machine
for example, breaks up and processes 8 bits at a time.
- 16 bit machine would break up the processes to 16 bits at a time
- The number of bits that are processed at a time are known as a computer word,
so we can think of bits as the "letters" that make up a computer word.
- there is 32 and 64 means your computer processes binary strings that are 
32 or 64 digits long.
- 1 character -> 8 bits -> 1 byte


## Bit Manipulation in CTCL
===========================
- if you xor a bit with its negate value, it will be 1, so if a^(~a) it will be all 1's sequence
- an operation like x & (~0<<n) means to clear the rightmost n bits of x. The value of
~0 is a bunch of 1 so by simply shifting it to the left n it will cause all 1s followed by
n zeros. By doing an AND with x, we clear the rightmost bit of x.

```
    Big Fact and tricks:
    (1s and 0s is a sequence of 1s and 0s)
    x ^ 0s = x // think of as 1 ^ 0 = 1 and 0 ^ 0 = 0(since it is the same so it will be false)
    x ^ 1s = 1 // think of as 1 ^ 1 = 0 and 0 ^ 1 = 1 the 1 and 0 on the left side is the x
    x ^ x = 0
    x & 0s = 0
    x & 1s = x
    x & x = x
    x | 0s = x
    x | 1s = 1
    x | x = x



    Get Bit: (performing AND)
    boolean getBit(int num, int i){
        return (num & (1 << i)) != 0;
    }

    Set bit: (performing OR, by performing OR so all 0s and only the one 
    in the num will change to 1 and that number will change)
    int setBit(int num, int i){
        return num | (1<<i);
    }

    clear bit: ( first we perform the 1 by become all 0s and only 1 in the i plae
    then reversing it, so all 1s only 0 in i place and AND that with the num it will
    clear that specific bit)
    int clearBit(int num, int i){
        int mask = ~(1<<i);
        return num & ~mask; 
    }

    To clear most significant( most right) to i(inclusive)
    int clearBitsthroughI(int num, int i){
        int mask = 1 << (i-1); // all things before i will get reserve because it become 1
              reutrn num & mask;
    }


    To clear i (inclusive) to 0 bit
    int clearBitsIthrough0(int num, int i){
        int mask = ~((1 << (i+1))-1); // this will set all 1 until i because we negate it
        return num & mask;
    }


    Update bit: We combine both merge set and clear bit. First clear the bit at the position i,
    then afterward set (OR) the bit on the i position on v to update the bit
    int updateBit(int num, int i, int v){
        int mask = ~(1<<i);
        return (num & mask) | (v << i);



```


- Some helpful uitility snippet:
    * Test kth bit is set: num & (1<<k)!=0
    * num |= (1<<k)
    * Turn off kth bit: num &= ~(1<<k)
    * Toggle the kth bit: num ^= (1<<k)
    * To check if a number is a power of 2: num & num-1 == 0

### ^ tricks
- Use ^ to remove even exactly same numbers and save the odd, or save the distinct bits
and remove the same.
- With array XOR of any number with itself gives us 0, XOR of any number with 0 gives us number 
itself.

- Missing Number: 
    - Given an array containing n distinct numbers taken from 0,1,2, ..., n, find the 
    one that is missing from the array. For example, Given nums =[0,1,3] return 2.
    ```
    int missingNumber(int [] nums){
        int ret = 0;
        for(int i = 0 ; i<nums.size(); i++){
            ret^=i; 
            ret ^= nums[i];
        }
        return ret ^= nums.size();
    }
    ```

### | tricks
- Keep as many 1 - bits as possible


