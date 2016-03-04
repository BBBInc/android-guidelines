# android-style-guide
본 문서는 BBB Inc 구성원들의 Android 협업을 쉽고 명확하게 진행하기 위한 스타일 가이드입니다. 구성원들의 의사결정에 따라 수시로 변경될 수 있습니다.

# 목차
- [네이밍](#네이밍)

## 네이밍

### 변수

- 변수 이름은 lowerCamelCase를 사용합니다.
- 멤버 변수 이름에 접두사<sup>Prefix</sup> `m-` 을 붙이지 않습니다.

### 상수

- 상수 이름은 ALL_UPPER_CASE를 사용합니다.
- 각 단어는 underscore `_` 로 분리합니다.
- 상수 이름은 부가 설명 없이도 코드를 이해할 수 있게 작성해야 합니다.

**좋은 예**

```java
final int TAX_RATE = 0.03f;
final int WEDNESDAY = 3;
final int DAYS_IN_WEEK = 7;

…중략…

day = (WEDNESDAY + numberOfDays) % DAYS_IN_WEEK;
```

**나쁜 예**

```java
final int texRate;
final int TAXRATE;
final int DaysInWeek;

…중략…

day = (3 + numberOfDays) % 7;
```

### 약어

- 약어는 항상 대문자로 표시합니다.

**좋은 예**

```java
int userID;
int URLString;
int HTML;
```

**나쁜 예**

```java
int userId;
int urlString;
int html;
```
