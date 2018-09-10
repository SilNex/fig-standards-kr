# 코딩 스타일 가이드

이 가이드는 기본 코딩 표준인 [PSR-1]의 확장이다.

이 가이드의 의의는 다른 사람이 만든 코드를 볼때 이해하기 힘듬을 줄이기 위함이다.  
또한 PHP 코드 형식을 지정하는 방법에 대한 일련의 집합과 목표들을 나열한다.

이 규칙 스타일은 많고 다양한 프로젝트들의 공통점에서 나온것 이다.
다양한 개발자들이 여러 프로젝트들을 통해서 협업 할때, 모든 프로젝트에서 하나의 가이드라인을 사용하는 것은 도움이된다.  
그러므로, 이 가이드라인의 장점은 규칙 차제가 아니라 이러한 규칙을 공유함에 있다.

이 문서에 "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", "OPTIONAL" 키워드 들은 [RFC 2119]에 설명된 대로 해석된다.

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/silnex/fig-standards-kr/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/silnex/fig-standards-kr/blob/master/accepted/PSR-1-basic-coding-standard.md

## 1. 요약

- **[MUST]** 코드는 반드시 "코딩 스타일 가이드" PSR [[PSR-1]]을 따라야 한다.

- **[MUST]** 코드는 반드시 4개의 스페이스를 사용해 들여쓰기를 해야한다.

- **[MUST NOT]** 한 행의 길이에 엄격한 제한을 둬선안된다.;  
  **[MUST]** 제한이 필요하다면 120자로 엄격하지 않은 제한을 둬야한다.;  
  **[SHOULD]** 한 행은 80자 이하가 좋다.

- **[MUST]** `namespace` 선언 뒤에 반드시 하나의 빈 행을 둬야한다.  
  **[MUST]** 또한 `use` 선언 블록 뒤에 반드시 하나의 빈 행을 둬야한다. 

- **[MUST]** 클래스를 여는 중괄호는 반드시 클래스 선언 다음 행에 둬야하며, 
  닫는 중괄호는 본문 다음행에 둬야한다.

- **[MUST]** 메소드를 여는 중괄호는 반드시 메소드 선언 다음 행에 둬야하며,
  닫는 중괄호는 본분 다음행에 둬야한다.

- **[MUST]** [가시성]은 모든 송성과 메소드에 반드시 선언되어야한다.  
  **[MUST]** `abstract`와 `final`은 반드시 [가시성] 전에 선언되어야 한다.  
  **[MUST]** `static`은 반드시 [가시성] 뒤에 선언 되어야 한다.


[가시성]:http://php.net/manual/kr/language.oop5.visibility.php

- **[MUST]** [제어구조] 키워드는 반드시 하나의 스페이스를 뒤에 작성되어야한다.   **[MUST NOT]** 메소드와 함수를 호출해선 안된다.

- **[MUST]** [제어구조]를 여는 중괄호는 반드시 같은 행에 둬야하며, 
  닫는 중괄호는 본문 다음행에 둬야한다.

- **[MUST NOT]** [제어구조]를 여는 괄호 뒤에는 절대 공백을 둬선 안되며,  
  **[MUST NOT]** [제어구조]를 닫는 괄호 앞에는 절대 공백을 둬선 안된다.

[제어구조]:http://php.net/manual/kr/language.control-structures.php

### 1.1. 예제

이 예는 아래의 가이드 중 일부를 간략히 설명한다.:

