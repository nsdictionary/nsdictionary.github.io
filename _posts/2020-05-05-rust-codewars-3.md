---
layout: post
title:  Rust - codewars 문제풀이 3
date:   2020-05-05 10:07:06 +0900
categories: rust
---
[문제 링크](https://www.codewars.com/kata/55c45be3b2079eccff00010f/train/rust)

### Instructions
Your task is to sort a given string. Each word in the string will contain a single number. This number is the position the word should have in the result.

Note: Numbers can be from 1 to 9. So 1 will be the first word (not 0).

If the input string is empty, return an empty string. The words in the input String will only contain valid consecutive numbers.

### Examples
"is2 Thi1s T4est 3a"  -->  "Thi1s is2 3a T4est"
"4of Fo1r pe6ople g3ood th5e the2"  -->  "Fo1r the2 g3ood 4of th5e pe6ople"
""  -->  ""

### Solution
```
fn order(sentence: &str) -> String {
    // code here
}
```

### Sample Tests
```
#[cfg(test)]
mod tests {
    use super::*;
    #[test]
    fn returns_expected() {
        assert_eq!(order("is2 Thi1s T4est 3a"), "Thi1s is2 3a T4est");
        assert_eq!(order(""), "");
    }
}
```

### 문제 풀이
```
fn order(sentence: &str) -> String {
    let mut v1: Vec<_> = sentence.split_whitespace().map(|v|{
        (
            v,
            v.chars()
                .find(|a| a.is_digit(10))
                .and_then(|a| a.to_digit(10))
                .unwrap()
        )
    }).collect();

    v1.sort_by(|x, y| x.1.cmp(&y.1));
    let v1_len = v1.len();

    v1.iter().enumerate().map(|(i, (x, _))| {
        if i == v1_len-1 {
            format!("{}", x)
        } else {
            format!("{} ", x)
        }
    }).collect()
}
```
- 인자로 받은 String을 map 메서드를 이용해 포함한 숫자와 단어를 튜플로 만들어 그것을 요소로 가지는 벡터로 변환
- 튜플의 숫자에 따라 벡터를 정렬
- 정렬된 벡터내의 문자열만 가져와서 String으로 generate한뒤 반환

### 다른 좋은 풀이
```
fn order(sentence: &str) -> String {
    let mut ws: Vec<_> = sentence.split_whitespace().map(String::from).collect();
    ws.sort_by_key(|s| s.chars().find(|c| c.is_digit(10)).unwrap());
    ws.join(" ")
}
```
- 핳.. 아직 표준 라이브러리 함수들을 잘 몰라서 이렇게 줄이기가 힘들다 .. ㅠㅠ 꾸준히 연습하자 !
