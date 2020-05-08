---
layout: post
title:  Rust - codewars 문제풀이 6
date:   2020-05-08 09:05:00 +0900
categories: rust
---
[문제 링크](https://www.codewars.com/kata/523f5d21c841566fde000009/train/rust)

### Instructions
Your goal in this kata is to implement a difference function, which subtracts one list from another and returns the result.

It should remove all values from list `a`, which are present in list `b`.

### Examples
```
array_diff(vec![1,2], vec![1]) == vec![2]
```

If a value is present in `b`, all of its occurrences must be removed from the other:

```
array_diff(vec![1,2,2,2,3], vec![2]) == vec![1,3]
```

### Solution
```
fn array_diff<T: PartialEq>(a: Vec<T>, b: Vec<T>) -> Vec<T> {
    unimplemented!()
}
```

### Sample Tests
```
#[cfg(test)]
mod tests {
    use super::*;
    #[test]
    fn returns_expected() {
        assert_eq!(array_diff(vec![1,2], vec![1]), vec![2]);
        assert_eq!(array_diff(vec![1,2,2], vec![1]), vec![2,2]);
        assert_eq!(array_diff(vec![1,2,2], vec![2]), vec![1]);
        assert_eq!(array_diff(vec![1,2,2], vec![]), vec![1,2,2]);
        assert_eq!(array_diff(vec![], vec![1,2]), vec![]);
    }
}
```

### 문제 풀이
```
fn array_diff<T: PartialEq>(a: Vec<T>, b: Vec<T>) -> Vec<T> {
    a.into_iter().filter(|v|{
        for item in &b {
            if *v == *item {
                return false
            }
        }
        true
    }).collect()
}
```

### 다른 좋은 풀이
```
fn array_diff<T: PartialEq>(a: Vec<T>, b: Vec<T>) -> Vec<T> {
    a.into_iter().filter(|x| !b.contains(x)).collect()
}
```
