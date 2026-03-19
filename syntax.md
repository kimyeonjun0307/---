# C++ Syntax Archive

---

## reverse

###  사용법 + 언제 + 주의사항

```cpp
#include <algorithm>

string s = "hello";

reverse(s.begin(), s.end());

/*
[어떻게 쓰는지]

→ 문자열을 제자리(in-place)에서 뒤집는다. == 추가 메모리 없이 원본 변경을 한다는 뜻.
→ 시간복잡도 O(N) == 문자열 길이에 비례해서 시간이 증가한다는 뜻.

[언제 쓰는지]
1. 팰린드롬 검사  == 앞에서 읽어도, 뒤에서 읽어도 같은 문자열인지 확인하는 것.( 거꾸로 해도 똑같으면 팰린드롬)
2. 문자열 비교 문제
3. 구현 문제에서 "뒤집기" 요구
4. 투포인터 / 그리디 방향 전환
5. vector, 배열 등 다양한 컨테이너에도 사용 가능

[무엇을 조심해야 하는지]
1. 원본이 바뀐다 → 필요하면 복사해서 사용
2. <algorithm> 헤더 필수
3. 문자열이 매우 길면 O(N) 성능 고려
*/

```

## isdigit

### 사용법 + 언제 + 주의사항

```cpp
#include <cctype>

char c = '3';

if(isdigit(c))
{
    cout << "숫자다";
}

/*
[어떻게 쓰는지]

→ 문자가 숫자인지 확인하는 함수 (0 ~ 9)
→ 반환값: true(숫자) / false(숫자 아님)

[언제 쓰는지]
1. 문자열이 "숫자인지" 판단할 때
   (ex: "123" vs "pikachu")
2. 입력이 숫자인지 문자로 구분해야 할 때
3. stoi 쓰기 전에 안전 체크
4. 포켓몬 도감 같은 문제 (문자 vs 숫자 구분)

[무엇을 조심해야 하는지]
1. char 하나만 검사한다
   → 문자열이면 s[0] 이런 식으로 하나씩 봐야 함

2. 문자열 전체가 숫자인지 확인하려면 반복문 필요
   ex)
   bool ok = true;
   for(char c : s)
   {
       if(!isdigit(c)) ok = false;
   }

3. 아스키 기반이라 영어/숫자만 확실
   (한글 이런 건 의미 없음)

*/

```

## isupper / islower / toupper / tolower

### 사용법 + 언제 + 주의사항

```cpp
#include <cctype>

isupper(c);   // 대문자 판별
islower(c);   // 소문자 판별
toupper(c);   // 대문자로 변환
tolower(c);   // 소문자로 변환

/*
[어떻게 쓰는지]

→ 문자(char) 하나를 대상으로 대소문자를 판별하거나 변환한다.
→ 내부적으로 아스키(ASCII) 값을 기반으로 동작한다.
→ 반환형
   - isupper / islower : bool (참/거짓)
   - toupper / tolower : 변환된 문자 반환
→ 시간복잡도 O(1) == 항상 일정한 시간.

[언제 쓰는지]

1. 문자열 문제에서 조건 분기
2. 대소문자 무시 비교
3. 입력 정규화 (ex. 사용자 입력 처리)
4. 알파벳 검사
5. 해시, map, set 전처리
6. 파싱 및 토큰 처리

[무엇을 조심해야 하는지]

1. 반드시 <cctype> 헤더 필요
2. string 전체 처리 시 반복문 필수
3. 알파벳이 아니면 false 반환
4. toupper / tolower는 반환값을 다시 저장해야 함
5. signed char 환경에서 UB 방지 위해
   → (unsigned char) 캐스팅이 안전
*/
```

## 문자열 전체 대소문자 변환

### 사용법 + 언제 + 주의사항

```cpp
#include <cctype>

string s = "AbCdEf";

for (int i = 0; i < s.size(); i++) {
    s[i] = tolower(s[i]);
}

/*
[어떻게 쓰는지]

→ 반복문으로 문자열 전체를 순회하면서 변환.
→ 가장 기본적인 방식.
→ O(N) == 문자열 길이에 비례.

[언제 쓰는지]

1. 대소문자 무시 비교
2. 검색 알고리즘
3. 문자열 정규화
4. 데이터 전처리
5. hash key 통일

[무엇을 조심해야 하는지]

1. 원본이 변경됨 → 필요 시 복사
2. 문자열 길이 고려 (최대 입력)
3. 숫자, 특수문자는 그대로 유지
4. 유니코드에는 사용 불가 (코테에서는 거의 없음)
*/
```

## 아스키 코드 대소문자 처리