~~~php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleMethod($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
~~~

## 2. 일반

### 2.1. 기본 코딩 표준 

**[MUST]** 코드는 반드시 "코딩 스타일 가이드" PSR [[PSR-1]]을 따라야 한다.

### 2.2. 파일

**[MUST]** 모든 PHP 파일은 Unix LF (라인피드)를 사용해야한다.

**[MUST]** 모든 PHP 파일은 하나의 빈 줄로 끝내야한다.

**[MUST]** 닫는 `?>` 태그는 PHP만 있는 파일에선 반드시 생략되어야한다.

### 2.3. 행

**[MUST NOT]** 행의 길이에는 제한은 두어선 안된다.

**[MUST]** 제약을 둔다면 120자 정도로 약한 제약을 둬야한다.
**[MUST]** 스타일 검사기는 줄길이에 대해서 경고 혹은 에러 알람을 띄워선 안된다.

**[SHOULD NOT]** 행은 80자 이하인것이 좋다. 행은 길수록 나눠서 각각 80자 내외로 맞춰 여러줄로 표현하는 것이 좋다. 

**[MUST NOT]** 공백이 아닌 행의 끝에는 공백 문자가 있으면 안된다.

**[MAY]** 가독성을 높이기위해 공백행을 추가할 수 있다.

**[MUST NOT]** 한줄에 하나이상의 문장이 있어선 안된다.

### 2.4. Indenting

**[MUST]** 들여쓰기는 탭이 아닌 반드시 4개의 스페이스로 들여쓰기 해야한다.

> 주의1: 스페이스와 탭을 섞어서 쓰지 말고 하나의 공백 표현 만을 사용해라,
> 이는 비교(diff), 패치(patches), 기록(history), 주석(annotations)등에 도움을 준다.
> 또한 공백을 사용하면 들여쓰기를 쉽게 세분화해 삽입 할 수 있다. 

### 2.5. 키워드(Keywords) 와 True/False/Null

**[MUST]** PHP [keywords]는 반드시 소문자로만 사용해야한다.

**[MUST]** PHP 상수 `true`, `false`, `null`는 반드시 소문자로만 사용해야한다.

[keywords]: http://php.net/manual/kr/reserved.keywords.php

## 3. 네임스페이스 와 Use 선언

**[MUST]** 위 키워드가 존재하는 경우, `namespace`을 선언한 다음에 반드시 하나의 빈 줄을 삽입해야한다.

**[MUST]** 위 키워드가 존재하는 경우, 모든 `use` 선언은 `namespace` 선언 뒤에 와야한다.

**[MUST]** `use`는 반드시 하나의 키워드에 하나의 선언을한다.

**[MUST]** 반드시 빈 줄 뒤에 `use` 단락이 와야한다.

예제:

~~~php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... 추가적인 PHP 코드 ...

~~~

## 4. 클래스, 속성, 메소드

단어 "class"는 모든 클래스, 인터페이스, 특성을 나타낸다.

### 4.1. Extends과 Implements

**[MUST]** `extends`와 `implements` 키워드는 클레스명과 같은 행에 선언되어야 한다.

**[MUST]** 클래스를 여는 중괄호는 반드시 클래스명 다음줄에 있어야한다;  
닫는 중괄호는 반드시 클래스 본문 다음 행에 둬야한다.

~~~php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
~~~

**[MAY]** `implements` 목록은 여러 행으로 둘 수도 있다. (다만, 각각의 줄은 한 번만 들여쓰기된다.)  
**[MUST]** 만약 여러 행으로 둔다면 첫번째 항목은 반드시 다음 행에 둬야하며,
오직 한 행에 하나의 인터페이스(interface)만 둘 수 있다.

~~~php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
~~~

### 4.2. 속성

**[MUST]** 모든 속성은 [가시성](Visibility)을 반드시 선언해야 한다.

**[MUST NOT]** `var` 키워드는 속성 선언엔 사용해선 안된다.

**[MUST NOT]** 한 명령문에 하나 이상의 속성을 선언해선 안된다.

**[SHOULD NOT]** 보호 혹은 개별적인 가시성을 나타내기 위해 속성 이름앞에 밑줄을 두지 않는 것이 좋다.

속성 선언은 다음과 같다.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
~~~

### 4.3. 메소드

**[MUST]** 모든 속성은 [가시성]을 반드시 선언해야 한다.

**[SHOULD NOT]** 보호된 혹은 개별적인 가시성을 나타내기 위해 메소드 이름 앞에 밑줄을 두지 않는 것이 좋다.

**[MUST NOT]** 메소드 이름뒤에 공백을 둬선 안된다.  
**[MUST]** 여는 중괄호는 메소드 이름 행 아래에 둬야하며, 
닫는 괄호는 본문 다음 행에 둬야한다.  
**[MUST NOT]** 절대 여는 괄호 뒤에 공백을 둬선 안되며,
닫는 괄호 전에도 공백을 둬선 안된다.

메소든 선언은 다음을 따른다.
괄호, 쉼표, 공백 및 중괄호의 배치에 유의해야한다.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
~~~

### 4.4. 메소드 인수

**[MUST NOT]** 인수 목록은 각각의 쉼표(,)앞에 공백을 둬선 안되며,  
**[MUST]** 반드시 각각의 쉼표(,)뒤에 공백을 둬야한다.

**[MUST]** 기본값을 가진 메소드 인수들은 반드시 목록의 끝에 와야한다.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
~~~

**[MAY]** 인수 목록은 여러 행으로 나뉠수도 있으며, 행 별로 한번의 들여 쓰여질수 있다.  
**[MUST]** 여러줄로 표시할 때는 첫번째 인수는 반드시 다음 행에 있어야 하며, 
오직 한 행에 하나의 인수만이 존재 할 수 있다.

**[MUST]** 인수 목록을 여러 행으로 나눌때, 닫는 괄호와 여는 중괄호 사이에는 한 줄의 빈 행을 둬야한다.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
~~~

### 4.5. `abstract`, `final`, `static`

**[MUST]** `abstract`와 `final`이 있다면, 반드시 [가시성] 선언 앞에 와야한다.

**[MUST]** `static`이 있다면, 반드시 [가시성] 선언 뒤에 와야한다.

~~~php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
~~~

### 4.6. 메소드와 함수 콜

**[MUST NOT]** 메소드 혹은 함수 콜을 만들때, 메소드 혹은 함수명과 여는 괄호 사이에는 절대 공백을 둬선 안되며, 여는 괄호 뒤에 공백을 둬서도 안된다.
또한 닫는 괄호 앞에도 절대 공백을 둬선 안된다.  
인수 리스트는 절대 각각의 쉼표(,) 앞에 공백이 들어가선 안되며,  
**[MUST]** 반드시 각각의 쉼표(,) 뒤에 공백이 들어가야한다.

~~~php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
~~~

**[MAY]** 인수 목록은 여러 행으로 나뉠수도 있으며, 행 별로 한번의 들여 쓰여질수 있다.  
**[MUST]** 여러줄로 표시할 때는 첫번째 인수는 반드시 다음 행에 있어야 하며, 
오직 한 행에 하나의 인수만이 존재 할 수 있다.

~~~php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
~~~

## 5. 제어 구조체

일반적인 제어 구조체 규칙은 다음을 따른다.:

- **[MUST]** 반드시 제어 구조체 키워드 뒤에 하나의 공백을 둔다.
- **[MUST NOT]** 절대 여는 괄호 뒤에 공백을 둬선 안된다.
- **[MUST NOT]** 절대 닫는 괄호 앞에 공백을 둬선 언된다.
- **[MUST]** 반드시 닫는 괄호와 여는 중괄호 사이에는 하나의 공백이 있어야한다.
- **[MUST]** 반드시 구조체 본문은 한번 들여쓰기 되어야 한다.
- **[MUST]** 반드시 닫는 중괄호는 본문 다음 행에 둬야한다.

**[MUST]** 구조체의 본문은 반드시 중괄호를 사용해야한다. 이는 구조체를 어떻게 보는지 표준화 하고 새로운 행이 본문에 추가 될 때에 오류 발생 가능성을 낮춰준다.

### 5.1. `if`, `elseif`, `else`

`if` 구조는 다음과 같다. 괄호, 공백, 중괄호의 위치에 주의 해야한다.
그리고 `else`와 `elseif`는 이전 본문을 닫는 중괄호와 같은 라인에 있어야한다.

~~~php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
~~~

**[SHOULD]** 모든 키워드는 한 단어인 것이 보기 좋기에, `else if`키워드 보다 키워드 `elseif`를 쓰는것이 좋다.

### 5.2. `switch`, `case`

`switch` 구조는 다음과 같다. 괄호, 공백, 중괄호의 위치에 유의해야 한다.  
**[MUST]** `case` 문단은 `switch`보다 반드시 한번 들여쓰기 해야한다.
그리고 `break` 키워드 (또는 다른 종료 키워드)는 반드시 `case` 본문과 같은 들여쓰기를 해야한다.  
**[MUST]** 비여 있지 않은 `case`본문에 의도적으로 `break` (또는 다른 종료 키워드)를 넣지 않은경우 (fall-through) `// no break`를 넣어줘야한다.

~~~php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
~~~

### 5.3. `while`, `do while`

`wheil` 구조체는 다음과 같다. 괄호, 공백, 중괄호의 유의해야 한다.

~~~php
<?php
while ($expr) {
    // structure body
}
~~~

이와 유사하게, `do while` 구조체는 다음과 같다. 괄호, 공백. 중괄호의 유의해야 한다.

~~~php
<?php
do {
    // structure body;
} while ($expr);
~~~

### 5.4. `for`

`for` 구조체는 다음과 같다. 괄호, 공백, 중괄호의 유의해야 한다.

~~~php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
~~~

### 5.5. `foreach`

`foreach` 구조체는 다음과 같다. 괄호, 공백, 중괄호의 유의해야 한다.

~~~php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
~~~

### 5.6. `try`, `catch`

`try catch` 구조체는 다음과 같다. 괄호, 공백, 중괄호의 유의해야 한다.

~~~php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
~~~

## 6. 클로저(Closures)

**[MUST]** 클로저는 반드시 `function` 키워드 뒤, `use` 키워드 앞과 뒤에 공백을 삽입해 선언해야 한다.

**[MUST]** 여는 중괄호는 반드시 같은 행에 둬야 하고,
닫는 중괄호는 본문 다음 줄에 둬야한다.

**[MUST NOT]** 여는 인수, 혹은 변수 목록의 여는 괄호 뒤에는 절대 공백을 둬선 안되며, 닫는 괄호 앞에도 공백을 둬선 안된다.

**[MUST NOT]** 인수, 변수 목록에서 각각의 쉼표(,) 앞에 공백을 둬선 안되며,  
**[MUST]** 반드시 쉼표다음에 공백을 둬야한다.

**[MUST]** 기본값을 가진 클로저 인수는 인수 목록 끝에 와야한다.

클로저 선언은 다음과 같다. 괄호, 쉼표, 공백, 그리고 중괄호에 유의해야 한다. :

~~~php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
~~~

**[MAY]** 인수와 변수 목록은 한행에 한번씩 들여쓰기해 여러 행으로 나눌 수 있다.
**[MUST]** 그렇게 나눈다면 반드시 첫번째 항목은 다음줄에 있어야하며, 오직 한행에 하나의 인수 혹은 변수만이 올 수 있다.

**[MUST]** 끝나는 목록(인수 또는 변수의 여부)가 여러 줄로 나뉘어 질 때, 반드시 닫는 괄호와 여는 중괄호는 빈 행을 사용해 각 행에 있어야한다.

다음은 인수가 없거나, 변수가 여러 행으로 나눠진 클로저에 예제이다.

~~~php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
    // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
    // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
    // body
};
~~~

