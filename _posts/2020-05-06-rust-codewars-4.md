---
layout: post
title:  Rust - codewars 문제풀이 4
date:   2020-05-06 10:07:06 +0900
categories: rust
---
[문제 링크](https://www.codewars.com/kata/5839edaa6754d6fec10000a2/train/rust)

### Instructions

#Find the missing letter

Write a method that takes an array of consecutive (increasing) letters as input and that returns the missing letter in the array.

You will always get an valid array. And it will be always exactly one letter be missing. The length of the array will always be at least 2.
The array will always contain letters in only one case.

### Examples
```
["a","b","c","d","f"] -> "e"
["O","Q","R","S"] -> "P"
```

(Use the English alphabet with 26 letters!)

Have fun coding it and please don't forget to vote and rank this kata! :-)

I have also created other katas. Take a look if you enjoyed this kata!

### Solution
```
fn find_missing_letter(chars: &[char]) -> char {

}
```

### Sample Tests
```
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn example_tests() {
        assert_eq!(find_missing_letter(&['a', 'b', 'c', 'd', 'f']), 'e');
        assert_eq!(find_missing_letter(&['O', 'Q', 'R', 'S']), 'P');
    }
}
```

### 문제 풀이
```
fn find_missing_letter(chars: &[char]) -> char {
    let ascii: Vec<u32> = chars.iter().map(|&c| c as u32).collect();

    for (idx, num) in ascii.iter().enumerate() {
        if idx != 0 && num-1 != ascii[idx-1] {
            return std::char::from_u32(num-1).unwrap()
        }
    }

    panic!();
}
```
- map을 이용하여 char vector를 u32 vector 로 변환
- 이전 인덱스 배열과 1차이가 아니라면 이전 요소를 다시 char로 변환해서 리턴
