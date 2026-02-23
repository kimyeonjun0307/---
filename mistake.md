#C++ Mistake Archive

## iterator 실수
### 틀린 코드 + 왜 틀렸는가 + 주의사항 + 정답
```cpp
for(int i = 65; i<=90; i++)
    {
        auto it = find(s.begin(),s.end(),i);
        if( *it != 0)
        {
            v[i-65] +=1;
        }
    }
/*
[왜 틀렸는가]

1. find는 값이 아니라 위치(iterator)를 반환함
   - 찾으면 해당 위치 iterator
   - 못 찾으면 s.end()

 (못 찾았을때 기본값 0을 반환하지도 않고 못 찾았다고 마지막 위치도 아니다.
 단순히, 범위 끝을 가리키는 iterator를 반환할 뿐이기때문에,
 *it으로 접근해도 마지막 위치 값을 꺼내는 것이 아니라 런타임 에러.)
   
2. *it != 0 은 존재 여부 판단이 아님
   - 대부분의 문자 아스키 값은 0이 아님 → 항상 true
   - 찾지 못하면 it == s.end() → *it 접근하면 런타임 에러 발생!!!

3. 목적과 맞지 않음
   - 문자 개수 세기는 find가 아니라 직접 카운트 필요
   - 반복문 안에서 find 사용 → O(26*N) 비효율

[주의사항]

- 존재 여부 확인: if(it != s.end())
- end() 상태에서 * 역참조 금지
- 문자 빈도는 배열/벡터 직접 카운트

[정답]

if (it != s.end()); it이 가리키는 값이 유효하다.

```

## iterator 실수
### 틀린 코드 + 왜 틀렸는가 + 주의사항 + 정답
```cpp
/*
[틀린 코드]

int result = max_element(v.begin(), v.end());  // ❌ 타입 오류
cout << v[*result] << "\n";                    // ❌ *도 의미 없음

[왜 틀렸는가]

1. max_element()는 iterator(위치)를 반환함
   - "가장 큰 값이 있는 위치를 가리키는 포인터" 같은 개념
   - int에 바로 저장하면 타입 오류 발생

2. * 연산자는 iterator 상태에서만 값에 접근 가능
   - int에 저장 후 *result는 의미 없음
   - *는 iterator 상태에서 붙여야 함
[정답]

 1: iterator에서 인덱스로 변환
    int result = max_element(v.begin(), v.end()) - v.begin();
    cout << (char)('A' + result) << "\n";  

 2: auto로 iterator 그대로 저장
    auto it = max_element(v.begin(), v.end());
    cout << (char)('A' + (it - v.begin())) << "\n";  

 3: 값만 꺼내기
    int mx = *max_element(v.begin(), v.end());
    cout << mx << "\n";

```
