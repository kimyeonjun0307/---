# 개선하면 좋을 꿀팁
## bool을 활용 
### 소수 찾기 꿀팁
```cpp
/*
백준 소수 찾기 문제 개선 버전

✅ 개선 포인트
1. result 변수 제거 → 코드 단순화
2. 소수 판별 함수(isPrime) 분리 → 재사용성 증가
3. 짝수 제외 최적화 → 반복 횟수 절반 감소
4. while(true) 대신 while(!isPrime(B)) 사용 → 가독성 향상
5. B < 2 처리 → 0,1 입력 대응

⚡ 추가 개선 가능
- 입력 범위가 매우 큰 경우(10^12 이상) → 밀러-라빈 소수 판별 적용 가능
- 입력 범위가 작은 경우 '에라토스테네스의 체' 적용가능
*/

#include <bits/stdc++.h>
using namespace std;

// 소수 판별 함수
bool isPrime(long long n){
    if(n < 2) return false;         // 0,1은 소수 아님
    if(n == 2) return true;         // 2는 소수
    if(n % 2 == 0) return false;    // 짝수는 소수 아님

    // 홀수만 검사, 3부터 √n까지
    for(long long i = 3; i*i <= n; i += 2){
        if(n % i == 0) return false;
    }
    return true;
}

int main(){
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    long long A, B;
    cin >> A;

    while(A--){
        cin >> B;

        if(B < 2) B = 2;          // 0,1 처리

        // B 이상에서 가장 작은 소수 찾기
        while(!isPrime(B)) B++;

        cout << B << "\n";
    }
}
```

## 나누면서 곱하기로 데이터 줄이기
### 이항계수
```cpp
/*
백준 이항계수 (nCr) 개선 버전

✅ 개선 포인트
1. 팩토리얼 제거 → 오버플로우 방지
2. 곱하면서 나누기 → 값을 작게 유지
3. B = min(B, A-B) → 연산 횟수 절반 감소
4. long long 사용 → 범위 확장

⚡ 추가 개선 가능
- 결과가 매우 큰 경우 → Big Integer (문자열 곱셈)
- 모듈러 연산 필요 시 → 페르마의 소정리 + 빠른 거듭제곱

💡 핵심 아이디어
nCr = A! / (B!(A-B)!)
→ 약분하면
nCr = (A * (A-1) * ... * (A-B+1)) / B!

→ 그래서 "곱하면서 나눈다"
*/

#include <bits/stdc++.h>
using namespace std;

long long combination(long long A, long long B){
    if(B > A) return 0; // 예외 처리

    B = min(B, A - B);  // 대칭성 활용

    long long result = 1;

    for(long long i = 1; i <= B; i++){
        result = result * (A - i + 1) / i;
    }

    return result;
}

int main(){
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    long long A, B;
    cin >> A >> B;

    cout << combination(A, B);
}
```