### 사용법 + 언제 + 주의사항
```cpp
har c = 'a';

if (c >= 'A' && c <= 'Z') {
    c = c + 32;
}

/*
[어떻게 쓰는지]

→ 아스키 코드에서 대문자와 소문자의 차이 32를 이용.
→ 직접 변환하는 low-level 방식.

[언제 쓰는지]

1. 라이브러리 제한 문제
2. 빠른 구현
3. 알고리즘 최적화
4. CP(Competitive Programming) 환경

[무엇을 조심해야 하는지]

1. 영어 알파벳만 가능
2. locale / 국제화 대응 불가
3. 가독성이 떨어짐
4. 실수로 범위를 벗어나면 버그 발생
*/

```

## transform

### 사용법 + 언제 + 주의사항
```cpp
#include <algorithm>

transform(시작, 끝, 결과 시작, 함수);

/*
[어떻게 쓰는지]

→ 범위의 모든 요소를 "한 번씩" 변환해서 저장한다.
→ 반복문 없이 컨테이너 전체를 처리하는 STL 알고리즘.
→ 시간복잡도 O(N).

형태
1. 원본 변경 (in-place)
transform(s.begin(), s.end(), s.begin(), 함수);

2. 다른 컨테이너에 저장
transform(a.begin(), a.end(), b.begin(), 함수);

3. 람다 함수도 가능
transform(v.begin(), v.end(), v.begin(), [](int x){ return x * 2; });

[언제 쓰는지]
1. 문자열 전체 변환 (대문자 ↔ 소문자)
2. 배열 / vector 값 변환
3. 데이터 전처리
4. 수학 연산 일괄 적용
5. 반복문 줄이고 코드 가독성 향상

[무엇을 조심해야 하는지]
1. 결과 컨테이너 크기가 충분해야 함
2. 함수는 입력 1개 → 출력 1개 형태
3. iterator 범위 실수 주의
4. tolower 같은 경우 :: 붙이는 것 중요
*/
```

## max_element
### 사용법 + 언제 + 주의사항
```cpp
#include <algorithm>

max_element(시작, 끝);

/*
[어떻게 쓰는지]

→ 범위 내에서 가장 큰 값을 "가리키는 iterator"를 반환한다.
→ 값이 아니라 iterator를 반환하므로 * 로 역참조해야 한다. ( *를 안붙이면 위치(iterator), *를 붙이면 "그 위치의 값")
→ 내부적으로 선형 탐색을 한다.
→ 시간복잡도 O(N).

형태
1. 값만 구하기
int mx = *max_element(v.begin(), v.end());

2. 인덱스 구하기
int idx = max_element(v.begin(), v.end()) - v.begin();

3. 배열에서도 가능
int mx = *max_element(arr, arr + N);

4. 사용자 정의 기준 (람다)
max_element(v.begin(), v.end(), [](int a, int b){
    return a < b;   // 기본 오름차순 기준과 동일
});

[언제 쓰는지]
1. vector / 배열에서 최댓값 찾기
2. 빈도 배열에서 가장 많이 나온 값 찾기
3. 그리디 문제
4. DP 결과 중 최대값 선택
5. 정렬 없이 최대값만 필요할 때

[무엇을 조심해야 하는지]
1. <algorithm> 헤더 필수
2. 빈 컨테이너에서 사용하면 오류
3. iterator 반환 → 반드시 * 필요
4. 범위 설정 실수 주의 (begin, end)
*/
```
## find
### 사용법 + 언제 + 주의사항
```cpp
#include <algorithm>

find(시작, 끝, 찾을값);
ex)auto it = find(v.begin(), v.end(), x);

/*
[어떻게 쓰는지]

→ 범위 내에서 특정 값을 찾는다.
→ 찾으면 그 위치를 가리키는 iterator 반환.
→ 못 찾으면 끝 iterator (end) 반환.
→ 내부적으로 선형 탐색 수행.
→ 시간복잡도 O(N).

형태
1. 존재 여부 확인
auto it = find(v.begin(), v.end(), x);

if (it != v.end()) {
    // 찾음
}

2. 인덱스 구하기
int idx = find(v.begin(), v.end(), x) - v.begin();

3. 배열에서도 사용 가능
auto it = find(arr, arr + N, x);

4. 문자열에서도 사용 가능
auto it = find(s.begin(), s.end(), 'A');

[언제 쓰는지]
1. 특정 값 존재 여부 확인
2. 중복 검사
3. 구현 문제에서 조건 체크
4. 방문 여부 확인
5. 문자열에서 문자 탐색

[무엇을 조심해야 하는지]
1. <algorithm> 헤더 필수
2. iterator 반환 → 반드시 end와 비교
3. 못 찾으면 v.end() 반환
4. 정렬 여부와 상관없이 사용 가능
5. 큰 데이터에서는 O(N) 성능 고려
*/

```

