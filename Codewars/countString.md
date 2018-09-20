## Original Kata : [Count the Digit](https://www.codewars.com/kata/566fc12495810954b1000030/solutions/cpp)  

### Difficulty : 7kyu
### Felt like : Medium  

### Clever Code
``` C++
namespace CountDig
{
  int nbDig(int n, int d)
  {
    std::string digits;
    for (int k = 0; k <= n; ++k)
      digits += std::to_string(k * k);
  
    return std::count(digits.begin(), digits.end(), std::to_string(d)[0]);
  }
}
```

위 코드는 주어진 인자를 바탕으로 숫자를 생성하고 특정 숫자가 몇번 출현했는지를 측정한다.  

#### `int nbDig(int n, int d)`  
이 함수는 입력으로 인자를 2개 받는다.  
`n`은 생성할 숫자의 갯수이고, `d`는 검출할 숫자를 의미한다.  

#### `std::string digits;`  
생성한 수를 저장할 문자열 변수를 선언한다.  

#### `for (int k = 0; k <= n; ++k)`  
주어진 인자 `n` 만큼 숫자를 생성하기 위해 반복문을 구동한다.  

#### `digits += std::to_string(k * k);`  
선언한 문자열에 정해진 규칙으로 숫자를 추가한다.  
문제에서 주어진 규칙은 제곱수이다.  
`std::to_string()` 함수를 사용해 정수를 문자열로 변환한다.  

#### `return std::count(digits.begin(), digits.end(), std::to_string(d)[0]);`  
`algorithm` 라이브러리의 `std::count()` 함수를 사용해 생성된 전체 문자열에서 `d` 문자를 검색한다.  
`std::count()` 함수는 주어진 문자열에서 인자로 정해진 문자가 몇번 사용되었는지 세고 그 횟수를 리턴한다.  

### Things to review  
*std::count() 함수의 3번째 인자에서 왜 char가 아닌 string도 유효한지 알아볼것*  
*namespace CountDig 의 사용이유 알아볼것*  

### My Code  
``` C++
#include <algorithm>

class CountDig
{
public:
    static int nbDig(int n, int d);
};

int CountDig::nbDig(int n, int d)
{
  int tmp;
  int cnt = 0;
  std::string t;
  
  for (int i=0; i<=n; i++)
  {
    tmp = i * i;
    t = std::to_string(tmp);
    cnt += std::count(t.begin(), t.end(), d + '0');
  }
  
  return cnt;
}
```

`tmp` 변수에 즉각적으로 제곱수를 생성하고 `string` 으로의 형변환을 진행한다.  
변환된 문자열을 이용해 입력된 검출할 수를 검사한다.  
검사에는 `count()` 함수가 사용되었다.  
이 함수는 문자열의 시작과 끝을 지정하고 검색할 문자를 입력하면 그 문자의 출현횟수를 반환한다.  

`count()` 의 세번째 인자로 입력된 `d +` ``0``은 사용시 주의가 필요하다.  
그 뜻은 d 변수의 끝에 `0` 을 붙임으로써 인자로 입력받을때의 `int`형에서 `count()` 함수가  
요구하는 `char`형으로 변경한다.  
이 구문은 오직 d변수의 범위가 0 ~ 9 일때만 허용된다.  

이렇게 계산된 값을 `cnt`에 누적하고 모든 수를 반복하면 반환한다.  test