구조 지정 규칙은 함수 또는 메소드 호출에서 클로저가 인수로 직접 호출 될 때도 적용된다.

~~~php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
~~~

## 7. 결론

이 가이드에는 의도적으로 생략한 스타일과 연습등의 많은 요소가 있다.
다음이 포함되지만 이에 국한되지는 않는다.  
~~불분명~~  
~~There are many elements of style and practice intentionally omitted by this
guide. These include but are not limited to:~~

- 전역 변수 및 전역 상수 선언

- 함수 선언

- 연산자와 할당

- 행간 정렬

- 주석 및 문서 블록

- 클래스 이름의 접두사 및 접미사

- 모범 사례


**[MAY]** 향후 권장 사항은 스타일이나 실습의 요소 또는 기타 요소를 다루기 위해 이 가이드를 수정하고 추가 할 수 있다.

## 부가 A. 설문 조사

이 가이드를 작성하면서 그룹 공통의 사항들을 결정하기위해 여러 맴버가 참여한 프로젝트들을 조사했다.  
조사는 후일을 위해 여기 기록되어 유지된다.

### A.1. 설문 조사 데이터

    url,http://www.horde.org/apps/horde/docs/CODING_STANDARDS,http://pear.php.net/manual/en/standards.php,http://solarphp.com/manual/appendix-standards.style,http://framework.zend.com/manual/en/coding-standard.html,https://symfony.com/doc/2.0/contributing/code/standards.html,http://www.ppi.io/docs/coding-standards.html,https://github.com/ezsystems/ezp-next/wiki/codingstandards,http://book.cakephp.org/2.0/en/contributing/cakephp-coding-conventions.html,https://github.com/UnionOfRAD/lithium/wiki/Spec%3A-Coding,http://drupal.org/coding-standards,http://code.google.com/p/sabredav/,http://area51.phpbb.com/docs/31x/coding-guidelines.html,https://docs.google.com/a/zikula.org/document/edit?authkey=CPCU0Us&hgd=1&id=1fcqb93Sn-hR9c0mkN6m_tyWnmEvoswKBtSc0tKkZmJA,http://www.chisimba.com,n/a,https://github.com/Respect/project-info/blob/master/coding-standards-sample.php,n/a,Object Calisthenics for PHP,http://doc.nette.org/en/coding-standard,http://flow3.typo3.org,https://github.com/propelorm/Propel2/wiki/Coding-Standards,http://developer.joomla.org/coding-standards.html
    voting,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,no,no,no,?,yes,no,yes
    indent_type,4,4,4,4,4,tab,4,tab,tab,2,4,tab,4,4,4,4,4,4,tab,tab,4,tab
    line_length_limit_soft,75,75,75,75,no,85,120,120,80,80,80,no,100,80,80,?,?,120,80,120,no,150
    line_length_limit_hard,85,85,85,85,no,no,no,no,100,?,no,no,no,100,100,?,120,120,no,no,no,no
    class_names,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,studly,lower_under,studly,lower,studly,studly,studly,studly,?,studly,studly,studly
    class_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,next,next,next,next,next,next,same,next,next
    constant_names,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper,upper
    true_false_null,lower,lower,lower,lower,lower,lower,lower,lower,lower,upper,lower,lower,lower,upper,lower,lower,lower,lower,lower,upper,lower,lower
    method_names,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel,lower_under,camel,camel,camel,camel,camel,camel,camel,camel,camel,camel
    method_brace_line,next,next,next,next,next,same,next,same,same,same,same,next,next,same,next,next,next,next,next,same,next,next
    control_brace_line,same,same,same,same,same,same,next,same,same,same,same,next,same,same,next,same,same,same,same,same,same,next
    control_space_after,yes,yes,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes,yes
    always_use_control_braces,yes,yes,yes,yes,yes,yes,no,yes,yes,yes,no,yes,yes,yes,yes,no,yes,yes,yes,yes,yes,yes
    else_elseif_line,same,same,same,same,same,same,next,same,same,next,same,next,same,next,next,same,same,same,same,same,same,next
    case_break_indent_from_switch,0/1,0/1,0/1,1/2,1/2,1/2,1/2,1/1,1/1,1/2,1/2,1/1,1/2,1/2,1/2,1/2,1/2,1/2,0/1,1/1,1/2,1/2
    function_space_after,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no,no
    closing_php_tag_required,no,no,no,no,no,no,no,no,yes,no,no,no,no,yes,no,no,no,no,no,yes,no,no
    line_endings,LF,LF,LF,LF,LF,LF,LF,LF,?,LF,?,LF,LF,LF,LF,?,,LF,?,LF,LF,LF
    static_or_visibility_first,static,?,static,either,either,either,visibility,visibility,visibility,either,static,either,?,visibility,?,?,either,either,visibility,visibility,static,?
    control_space_parens,no,no,no,no,no,no,yes,no,no,no,no,no,no,yes,?,no,no,no,no,no,no,no
    blank_line_after_php,no,no,no,no,yes,no,no,no,no,yes,yes,no,no,yes,?,yes,yes,no,yes,no,yes,no
    class_method_control_brace,next/next/same,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/next,same/same/same,same/same/same,same/same/same,same/same/same,next/next/next,next/next/same,next/same/same,next/next/next,next/next/same,next/next/same,next/next/same,next/next/same,same/same/same,next/next/same,next/next/next