##  매핑 unordered_map
### 사용법 + 언제 + 주의사항
```cpp
#include <unordered_map>

unordered_map<key타입, value타입> 이름;

/*
[어떻게 쓰는지]

→ key를 통해 value를 빠르게 찾는다.
→ 내부적으로 해시 테이블 사용.
→ 평균 시간복잡도 O(1).
→ 순서는 보장되지 않는다.

형태
1. 선언 + 초기화
unordered_map<string, double> grade = {
    {"A+", 4.5},
    {"A0", 4.0},
    {"B+", 3.5}
};

2. 값 접근
double score = grade["A+"];

3. 존재 여부 확인
auto it = grade.find("A+");

if (it != grade.end()) {
    // 존재함
}

4. 값 수정 / 삽입
grade["C+"] = 2.5;

5. 자동 생성 주의
grade["X"];                    // 그래서 나오는 중급스킬: grade.at() 를 쓰게되면, key가 없을때 에러발생. 단, 프로그림애 종료됨
                              // 하지만 그래서 나오는 고급스킬: grade.find() 를 쓴다. 위에서 iterator 반환 하듯이 없으면 grade.end()를 반환, 직접 처리해줘야 하지만 이 말은 곧 제어할 수 있다는 것. 용도에 따라 쓰면됨.
// key가 없으면 기본값으로 생성됨
// double이면 0.0

6. 반복문 순회
for (auto &p : grade) {
    cout << p.first << " " << p.second << "\n";
}

7. 삭제
grade.erase("A+");

8. 전체 삭제
grade.clear();

[언제 쓰는지]

1. 문자열 → 숫자 매핑
   (학점 변환, 문자 변환 등)

2. 빈도수 세기
   (단어 개수, 문자 개수)

3. 빠른 탐색이 필요할 때

4. 중복 체크

5. 좌표, 이름, ID 같은 Key 기반 문제

6. 해시 기반 문제 대부분

[무엇을 조심해야 하는지]

1. <unordered_map> 헤더 필수

2. [] 사용 시 자동 생성됨
   → 존재 여부 확인 후 접근하는 습관

   if (grade.find(key) != grade.end())

3. 순서 보장 안 됨
   → 정렬 필요하면 map 사용

4. 해시 충돌 가능
   → 평균 O(1), 최악 O(N)

5. key는 hash 가능한 타입이어야 함
   → string, int 등

6. 매우 큰 데이터에서 메모리 사용량 큼
*/
```
## Map
###  사용법 + 언제 + 주의사항
```cpp
#include <map>

map<key타입, value타입> 이름;

/*
[어떻게 쓰는지]

→ key → value 저장
→ key 기준 자동 정렬
→ 내부적으로 Red-Black Tree 사용
→ 시간복잡도 O(log N)

형태
1. 선언
map<string, int> m;

2. 값 삽입
m["apple"] = 3;
m["banana"] = 5;

3. 값 접근
cout << m["apple"];

4. 존재 여부 확인
if (m.find("apple") != m.end()) {
    // 존재함
}

5. 반복문
for (auto &p : m) {
    cout << p.first << " " << p.second << "\n";
}

6. 삭제
m.erase("apple");

7. 전체 삭제
m.clear();

[언제 쓰는지]

1. 정렬된 상태 유지 필요할 때
2. key 기준 순회해야 할 때
3. 사전 순 출력 문제
4. 범위 탐색 (lower_bound)

[무엇을 조심해야 하는지]

1. unordered_map보다 느림
2. [] 사용 시 자동 생성됨
3. 단순 탐색이면 unordered_map이 더 좋음
*/
```
##unordered_set
###사용법 + 언제 + 주의사항
```cpp

#include <unordered_set>

unordered_set<타입> 이름;

/*
[어떻게 쓰는지]

→ 중복 없는 데이터 저장
→ 정렬 없음
→ 내부적으로 해시 테이블 사용
→ 평균 시간복잡도 O(1)

형태
1. 선언
unordered_set<int> s;

2. 삽입
s.insert(10);

3. 존재 여부 확인
if (s.count(10)) {
    // 존재함
}

또는
if (s.find(10) != s.end())

4. 삭제
s.erase(10);

5. 반복문
for (auto &x : s) {
    cout << x << "\n";
}

또는
for (auto it = s.begin(); it != s.end(); ) {
    if (삭제조건) {
        it = s.erase(it);  // erase 후 iterator는 다음 위치 반환
    } else {
        ++it;              // 삭제 안 하면 그냥 다음으로 이동
    }
}

6. 크기
s.size();

7. 전체 삭제
s.clear();

[언제 쓰는지]

1. 빠른 존재 확인 (핵심 ⭐)
2. 중복 체크
3. 숫자 카드, 문자열 집합 문제
4. 순서 필요 없는 경우

[무엇을 조심해야 하는지]

1. 순서 보장 안 됨
2. 해시 충돌 → 최악 O(N)
3. set보다 메모리 많이 씀
4. 정렬 필요하면 사용 ❌

*/
```


