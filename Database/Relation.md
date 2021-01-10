## Relation

관계형 데이터베이스의 3가지 관계

- [1:1 관계](#1:1-관계)
- [1:N 관계](#1:N-관계)
- [M:N 관계](#M:N-관계)

---

### 1:1 관계

양쪽 개체가 **반드시 하나씩** 매핑되는 관계

ex ) 이름과 주민번호

[`USER` table]

| idx  | Name   | IdNumber       |
| ---- | ------ | -------------- |
| 0    | 류세화 | 990226-xxxxxxx |
| 1    | 안재은 | 971113-xxxxxxx |
| 2    | 최예진 | 980718-xxxxxxx |

---

### 1:N 관계

**한 쪽 개체**가 관계를 맺은 개체쪽의 **여러 객체를 가질** 수 있는 관계

ex) 이름과 이메일

| idx  | Name   | idNumber       | Email              |
| ---- | ------ | -------------- | ------------------ |
| 0    | 류세화 | 990226-xxxxxxx | tpghk3tp@naver.com |
| 1    | 류세화 | 990226-xxxxxxx | tpghkRyu@gmail.com |
| 2    | 안재은 | 971113-xxxxxxx | jeunao@naver.com   |
| 3    | 안재은 | 971113-xxxxxxx | jeunaaaa@gmail.com |
| 4    | 안재은 | 971113-xxxxxxx | jeun@kakao.com     |
| 5    | 최예진 | 980718-xxxxxxx | dPwls@daum.net     |

그런데, **사람 한 명이 여러 개의 메일주소**를 가질 수 있으므로 위와 같이 데이터베이스를 설계하면 사람이름과 주민번호가 **중복인 데이터(Row)**가 쌓일 수 있다.

그래서 1:N 관계는 테이블을 나누어서 외래키를 이용해 중복인 데이터를 최소한으로 줄인다.

`USER`

| idx (기본키) | Name   | IdNumber       |
| ------------ | ------ | -------------- |
| 0            | 류세화 | 990226-xxxxxxx |
| 1            | 안재은 | 971113-xxxxxxx |
| 2            | 최예진 | 980718-xxxxxxx |

`EMAIL`

| idx (기본키) | userIdx (USER 외래키❗) | Email              |
| ------------ | ---------------------- | ------------------ |
| 0            | 0                      | tpghk3tp@naver.com |
| 1            | 0                      | tpghkRyu@gmail.com |
| 2            | 1                      | jeunao@naver.com   |
| 3            | 1                      | jeunaaaa@gmail.com |
| 4            | 1                      | jeun@kakao.com     |
| 5            | 2                      | dPwls@daum.net     |

---

### M:N 관계

양쪽 개체 모두에서 1:N 관계가 존재할 때 나타나는 모습. 즉 서로가 서로를 1:N 관계로 보고 있음.

| Idx  | Name   | IdNumber       | 스터디      |
| ---- | ------ | -------------- | ----------- |
| 0    | 류세화 | 990226-xxxxxxx | 뇌지컬 서버 |
| 1    | 류세화 | 990226-xxxxxxx | 컨트롤 바디 |
| 2    | 류세화 | 990226-xxxxxxx | 애자일 회고 |
| 3    | 안재은 | 971113-xxxxxxx | AWS         |
| 4    | 안재은 | 971113-xxxxxxx | 컨트롤 바디 |
| 5    | 최예진 | 980718-xxxxxxx | 컨트롤 바디 |
| 6    | 최예진 | 980718-xxxxxxx | AWS         |

이 테이블의 중복을 줄이려면 ❗❗

`USER`

| idx (기본키) | Name   | IdNumber       |
| ------------ | ------ | -------------- |
| 0            | 류세화 | 990226-xxxxxxx |
| 1            | 안재은 | 971113-xxxxxxx |
| 2            | 최예진 | 980718-xxxxxxx |

`STUDY`

| Idx  | studyName   |
| ---- | ----------- |
| 0    | 애자일 회고 |
| 1    | 컨트롤 바디 |
| 2    | AWS         |
| 3    | 뇌지컬 서버 |

`USER_STUDY `👉🏻 이런 식으로 테이블 하나를 따로 생성해서 외래키로 관리한다

| Idx  | userIdx(USER 외래키) | studyIdx(STUDY 외래키) |
| ---- | -------------------- | ---------------------- |
| 0    | 0                    | 3                      |
| 1    | 0                    | 1                      |
| 2    | 0                    | 0                      |
| 3    | 1                    | 2                      |
| 4    | 1                    | 1                      |
| 5    | 2                    | 1                      |
| 6    | 2                    | 2                      |