### A.2. 설문 사례

`indent_type`:
들여쓰기 타입. `tab` = "탭", `2` or `4` = "공백의 개수"

`line_length_limit_soft`:
약한("soft") 라인 당 문자 수 제한 . `?` = 식별이 불가능하거나 응답이 없음, `no`는 제한 없음을 의미한다.

`line_length_limit_hard`:
강한("hard") 라인 당 문자 수 제한 `?` = 식별이 불가능하거나 응답이 없음, `no`는 제한 없음을 의미한다.

`class_names`:
어떻게 클래스 이름을 지을 것인가. `lower` = 소문자만 사용, `lower_under` = 소문자와 언더바 구분자 사용., `studly` = StudlyCase.

`class_brace_line`:
여는 중괄호를 클래스 키워드와 같은(`same`) 행에 둘것 인가, 아니면 다음(`next`) 행에 둘 것인가?

`constant_names`:
어떻게 클래스 상수 명을 지을 것인가 `upper` = 대문자와 언더바 구분자 사용.

`true_false_null`:
`true`, `false`, `null` 키워드를 소문자(`lower`)로 쓸것인가? 대문자(`upper`)로 쓸것인가?

`method_names`:
메소드 이름을 어떻게 지을 것인가. `camel` = `camelCase`, `lower_under` = 소문자와 언더바 구분자 사용.