## unordered_set에서 pair 응용법
### 사용법 + 언제 + 주의사항
```cpp
#include <iostream>
#include <unordered_set>
#include <utility>
using namespace std;

struct PairHash {// struct란 class가 함수로 사용할 객체를 만들 블루 프린트라면 struct는 자료형 객체를 만들때 쓰는 블루프린트.
    size_t operator()(const pair<int,int>& p) const {
        return hash<int>()(p.first) ^ (hash<int>()(p.second) << 1);
    }
};

unordered_set<pair<int,int>, PairHash> s;

/*
[어떻게 쓰는지]

→ unordered_set<pair<int,int>, PairHash> 형태로 사용
→ pair는 기본 hash가 없어서 "해시 함수"를 직접 정의해야 한다

→ 삽입: s.insert({x, y});
→ 조회: s.count({x, y});  // 있으면 1, 없으면 0

→ 평균 시간복잡도 O(1)

[언제 쓰는지]

1. 좌표 방문 체크 (BFS / DFS)
2. (x, y) 형태 상태 저장
3. pair 단위 중복 제거
4. 간선 (u, v) 저장

→ "값 2개를 묶어서 빠르게 관리"할 때 사용

[무엇을 조심해야 하는지]

1. PairHash 없으면 컴파일 에러 (pair는 기본 hash 없음)
2. unordered_set은 순서 없음 (정렬 X)
3. 값 수정 불가 → erase 후 insert
4. 해시 충돌 가능 (최악 O(N), 보통 문제 없음)

[추가 지식]

→ 해시 함수는 pair를 하나의 숫자로 바꾸는 역할
→ XOR(^) + shift(<<)로 두 값을 섞어서 충돌을 줄임

[코테 팁]

unordered_set<long long> s;
long long key = ((long long)x << 32) | y;

→ 해시 정의 없이 더 간단하게 사용 가능 (실전에서 많이 씀)
*/

```

##set
### 사용법 + 언제 + 주의사항
```cpp
#include <set>

set<타입> 이름;

/*
[어떻게 쓰는지]

→ 중복 없는 데이터 저장
→ 자동 정렬 (오름차순)
→ 내부적으로 Red-Black Tree 사용
→ 시간복잡도 O(log N)

형태
1. 선언
set<int> s;

2. 값 삽입
s.insert(3);
s.insert(1);
s.insert(3); // 중복 무시

3. 값 확인
if (s.find(3) != s.end()) {
    // 존재함
}

4. 삭제
s.erase(3);

5. 반복문
for (auto &x : s) {
    cout << x << "\n";
}

6. 크기
s.size();

7. 비우기
s.clear();

[언제 쓰는지]

1. 중복 제거 + 정렬이 동시에 필요할 때
2. 자동 정렬된 상태 유지해야 할 때
3. 범위 탐색 (lower_bound 등)
4. 순서가 중요한 문제

[무엇을 조심해야 하는지]

1. unordered_set보다 느림 (O(log N))
2. 삽입할 때마다 정렬됨 → 비효율 가능
3. 단순 중복 제거면 vector + sort가 더 빠름
*/
```

##해시 튜닝 hash tuning (unordered_set / unordered_map)
## 사용법 + 언제 + 주의사항
```cpp
#include <unordered_set>

unordered_set<int> s;

s.reserve(100000);        // 예상 원소 개수
s.max_load_factor(0.7);   // 충돌 허용 비율

/*
[어떻게 쓰는지]

→ 해시 테이블의 내부 크기(버킷 수)를 미리 설정한다.
→ 충돌을 줄여서 평균 O(1) 성능을 더 안정적으로 유지한다.

1. reserve(n)
   → n개의 원소를 넣을 것을 "미리 알려주는 것"
   → rehash(재정렬) 횟수를 줄여 성능 향상

2. max_load_factor(x)
   → 버킷 1개당 평균 원소 수 제한
   → load factor = (원소 개수 / 버킷 개수)

   예: 0.7이면
   → 버킷 10개일 때 원소 7개 수준 유지

---

[언제 쓰는지]

1. 데이터가 많을 때 (10만 ~ 100만 이상)
2. insert / find를 매우 많이 할 때
3. 실시간 성능 중요한 경우 (게임, 서버, 실시간 처리)
4. 해시 충돌로 인한 성능 저하를 방지하고 싶을 때

---

[무엇을 조심해야 하는지]

1. reserve는 "넣을 개수 기준"으로 설정
   → 너무 크게 잡으면 메모리 낭비
   → 너무 작으면 효과 없음

2. max_load_factor 낮추면
   → 속도 ↑ (충돌 감소)
   → 메모리 사용 ↑

3. unordered_set은 최악의 경우 O(N) 가능
   → (해시 충돌 많으면 발생)

4. 데이터 적으면 튜닝 의미 없음
   → 오히려 코드만 복잡해짐

---

[핵심 한 줄 요약]

→ "미리 공간 넉넉히 잡고, 충돌 줄여서 진짜 O(1) 만들기"
*/
```

## subtr
### 사용법 + 언제 + 주의사항
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s = "hello";

    string sub = s.substr(0, 3); // s[0]~s[2] 부분 추출 → "hel"
    cout << sub << "\n";
}

