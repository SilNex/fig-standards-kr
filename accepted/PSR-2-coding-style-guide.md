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

### 4.2. Properties

Visibility MUST be declared on all properties.

The `var` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

Property names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

A property declaration looks like the following.

~~~php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
~~~

### 4.3. Methods

Visibility MUST be declared on all methods.

Method names SHOULD NOT be prefixed with a single underscore to indicate
protected or private visibility.

Method names MUST NOT be declared with a space after the method name. The
opening brace MUST go on its own line, and the closing brace MUST go on the
next line following the body. There MUST NOT be a space after the opening
parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

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

### 4.4. Method Arguments

In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument
list.

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

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed together on their own line with one space
between them.

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

### 4.5. `abstract`, `final`, and `static`

When present, the `abstract` and `final` declarations MUST precede the
visibility declaration.

When present, the `static` declaration MUST come after the visibility
declaration.

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

### 4.6. Method and Function Calls

When making a method or function call, there MUST NOT be a space between the
method or function name and the opening parenthesis, there MUST NOT be a space
after the opening parenthesis, and there MUST NOT be a space before the
closing parenthesis. In the argument list, there MUST NOT be a space before
each comma, and there MUST be one space after each comma.

~~~php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
~~~

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

~~~php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
~~~

## 5. Control Structures

The general style rules for control structures are as follows:

- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- There MUST be one space between the closing parenthesis and the opening
  brace
- The structure body MUST be indented once
- The closing brace MUST be on the next line after the body

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look, and reduces the likelihood of introducing errors as new
lines get added to the body.

### 5.1. `if`, `elseif`, `else`

An `if` structure looks like the following. Note the placement of parentheses,
spaces, and braces; and that `else` and `elseif` are on the same line as the
closing brace from the earlier body.

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

The keyword `elseif` SHOULD be used instead of `else if` so that all control
keywords look like single words.

### 5.2. `switch`, `case`

A `switch` structure looks like the following. Note the placement of
parentheses, spaces, and braces. The `case` statement MUST be indented once
from `switch`, and the `break` keyword (or other terminating keyword) MUST be
indented at the same level as the `case` body. There MUST be a comment such as
`// no break` when fall-through is intentional in a non-empty `case` body.

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

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

~~~php
<?php
while ($expr) {
    // structure body
}
~~~

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

~~~php
<?php
do {
    // structure body;
} while ($expr);
~~~

### 5.4. `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

~~~php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
~~~

### 5.5. `foreach`

A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

~~~php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
~~~

### 5.6. `try`, `catch`

A `try catch` block looks like the following. Note the placement of
parentheses, spaces, and braces.

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

## 6. Closures

Closures MUST be declared with a space after the `function` keyword, and a
space before and after the `use` keyword.

The opening brace MUST go on the same line, and the closing brace MUST go on
the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list
or variable list, and there MUST NOT be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each
comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument
list.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

~~~php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
~~~

Argument lists and variable lists MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list MUST be on the next line, and there MUST be only one argument or variable
per line.

When the ending list (whether of arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace MUST be placed
together on their own line with one space between them.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

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

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

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

## 7. Conclusion

There are many elements of style and practice intentionally omitted by this
guide. These include but are not limited to:

- Declaration of global variables and global constants

- Declaration of functions

- Operators and assignment

- Inter-line alignment

- Comments and documentation blocks

- Class name prefixes and suffixes

- Best practices

Future recommendations MAY revise and extend this guide to address those or
other elements of style and practice.

## Appendix A. Survey

In writing this style guide, the group took a survey of member projects to
determine common practices.  The survey is retained herein for posterity.

### A.1. Survey Data

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

### A.2. Survey Legend

`indent_type`:
The type of indenting. `tab` = "Use a tab", `2` or `4` = "number of spaces"

`line_length_limit_soft`:
The "soft" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`line_length_limit_hard`:
The "hard" line length limit, in characters. `?` = not discernible or no response, `no` means no limit.

`class_names`:
How classes are named. `lower` = lowercase only, `lower_under` = lowercase with underscore separators, `studly` = StudlyCase.

`class_brace_line`:
Does the opening brace for a class go on the `same` line as the class keyword, or on the `next` line after it?

`constant_names`:
How are class constants named? `upper` = Uppercase with underscore separators.

`true_false_null`:
Are the `true`, `false`, and `null` keywords spelled as all `lower` case, or all `upper` case?

`method_names`:
How are methods named? `camel` = `camelCase`, `lower_under` = lowercase with underscore separators.

`method_brace_line`:
Does the opening brace for a method go on the `same` line as the method name, or on the `next` line?

`control_brace_line`:
Does the opening brace for a control structure go on the `same` line, or on the `next` line?

`control_space_after`:
Is there a space after the control structure keyword?

`always_use_control_braces`:
Do control structures always use braces?

`else_elseif_line`:
When using `else` or `elseif`, does it go on the `same` line as the previous closing brace, or does it go on the `next` line?

`case_break_indent_from_switch`:
How many times are `case` and `break` indented from an opening `switch` statement?

`function_space_after`:
Do function calls have a space after the function name and before the opening parenthesis?

`closing_php_tag_required`:
In files containing only PHP, is the closing `?>` tag required?

`line_endings`:
What type of line ending is used?

`static_or_visibility_first`:
When declaring a method, does `static` come first, or does the visibility come first?

`control_space_parens`:
In a control structure expression, is there a space after the opening parenthesis and a space before the closing parenthesis? `yes` = `if ( $expr )`, `no` = `if ($expr)`.

`blank_line_after_php`:
Is there a blank line after the opening PHP tag?

`class_method_control_brace`:
A summary of what line the opening braces go on for classes, methods, and control structures.

### A.3. Survey Results

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
