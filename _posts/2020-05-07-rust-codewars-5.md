---
layout: post
title:  Rust - codewars 문제풀이 5
date:   2020-05-07 06:45:00 +0900
categories: rust
---
[문제 링크](https://www.codewars.com/kata/587731fda577b3d1b0001196/train/rust)

### Instructions
Write simple .camelCase method (`camel_case` function in PHP, `CamelCase` in C# or `camelCase` in Java) for strings. All words must have their first letter capitalized without spaces.

### Examples
```
camel_case("hello case"); // => "HelloCase"
camel_case("camel case word"); // => "CamelCaseWord"
```

### Solution
```
fn camel_case(str: &str) -> String {
    "Test String".to_string()
}
```

### Sample Tests
```
#[test]
fn sample_test() {
  assert_eq!(camel_case("test case"), "TestCase");
  assert_eq!(camel_case("camel case method"), "CamelCaseMethod");
  assert_eq!(camel_case("say hello "), "SayHello");
  assert_eq!(camel_case(" camel case word"), "CamelCaseWord");
  assert_eq!(camel_case(""), "");
}
```

### 문제 풀이
```
fn camel_case(str: &str) -> String {
    str.split_whitespace().map(|s|{
        let mut v: Vec<char> = s.chars().collect();
        v[0] = v[0].to_uppercase().nth(0).unwrap();
        v.into_iter().collect()
    }).collect::<Vec<String>>().join("")
}
```
- split_whitespace() 메서드로 iterator를 획득
- map 을 통해 첫번째 글자를 대문자로 변환
- join으로 최종 CamelCase형태로 반환

### 다른 좋은 풀이
```
fn camel_case(str: &str) -> String {
    str.split_whitespace()
        .map(|s| [&s[..1].to_uppercase(), &s[1..]].join(""))
        .collect()
}
```