/*
[어떻게 쓰는지]

→ 문자열 s에서 일부 구간을 잘라 새로운 문자열을 만든다.
→ substr(start_index, length) 형태 사용
   - start_index: 시작 위치 (0부터)
   - length: 잘라낼 길이
→ 원본 문자열은 변하지 않는다. (새로운 string 반환)
→ 시간복잡도 O(length)

[언제 쓰는지]

1. 문자열 슬라이싱 필요할 때
2. 접두사/접미사 비교 문제
3. 특정 길이 부분 문자열을 key로 사용할 때 (unordered_set/unordered_map)
4. 문자열 패턴 탐색 / 해시 / rolling hash 문제

[무엇을 조심해야 하는지]

1. start_index + length가 문자열 길이를 초과하지 않도록 주의
2. 원본 문자열 s는 변하지 않음 → 변경하려면 별도 대입 필요
3. substr로 만들어진 문자열은 새 객체 → 큰 문자열 반복 시 메모리/시간 고려
*/

```

##getline
### 사용법 + 언제 + 주의사항
```cpp
#include <string>
#include <iostream>

string s;

getline(cin, s);

/*
[어떻게 쓰는지]

→ 입력 스트림(cin)에서 한 줄 전체를 읽어서 문자열에 저장한다.
→ 공백, 탭을 포함한 모든 문자 입력 가능.
→ 엔터(줄바꿈)가 나올 때까지 읽는다.
→ 줄바꿈 문자는 버리고 문자열에 저장하지 않는다.

→ 시간복잡도 O(N) == 입력된 문자열 길이에 비례해서 시간 증가.


[언제 쓰는지]

1. 문장 입력 (공백 포함 문자열)
   → 이름, 문장, 텍스트 등

2. 문자열 문제 (예: [Baekjoon Online Judge](chatgpt://generic-entity?number=0))
   → 단어가 아닌 문장 단위 입력일 때 필수

3. 공백 포함 입력 문제
   → 예: "hello world", "C++ is fun"

4. 한 줄씩 처리해야 하는 문제
   → 로그, 텍스트 분석, 문자열 파싱

5. stringstream과 함께 사용
   → 한 줄 입력 후 숫자나 단어 분리

6. EOF까지 반복 입력
   → 파일 입력, 테스트 케이스 개수 없는 문제


[무엇을 조심해야 하는지]

1. cin >> 와 함께 사용 시 버퍼 문제
   → cin >> 는 엔터를 남긴다.
   → getline은 그 엔터를 바로 읽고 종료된다.

   해결 방법:
   cin.ignore();

2. 빈 줄 입력 가능
   → 사용자가 그냥 엔터를 누르면 빈 문자열("")이 들어온다.

3. EOF 처리 시
   → while(getline(cin, s)) 패턴 사용

4. 문자열이 매우 길 경우
   → 메모리, 시간 고려 필요

5. Windows 줄바꿈(\r\n) 문제
   → 일부 환경에서 '\r' 제거 필요할 수 있음.


[추가 꿀팁]

1. 문자열 여러 줄 입력
   while(getline(cin, s))

2. 숫자 + 문자열 혼합 입력
   cin >> n;
   cin.ignore();
   getline(cin, s);

3. 입력 속도 최적화
   ios::sync_with_stdio(false);
   cin.tie(NULL);

*/
```

##stringstream
### 사용법 + 언제 + 주의사항
```cpp


#include <sstream>
#include <string>
#include <iostream>

string s = "10 20 30";

stringstream ss(s);

int x;
while (ss >> x)
{
    cout << x << '\n';
}

