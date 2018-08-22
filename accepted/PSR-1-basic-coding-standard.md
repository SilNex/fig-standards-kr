# 기본 코딩 표준 가이드

이 섹션은 공유 표준 PHP 코드 간의 상호 운용성을 보장하는데 필요한 표준 코딩 요소를 지켜야하는 것을 포함 한다. ~~불분명~~  
 ~~This section of the standard comprises what should be considered the standard
coding elements that are required to ensure a high level of technical
interoperability between shared PHP code.~~

이 문서에 "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", "OPTIONAL" 키워드 들은 [RFC 2119]에 설명된 대로 해석된다.

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/SilNex/fig-standards-kr/blob/master/accepted/PSR-0.md
[PSR-4]: https://github.com/SilNex/fig-standards-kr/blob/master/accepted/PSR-4-autoloader.md

## 1. 개요

- **[MUST]** 파일은 반드시 `<?php`과 `<?=` 테그만 사용한다.

- **[MUST]** 파일은 반드시 BOM 없이 UTF-8(without BOM) 만 PHP 코드에 사용한다. 

- **[SHOULD]** 파일은 기호(클래스, 함수, 상수 등)를 선언하거나,  
 또는 부작용을 일으킬 수 있는 ini 설정 변경 등을 수행 할 수 있지만,  
 **[SHOULD NOT]** 둘다 수행 해서는 안된다. ~~불분명~~  
~~Files SHOULD *either* declare symbols (classes, functions, constants, etc.)
  *or* cause side-effects (e.g. generate output, change .ini settings, etc.)
  but SHOULD NOT do both.~~

- **[MUST]** 네임스페이와 클래스는 반드시 오버로딩 규정인 PSR: [[PSR-0], [PSR-4]]를 따른다. 

- **[MUST]** 클래스 이름은 반드시 `StudlyCaps`로(첫 글자가 대문자로 시작하게) 선언 되어야 한다.

- **[MUST]** 클래스 상수는 반드시 모두 대문자와 언더바로 선언되어야한다.

- **[MUST]** 메소드 이름은 반드시 `camelCase`(중간에 공백 대신 대문자로 단어를 구분)로 선언 되어야 한다.

## 2. 파일

### 2.1. PHP 태그

**[MUST]** PHP 코드는 반드시 `<?php ?>`(긴 태그)를 사용하거나, `<?= ?>`(짧은 echo 태그)를 사용해야 한다;  
[MUST NOT] 다른 태그로 변형해서 사용해선 절대 안된다.

### 2.2. 문자 인코딩

**[MUST]** PHP 코드의 문자 인코딩은 반드시 BOM(Byte Order Mark)이 없는 UTF-8을 사용해야한다.

### 2.3. 부작용

**[SHOULD]** 파일은 새로운 상징들 (클래스, 함수, 상수 등)은 다른 부작용 들을 일으키지 않아야 하며, 부작용 있는 로직들을 실행 해야하지만, **[SHOULD NOT]** 두개를 같이 수행해선 안된다. ~~불분명~~  
~~A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.~~

"부작용"(side effects)는 클래스, 함수, 상수 등을 선언하는 것과 관련없는 *로직 파일을 불러(include)오는 것 으로 부터 실행 되는 것을 의미합니다.*

"부작용"은 다음을 포함하지만 이에 국한되지 않는다.  
생성 결과 파일(generating output), `require`와 `include`, 외부 서비스와의 연결, ini 세팅 파일 수정, 에러 또는 예외 출력, 전역 또는 정적(static) 변수의 수정, 파일 읽기와 쓰기 등

다음 예제는 선언과 부작용이 모두 포함된 파일이다.  
즉, 다음과 같은 코딩은 반드시 피해야한다.

~~~php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
~~~

다음 예제는 부작용이 없는 선언이 포함된 예제이다.  
즉, 다음과 같은 코딩을 해야한다.

~~~php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
~~~

## 3. 네임스페이스와 클래스 이름

**[MUST]** 네임스페이와 클래스는 반드시 오버로딩 규정인 PSR: [[PSR-0], [PSR-4]]를 따른다. 

각 클래스가 그 자체로 하나의 파일이고 최상위 래벨 벤더 이름을 가진 하나 이상의 네임스페이스에 있음을 의미한다.

**[MUST]** 클래스 이름은 반드시 `StudlyCaps`로(첫 글자가 대문자로 시작하게) 선언 되어야 한다.

**[MUST]** PHP 5.3 및 그 이상의 버전용으로 작성된 코드는 반드시 공식 네임스페이스를 사용해야한다.

예제:

~~~php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
~~~

**[SHOULD]** 5.2.x 및 그 이하의 버전에서는 의사-네임스페이싱 클래스 이름 앞에 `Vendor_`를 붙이는 규칙을 사용해야한다.

~~~php
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
~~~

## 4. 클래스 상수, 속성 과 메소드

"클래스"란 용어는 모든 클래스, 인터페이스와 특성을 의미한다.

### 4.1. 상수

**[MUST]** 클래스 상수는 반드시 모두 대문자와 언더바로 선언되어야한다.

예제:

~~~php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
~~~

### 4.2. 속성

이 가이드는 `$StudlyCaps`, `$camelCase`, `$under_score`속성 이름 사용에 관한 권장 사항을 의도적으로 피한다. 
This guide intentionally avoids any recommendation regarding the use of
`$StudlyCaps`, `$camelCase`, or `$under_score` property names.

**[SHOULD]**어떤 명명 규칙이 사용 되든 합당한 범위 내에서 일관되게 적용되어야한다.
합당한 범위라 함은 공급 업체, 패키지, 메서드 수준일 수 있다.
Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.

### 4.3. 메소드

**[MUST]** 이름은 반드시 `camelCase()`로 선언 되어야 한다.