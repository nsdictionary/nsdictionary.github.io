---
layout: post
title:  Rust - codewars 문제풀이 2
date:   2020-05-04 10:07:06 +0900
categories: rust
---
[문제 링크](https://www.codewars.com/kata/5502c9e7b3216ec63c0001aa/train/rust)

### Instructions
The Western Suburbs Croquet Club has two categories of membership, Senior and Open. They would like your help with an application form that will tell prospective members which category they will be placed.

To be a senior, a member must be at least 55 years old and have a handicap greater than 7. In this croquet club, handicaps range from -2 to +26; the better the player the lower the handicap.

### Input
Input will consist of a list of lists containing two items each. Each list contains information for a single potential member. Information consists of an integer for the person's age and an integer for the person's handicap.

Note for F#: The input will be of (int list list) which is a List<List>

#### Example Input
`vec![(45, 12), (55,21), (19, -2), (104, 20)])`

### Output
Output will consist of a list of string values (in Haskell: **Open** or **Senior**) stating whether the respective member is to be placed in the senior or open category.

### Example Output
`vec!["Open", "Senior", "Open", "Senior"]`

### Solution
```
fn open_or_senior(data: Vec<(i32, i32)>) -> Vec<String> {
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
        assert_eq!(open_or_senior(vec![(45, 12), (55,21), (19, -2), (104, 20)]), vec!["Open", "Senior", "Open", "Senior"]);
        assert_eq!(open_or_senior(vec![(3, 12), (55,1), (91, -2), (54, 23)]), vec!["Open", "Open", "Open", "Open"]);
    }
}
```

### 문제 풀이
```
fn open_or_senior(data: Vec<(i32, i32)>) -> Vec<String> {
    let mut result: Vec<String> = Vec::new();

    for (age, handicap) in data {
        if age >= 55 && handicap > 7 {
            result.push(String::from("Senior"));
        } else {
            result.push(String::from("Open"));
        }
    }

    result
}
```
- 아주 쉬운 문제라도 러스트 문법에 익숙해지기 위해서 풀어보기
- 가변 벡터를 생성해서 조건에 맞춰 Open 또는 Senior를 push 한뒤 리턴

### 다른 좋은 풀이
```
fn open_or_senior(data: Vec<(i32, i32)>) -> Vec<String> {
    data.into_iter()
        .map(|(age, handicap)| {
            if age >= 55 && handicap > 7 {
                "Senior"
            } else {
                "Open"
            }
            .to_string()
        })
        .collect()
}
```
- map함수를 이용해 튜플을 클로저의 인자로 받아 조건에 따라 스트링을 만들고 collect() 소비 어댑터로 벡터로 변환하여 리턴
- 함수형 풀이가 내가 단순하게 짠 코드보다 훨씬 우아하고 가독성이 좋다.
- 더 중요한것은 가변 스트링 벡터자체를 선언하지 않았기 때문에 성능상으로도 더 우위에 있다.
- 고비용 타입을 쓰지 않고 문제를 해결할수 있는지 한번 더 생각하는 습관을 들여야 겠다.