/*
[어떻게 쓰는지]

→ 문자열을 입력 스트림처럼 사용하게 해주는 도구.
→ 공백 기준으로 데이터를 나눠서 읽을 수 있다.
→ cin >> 처럼 사용 가능.
→ 원본 문자열은 바뀌지 않는다.

→ 시간복잡도 O(N) == 문자열 길이에 비례


[언제 쓰는지]

1. 한 줄 입력 후 단어 분리
   예: "hello world C++"

2. 숫자 여러 개 한 줄에 입력
   예: "10 20 30 40"

3. getline + 숫자 파싱
   → 백준에서 매우 자주 나옴
   → 테스트 케이스 개수 없이 한 줄씩 처리할 때

4. 문자열 파싱 문제
   → 로그 분석, CSV 처리, 공백 기준 분리

5. 자료형 변환
   → string → int
   → string → double


[무엇을 조심해야 하는지]

1. <sstream> 헤더 필수

2. 공백 기준 분리
   → 기본은 공백(스페이스, 탭, 엔터)

3. 한 번 읽으면 내부 포인터가 이동한다
   → 다시 쓰려면 새로 만들어야 한다

   stringstream ss(s);
   ss.clear();
   ss.str(new_string);

4. getline과 같이 쓸 때
   → cin >> 후에는 cin.ignore() 필요

5. 매우 긴 문자열 반복 사용 시
   → 성능 고려 (하지만 대부분 문제 없음)


[자주 쓰는 패턴]

1. getline + stringstream

   string line;
   getline(cin, line);

   stringstream ss(line);
   int x;
   while (ss >> x)
   {
       // 처리
   }

2. 구분자 직접 지정

   string token;
   while (getline(ss, token, ','))
   {
       // 쉼표 기준 분리
   }

*/
```

## XOR

###  사용법 + 언제 + 주의사항
```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5, b = 3;
    int c = a ^ b; // XOR 연산
    cout << c;     // 출력: 6
}
/*
[어떻게 쓰는지]

→ ^ 연산자를 사용해서 두 정수의 비트 단위 XOR 계산.
→ 각 비트가 서로 다르면 1, 같으면 0으로 계산됨.
→ 두 개 이상도 가능: a ^ b ^ c
→ 동일한 값이 두 번 XOR 되면 0으로 사라지는 성질 있음.
   예: a ^ a ^ b = b

[언제 쓰는지]
1. 문제에서 "두 값이 다르면 1, 같으면 0" 논리 필요할 때
2. 백준 3009번 같은 "두 개는 같고 하나만 다른 값" → 남은 값 바로 찾기
3. 배열에서 한 개만 다른 숫자 찾기 (짝수 개씩 등장하는 수 문제)
4. 비트 마스크, 집합 표현, 특정 알고리즘 최적화
5. swap(a,b) = a^b^a 방식 등 간단한 비트 트릭

[무엇을 조심해야 하는지]
1. 부호 있는 정수에서 비트 연산 결과가 음수일 수 있음
2. XOR은 교환/결합 법칙 성질 이용 → 순서 고려하지 않아도 되지만 이해 필수
3. 너무 많은 비트 연산을 중첩하면 가독성 떨어질 수 있음
4. 초기값 0과의 XOR은 원본 값 그대로 유지됨
*/

```
## min, max, *min_element, *max_element
### 사용법 + 언제 + 주의사항
```cpp
#include <bits/stdc++.h>
using namespace std;

// 두 값 비교
int a = 5, b = 9;
int minVal1 = min(a,b);
int maxVal1 = max(a,b);

// 여러 값 비교 (C++11 이상)
int minVal2 = min({a, b, 2, 7});
int maxVal2 = max({a, b, 2, 7});

// 벡터 / 배열 전체 최소/최대
vector<int> v = {5, 2, 9, 1, 7};
int minVal3 = *min_element(v.begin(), v.end());
int maxVal3 = *max_element(v.begin(), v.end());

// 직접 최소/최대 갱신 (벡터 없이 실전용)
int xArr[] = {5,2,9,1,7};
int xmin = INT_MAX, xmax = INT_MIN;
for(int x : xArr){
    xmin = min(xmin, x);
    xmax = max(xmax, x);
}

/*
[어떻게 쓰는지]

1. min(a,b) / max(a,b)
→ 단순히 두 값 비교

2. min({a,b,c,d}) / max({a,b,c,d})
→ 여러 값 중 최소/최대

3. *min_element(v.begin(), v.end()) / *max_element(v.begin(), v.end())
→ 벡터나 배열 전체에서 최소/최대
→ iterator 반환 → * 붙여서 값 사용
→ 시간복잡도 O(N)

4. INT_MAX / INT_MIN 활용 + 반복문
→ 벡터 없이 최소/최대 갱신 가능
→ 실전 코드에서 메모리 절약 / 속도 약간 향상

[언제 쓰는지]

1. 벡터/배열에서 최소값/최대값 필요할 때
2. 범위 내 최솟값/최댓값 갱신할 때
3. 문제에서 x,y,w,h 등 최솟값/최댓값 찾을 때
4. 두 값, 여러 값, 전체 배열 등 상황에 따라 적절히 선택

[무엇을 조심해야 하는지]

1. min_element / max_element → iterator 반환, 실제 값 필요 시 * 필요
2. 배열/벡터가 비어있으면 undefined behavior
3. INT_MAX / INT_MIN 초기화 → 적절히 사용
4. O(N) 연산 → 매우 큰 벡터에서는 성능 고려
*/
```

## 브루트 포스 - 비트마스크
### 사용법 + 언제 + 주의사항
```cpp

#include <iostream>
using namespace std;

int main() {
    int arr[3] = {1, 2, 3};
    int n = 3;

    // 0~7까지 모든 부분집합 탐색 (2^3)
    for(int mask = 0; mask < (1 << n); mask++) {
        cout << "{ ";
        for(int i = 0; i < n; i++) {
            if(mask & (1 << i)) {  // i번째 원소 선택 여부
                cout << arr[i] << " ";
            }
        }
        cout << "}\n";
    }

    return 0;
}

