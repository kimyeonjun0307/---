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