`method_brace_line`:
여는 중괄호를 메소드 이름와 같은(`same`) 행에 둘것 인가, 아니면 다음(`next`) 행에 둘 것인가?

`control_brace_line`:
여는 중괄호를 제어 구조체와 같은(`same`) 행에 둘것 인가, 아니면 다음(`next`) 행에 둘 것인가?

`control_space_after`:
제어 구조체 키워드 뒤에 공백을 둘 것인가?

`always_use_control_braces`:
제어 구조체는 항상 중괄호를 사용할 것인가?

`else_elseif_line`:
`else` 또는 `elseif`를 사용할 때, 닫는 중괄호와 같은(`same`) 행에 둘 것인가? 아니면 다음(`next`) 행에 둘 것인가?

`case_break_indent_from_switch`:
`switch`문에 `case`와 `break`가 몇번 들여쓸 것인가?

`function_space_after`:
함수 호출은 함수 이름 다음에 여는 괄호 앞에 공백을 둘 것인가?

`closing_php_tag_required`:
PHP만 있는 파일에 닫는 `?>`태그가 필요한가? 

`line_endings`:
어떤 타입에 끝내는 행이 사용되는가?

`static_or_visibility_first`:
메소드를 선언할 때 `static`을 먼저 쓰는가. 아니면 가시성을 먼저 쓰는가?