/*
[어떻게 쓰는지]

→ 정수의 비트(0/1)로 선택 여부를 표시하여, N개의 원소로 만들 수 있는 모든 부분집합(조합)을 탐색
→ mask & (1 << i) : i번째 원소가 선택되었는지 확인
→ mask | (1 << i) : i번째 원소를 포함시키기
→ mask ^ (1 << i) : i번째 원소 상태 반전
→ 시간복잡도 O(2^N * N) == 모든 부분집합 + 내부 원소 확인

[언제 쓰는지]
1. 부분집합(all subsets) 탐색
2. 조합/선택 문제에서 각 원소 선택 여부 표시
3. DP + 상태(bitmask) 문제
4. N이 작을 때 2^N 완전 탐색 가능

[무엇을 조심해야 하는지]
1. N이 크면 2^N이 너무 커서 시간 초과 가능 (보통 N ≤ 20)
2. 비트 연산자(&, |, ^, <<, >>) 사용법 숙지 필요
3. mask 값 자체는 int 범위 고려 (최대 31~32비트)
4. 원소 선택/해제 논리 실수 주의
*/
```
## reference
### 사용법 + 언제 + 주의사항
```cpp
#include <iostream>
using namespace std;

void change(int& x) {
    x = 100;
}

int main() {
    int a = 10;
    change(a);

    cout << a; // 100
}

/*
[어떻게 쓰는지]

→ 변수 옆에 & 붙여서 "참조(별명)" 생성
→ 복사 없이 원본 데이터를 직접 사용
→ 함수 매개변수에서 많이 사용됨

ex)
int& ref = a;        // a의 별명
void func(int& x)    // 참조로 받기

→ 메모리 복사 없이 값 변경 가능


[언제 쓰는지]

1. 함수에서 원본 값을 바꿔야 할 때
   → swap, 값 수정, 상태 변경

2. 큰 데이터 구조 전달할 때
   → vector, 배열, string 등
   → 복사 비용 줄이기 (성능 핵심)

3. 반복문에서 원소 직접 수정할 때
   → for (int& x : v)

4. 함수 성능 최적화
   → 불필요한 복사 제거

5. const reference
   → 읽기 전용 + 복사 방지
   → 실무/코테에서 매우 자주 사용


[무엇을 조심해야 하는지]

1. 선언과 동시에 초기화 필수
   int& r; // ❌ 안됨

2. 다른 변수로 "재참조" 불가능
   int a = 1, b = 2;
   int& r = a;
   r = b; // b를 가리키는게 아니라 a에 b값을 넣음

3. 원본이 바뀐다
   → 의도치 않은 변경 주의

4. 지역변수 참조 반환 금지
   int& func() {
       int a = 10;
       return a; // ❌ (메모리 사라짐)
   }

5. const 붙이면 수정 불가
   const int& r = a;

6. 임시값 참조 불가
   int& r = 10; // ❌

*/
```
##const reference
### 사용법 + 언제 + 주의사항
```cpp
#include <iostream>
#include <vector>
using namespace std;

void print(const vector<int>& v) {
    // v[0] = 10; // ❌ 수정 불가

    for (const int& x : v) {
        cout << x << " ";
    }
}

int main() {
    vector<int> v = {1, 2, 3};
    print(v);
}

/*
[어떻게 쓰는지]

→ const + reference
→ "읽기 전용 참조"

ex)
const int& r = a;
const vector<int>& v

→ 복사는 안 하고, 수정도 못함
→ 즉, 빠르고 안전함


[언제 쓰는지]

1. 큰 데이터 읽기 전용으로 받을 때 (최우선)
   → vector, string, 배열 등
   → 복사 비용 제거 + 안전성 확보

2. 함수에서 값 변경 의도가 없을 때
   → 실수 방지 (코드 신뢰도 상승)

3. 반복문에서 값만 읽을 때
   → for (const int& x : v)

4. 임시값 받을 때 (중요 포인트)
   → const reference는 임시값도 가능

ex)
const int& r = 10; // ✅ 가능


[무엇을 조심해야 하는지]

1. 값 수정 불가
   → r = 20; ❌

2. const 빼면 실수로 값 변경 가능
   → 의도 명확하게 할 것

3. 너무 작은 타입(int 등)은 굳이 필요 없음
   → int는 그냥 값으로 받아도 됨

4. 원본이 바뀌면 참조 값도 같이 바뀜
   → "읽기 전용"이지 "고정값"은 아님

*/
```
## stable_sort
### 사용법 + 언제 + 주의사항
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<pair<int, int>> v = {
        {1, 100},
        {2, 200},
        {1, 300},
        {2, 400}
    };

    stable_sort(v.begin(), v.end(), [](auto a, auto b) {
        return a.first < b.first;
    });

    for (auto x : v) {
        cout << x.first << " " << x.second << "\n";
    }
}

/*
[어떻게 쓰는지]

→ stable_sort(begin, end)
→ stable_sort(begin, end, 비교함수)

→ 기본은 sort와 동일하게 사용
→ 차이점: "안정 정렬" (stable)

→ 안정 정렬이란?
   → 같은 값이면 "기존 순서 유지"

ex)
(1,100), (1,300)
→ 정렬 후에도 순서 그대로 유지됨


[언제 쓰는지]

1. "같은 값일 때 순서 유지"가 중요한 문제
   → 순서 자체가 의미 있을 때

2. 다중 기준 정렬 (핵심)
   → 2순위, 3순위 정렬

ex)
1. second 기준으로 먼저 정렬
2. first 기준으로 stable_sort

→ first 같으면 second 순서 유지됨

3. 정렬 후에도 원래 순서 정보가 필요할 때

4. 데이터의 "안정성"이 중요한 경우


[무엇을 조심해야 하는지]

1. 일반 sort보다 느림
   → sort: O(N log N)
   → stable_sort: O(N log N) (하지만 상수 시간 더 큼)

2. 메모리 추가 사용 가능
   → 내부적으로 추가 공간 사용

3. 굳이 필요 없으면 sort 쓰는 게 더 좋음

4. comparator 잘못 쓰면 의미 없음
   → "같을 때 false 반환" 유지해야 안정성 의미 있음

*/
```
## lower_bound
### 사용법 + 언제 + 주의사항
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40};

    auto it = lower_bound(v.begin(), v.end(), 25);

    cout << *it; // 30
}

