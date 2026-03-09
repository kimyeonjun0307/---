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
## *min_element, *max_element
### 사용법 + 언제 + 주의사항
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> v = {5, 2, 9, 1, 7};

// 벡터 최소값
int minVal = *min_element(v.begin(), v.end());

// 벡터 최대값
int maxVal = *max_element(v.begin(), v.end());

/*
[어떻게 쓰는지]

→ 벡터(혹은 배열) 전체에서 최소값/최대값을 찾아준다.
→ 반환값은 iterator이므로 실제 값이 필요하면 * 연산자를 사용.
→ 시간복잡도 O(N) == 벡터 길이에 비례해서 시간이 증가함.

[언제 쓰는지]
1. 벡터/배열에서 최소값이나 최대값 필요할 때
2. 범위 내 최솟값/최댓값 갱신할 때
3. 백준 1085번 같은 문제에서 x, y, w, h 중 최솟값/최댓값 찾을 때
4. 부분 범위 최소/최대 필요할 때(v.begin()+i, v.begin()+j)

[무엇을 조심해야 하는지]
1. iterator 반환 → 실제 값 얻으려면 * 필요
2. 벡터가 비어있으면 undefined behavior
3. O(N)이므로 아주 큰 벡터에서는 성능 고려

*/
```