`control_space_parens`:
제어 구조체 표현에서 여는 괄호 뒤에 공백이 있고 닫는 괄호 앞에 공백이 있는가?
`yes` = `if ( $expr )`, `no` = `if ($expr)`.

`blank_line_after_php`:
여는 PHP태크 뒤에 빈 행이 있는가?

`class_method_control_brace`:
클래스, 메소드 및 제어 구조에 대해 여는 중괄호가 어떤 행에 표시되는지 요약한다.

### A.3. 설문 결과

    indent_type:
        tab: 7
        2: 1
        4: 14
    line_length_limit_soft:
        ?: 2
        no: 3
        75: 4
        80: 6
        85: 1
        100: 1
        120: 4
        150: 1
    line_length_limit_hard:
        ?: 2
        no: 11
        85: 4
        100: 3
        120: 2
    class_names:
        ?: 1
        lower: 1
        lower_under: 1
        studly: 19
    class_brace_line:
        next: 16
        same: 6
    constant_names:
        upper: 22
    true_false_null:
        lower: 19
        upper: 3
    method_names:
        camel: 21
        lower_under: 1
    method_brace_line:
        next: 15
        same: 7
    control_brace_line:
        next: 4
        same: 18
    control_space_after:
        no: 2
        yes: 20
    always_use_control_braces:
        no: 3
        yes: 19
    else_elseif_line:
        next: 6
        same: 16
    case_break_indent_from_switch:
        0/1: 4
        1/1: 4
        1/2: 14
    function_space_after:
        no: 22
    closing_php_tag_required:
        no: 19
        yes: 3
    line_endings:
        ?: 5
        LF: 17
    static_or_visibility_first:
        ?: 5
        either: 7
        static: 4
        visibility: 6
    control_space_parens:
        ?: 1
        no: 19
        yes: 2
    blank_line_after_php:
        ?: 1
        no: 13
        yes: 8
    class_method_control_brace:
        next/next/next: 4
        next/next/same: 11
        next/same/same: 1
        same/same/same: 6