/*
[어떻게 쓰는지]

→ lower_bound(시작, 끝, 값)

→ "값 이상이 처음 나오는 위치"를 iterator로 반환

ex)
v = {10, 20, 30, 40}

lower_bound(v.begin(), v.end(), 25)
→ 30 위치 반환

lower_bound(v.begin(), v.end(), 30)
→ 30 위치 반환


→ index로 쓰고 싶으면
lower_bound(...) - v.begin()


[언제 쓰는지]

1. 정렬된 배열에서 위치 찾을 때 (핵심)
   → 이분 탐색 자동 수행 (O(log N))

2. 좌표 압축 (필수 패턴)
   → 값의 순서(index) 구할 때

3. 특정 값이 들어갈 위치 찾기
   → 삽입 위치 계산

4. 범위 문제 (이분 탐색 활용)
   → 조건 만족하는 첫 위치 찾기

5. 중복 값 처리
   → 같은 값 중 "첫 번째 위치"


[무엇을 조심해야 하는지]

1. 반드시 정렬되어 있어야 함
   → sort 안 하면 결과 ❌

2. iterator 반환함
   → 값이 아니라 "주소"

3. 범위 벗어날 수 있음
   → 못 찾으면 end() 반환

ex)
auto it = lower_bound(v.begin(), v.end(), 100);
if (it == v.end()) // 체크 필수

4. vector뿐 아니라 배열도 가능

int arr[] = {1,2,3,4};
lower_bound(arr, arr+4, 3);

5. 시간복잡도 O(log N)
   → 매우 빠름

*/
```
## 람다
### 사용법 + 언제 + 주의사항
```cpp
#include <algorithm>

vector<int> v = {3, 1, 4, 2};

sort(v.begin(), v.end(), [](int a, int b){
    return a > b; // 내림차순 정렬
});

pair 정렬할때(정렬할때 아주 요긴함)
vector<pair<int,int>> v;

sort(v.begin(), v.end(), [](auto a, auto b){
    if(a.first == b.first)
        return a.second > b.second;
    return a.first < b.first;
});


/*
[어떻게 쓰는지]

→ 함수를 따로 만들지 않고, 그 자리에서 바로 정의해서 사용하는 "익명 함수"
→ 주로 sort, find, for_each 같은 알고리즘과 같이 사용

기본 형태:

[] (매개변수) {
    실행문
};

→ [] : 캡처 (외부 변수 가져오기)
→ () : 함수 인자
→ {} : 함수 내용

---

[언제 쓰는지]

1. 정렬 기준 커스터마이징 (가장 많이 씀 ⭐)
   → sort에서 조건 직접 정의

2. 간단한 함수 한 번만 쓸 때
   → 굳이 함수 따로 만들 필요 없음

3. 우선순위 조건 만들 때
   → pair 정렬, 구조체 정렬 등

4. 알고리즘 함수와 같이 쓸 때
   → find_if, for_each 등

---

[무엇을 조심해야 하는지]

1. 캡처 개념 중요
   → [] 안에 외부 변수 가져와야 사용 가능

   예:
   [=] : 값 복사
   [&] : 참조 (원본 수정 가능)

2. 코드 길어지면 가독성 떨어짐
   → 복잡하면 그냥 함수로 빼는 게 좋음

3. return 반드시 필요 (bool 조건일 때)
   → sort에서는 true/false 기준 중요

4. 비교 함수 방향 실수 주의

   a > b → 내림차순
   a < b → 오름차순

---

[핵심 한 줄 요약]

→ "그 자리에서 바로 쓰는 미니 함수 (특히 정렬에서 핵심)"
*/
```
