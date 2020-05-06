---
layout: post
title:  Rust - codewars 문제풀이 1
date:   2020-05-03 10:07:06 +0900
categories: rust
---
[문제 링크](https://www.codewars.com/kata/5467e4d82edf8bbf40000155/train/rust)

### Instructions
Your task is to make a function that can take any non-negative integer as a argument and return it with its digits in descending order. Essentially, rearrange the digits to create the highest possible number.

### Examples:
Input: `21445` Output: `54421`

Input: `145263` Output: `654321`

Input: `123456789` Output: `987654321`


### Solution
```
fn descending_order(x: u64) -> u64 {
    unimplemented!()
}
```

### Sample Tests
```
#[test]
fn returns_expected() {
    assert_eq!(descending_order(0), 0);
    assert_eq!(descending_order(1), 1);
    assert_eq!(descending_order(15), 51);
    assert_eq!(descending_order(1021), 2110);
    assert_eq!(descending_order(123456789), 987654321);
    assert_eq!(descending_order(145263), 654321);
    assert_eq!(descending_order(1254859723), 9875543221);
}
```

### 문제 풀이
```
fn descending_order(x: u64) -> u64 {
    let mut vec: Vec<u64> = x.to_string().chars()
        .map(|c| c.to_digit(10).unwrap() as u64)
        .collect::<Vec<u64>>();

    vec.sort_by(|a, b| b.partial_cmp(a).unwrap());

    let result: u64 = vec.into_iter()
        .map(|i| i.to_string())
        .collect::<String>()
        .parse::<u64>().unwrap();

    result
}
```

1. 매개변수로 받은 숫자를 string으로 변환: to_string()
2. chars() 메서드로 Iterator를 받아서 
3. map() 메서드에 각 character를 다시 숫자로 변경
	- to_digit() 메서드 반환값이 u32이므로 `as u64` 로 형변환
4. collect(consuming adaptors)를 통해 다시 `Vec<64>`로 반환
5. sort_by로 내림차순 정렬 (이를위해 vec변수를 mut로 선언)
6. into_iter() 반복자를 통해 map으로 각 요소를 문자열로 변환
7. collect()를 통해 string으로 변환후 parse()로 최종 Integer result 변환
