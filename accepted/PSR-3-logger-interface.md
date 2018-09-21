로거 인터페이스
================

이 문서는 로깅 라이브러리를 위한 공통 인터페이스를 기술한 문서이다.

주된 목표는 라이브러리가 `Psr\Log\LoggerInterface` 오브젝트를 받아서 간단하고 보편적인 방법으로 로그를 쓸 수 있게하는 것이다.
**[MAY]** 프레임워크와 CMS들은 사용자의 요구에 따라 인터페이스를 확장할 수 있지만,  
**[SHOULD]** 이 문서와 호완되어야 한다. 
이렇게하면 응용 프로그램에서 사용하는 타사 라이브러리가 중앙 집중화된 응용 프로그램 로그를 쓸 수 있다.

이 문서에 "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", "OPTIONAL" 키워드 들은 [RFC 2119]에 설명된 대로 해석된다..

이 문서 안에 있는 단어 `implementor`는 로그 관련 라이브러리 또는 프레임워크에서 `LoggerInterface`를 구현하는 것으로 해석되어야 한다.

로거 사용자는 `user`라고 한다.

[RFC 2119]: http://tools.ietf.org/html/rfc2119

## 1. 상세설명

### 1.1 기초

- `LoggerInterface`는 8개의 [RFC 5424] (debug, info, notice, warning, error, critical, alert, emergency)의 로그 레벨을 쓰는 8가지 메소드를 표현한다.

- 9번째 메소드, `log`는 첫번째 인수로 로그 레벨을 허용한다.
  **[MUST]** 로그 레벨 상수 중 하나를 사용하여 이 메소드를 호출하면 레벨별 메서드를 호출 할 때와 동일한 결과를 가져야한다.  
  **[MUST]** 구현 레벨에 대해 알지 못하면 스펙에 정의되지 않은 레벨로 해당 메소드를 호출하면 반드시 `Psr\Log\InvalidArgumentException`를 던져(throw)야한다.  
  **[SHOULD NOT]** 사용자는 현재 구현이 이를 지원하는지 모른 채 사용자 지정 수준을 사용해서는 안된다

[RFC 5424]: http://tools.ietf.org/html/rfc5424

### 1.2 메시지

- 모든 메소드는 문자열로된 메시지를 받거나, 또는 `__toString()` 메소드를 가진 객체를 받는다.  
  **[MAY]** 구현자는 전달된 객체를 따로 처리 할 수 있다.  
  **[MUST]** 만약 그렇지 않다면 구현자는 반드시 문자열로 변환 해야한다.

- **[MAY]** 메시지는 구현자들이 컨텍스트 배열값으로 변환 할 수 있는 자리표시자를 포함할 수도 있다.

  **[MUST]** 자리표시자명은 반드시 컨텍스트 배열의 키에 해당한다.

  **[MUST]** 자리표시자명은 반드시 한정된 단일 여는 중괄호 `{` 와 닫는 중괄호 `}` 와 함께 써야한다.  
  **[MUST NOT]** 절대 어떠한 공백도 구분 기호나 자리표시자명 사이에 둬어선 안된다.

  **[SHOULD]** 자리표자명은 오직 `A-Z`, `a-z`, `0-9`, `_`, `.` 문자로만 구성되어야 한다. 이 외에 문자사용은 자리표자의 향후 수정을 위해 예약해둡니다.

  **[MAY]** 구현자는 자리표지라를 사용하여 다양한 이스케이프 전략을 구현하고 표시를 위해 로그를 변활 할 수 있다.  
  **[SHOULD NOT]** 사용자는 데이터가 표시 될 컨텍스트를 알 수 없으므로 자리표시자 값을 미리 이스케이프해서는 안된다

다음은 참조용으로만 제공되는 자리표시자 보간법(interpolation)의 구현 예입니다.

  ~~~php
  <?php

  /**
   * 메시지 자리표시자에 컨텍스트 값을 보간한다.
   */
  function interpolate($message, array $context = array())
  {
      // 컨텍스트 키 주위에 중괄호로 대체 배열을 작성해라.
      $replace = array();
      foreach ($context as $key => $val) {
          // 값을 문자열에 형변환 할 수 있는지 확인해라.
          if (!is_array($val) && (!is_object($val) || method_exists($val, '__toString'))) {
              $replace['{' . $key . '}'] = $val;
          }
      }

      // 대체 값을 메시지로 보간하고 리턴한다.
      return strtr($message, $replace);
  }

  // 중괄호로 구분 된 자리표시자 이름이있는 메시지
  $message = "User {username} created";

  // 자리표시자명의 컨텍스트 배열 => 대체 값
  $context = array('username' => 'bolivar');

  // 출력값: "User bolivar created"
  echo interpolate($message, $context);
  ~~~

### 1.3 Context

- 모든 메소드는 배열을 컨텍스트 데이터로 허용한다. 이것은 문자열에 잘 맞지 않는 불필요한 정보를 포함하기 위한것이다. 배열은 어떠한 것이든 담을 수 있다.  
  **[MUST]** 구현자는 반드시 가능한 많이 컨테스트데이터를 수용해 처리해야한다.  
  **[MUST NOT]** 컨텍스트에서 주어진 값은 예외를 던지거나 PHP error, warning, notice를 던저선(throw)안된다.

- **[MUST]** 만약 콘텍스트 데이터 안에 `Exception` 객체를 전달됬다면, 반드시 `'exception'`키가 있어야 한다. 로깅예외는 일반적인 패턴이며, 이로 인해 구현자가 로그백엔드를 지원할 때 예외에서 스택 추적을 추출할 수 있다.
  **[MUST]** 구현자는 무엇이든 포함 할 수 있기 때문에 `'exception'`키가 실제로 사용하기전에 `Exception`인지 반드시 확인해야한다.

### 1.4 헬퍼 클래스와 인터페이스

- `Psr\Log\AbstractLogger` 클래스를 확장하고 일반적인 `log` 메소드를 구현함으로써 `LoggerInterface`를 쉽게 구현할 수 있게 한다. 다른 8개의 메소드들은 메시지와 콘텍스트를 전달하는 것들이다.

- 유사하게 `Psr\Log\LoggerTrait`는 오직 일반적인 `log` 메소드를 사용해서 구현할 수 있다. 특성은 인터페이스를 구현할수없으므로 이 경우에는 `LoggerInterface`를 구현해야한다.

- `Psr\Log\NullLogger`는 인터페이스와 함께 제공된다.   
  **[MAY]** 로거가 제공되지 않으면, 폴백(fall-back) "블랙홀" 구현을 제공하기위해 인터페이스를 사용자이 사용할 수 있습니다. ~~(불분명)~~  
  (It MAY be used by users of the interface to provide a fall-back "black hole" implementation if no logger is given to them.)  
  그러나 컨텍스트 데이터 작성이 비용면에서 조건부 로딩이 더 나은 접근 방법일 수 있다.

- `Psr\Log\LoggerAwareInterface`는 `setLogger(LoggerInterface $logger)` 메소드만을 포함하고 있으며, 임의의 인스턴스를 로거로 오토 와이어(auto-wire)하기 위해 프레임워크에서 사용할 수 있다.

- `Psr\Log\LoggerAwareTrait` 특성은 모든 클래스에서 쉽게 동일한 인터페이스를 구현하는데 사용할 수 있으며, `$this->logger`로 접근 할 수있다.

- `Psr\Log\LogLevel` 클래스는 8개의 로그레벨에 대한 상수를 가지고 있다.

## 2. 패키지

설명된 인터페이스와 클래스는 물론 관련 예외 클래스 및 구현을 확인하는 테스트 세트가 [psr/log](https://packagist.org/packages/psr/log) 패키지의 일부로 제공됩니다.

## 3. `Psr\Log\LoggerInterface`

~~~php
<?php

namespace Psr\Log;

/**
 * Describes a logger instance
 *
 * The message MUST be a string or object implementing __toString().
 *
 * The message MAY contain placeholders in the form: {foo} where foo
 * will be replaced by the context data in key "foo".
 *
 * The context array can contain arbitrary data, the only assumption that
 * can be made by implementors is that if an Exception instance is given
 * to produce a stack trace, it MUST be in a key named "exception".
 *
 * See https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
 * for the full interface specification.
 */
interface LoggerInterface
{
    /**
     * System is unusable.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function emergency($message, array $context = array());

    /**
     * Action must be taken immediately.
     *
     * Example: Entire website down, database unavailable, etc. This should
     * trigger the SMS alerts and wake you up.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function alert($message, array $context = array());

    /**
     * Critical conditions.
     *
     * Example: Application component unavailable, unexpected exception.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function critical($message, array $context = array());

    /**
     * Runtime errors that do not require immediate action but should typically
     * be logged and monitored.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function error($message, array $context = array());

    /**
     * Exceptional occurrences that are not errors.
     *
     * Example: Use of deprecated APIs, poor use of an API, undesirable things
     * that are not necessarily wrong.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function warning($message, array $context = array());

    /**
     * Normal but significant events.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function notice($message, array $context = array());

    /**
     * Interesting events.
     *
     * Example: User logs in, SQL logs.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function info($message, array $context = array());

    /**
     * Detailed debug information.
     *
     * @param string $message
     * @param array $context
     * @return void
     */
    public function debug($message, array $context = array());

    /**
     * Logs with an arbitrary level.
     *
     * @param mixed $level
     * @param string $message
     * @param array $context
     * @return void
     */
    public function log($level, $message, array $context = array());
}
~~~

## 4. `Psr\Log\LoggerAwareInterface`

~~~php
<?php

namespace Psr\Log;

/**
 * Describes a logger-aware instance
 */
interface LoggerAwareInterface
{
    /**
     * Sets a logger instance on the object
     *
     * @param LoggerInterface $logger
     * @return void
     */
    public function setLogger(LoggerInterface $logger);
}
~~~

## 5. `Psr\Log\LogLevel`

~~~php
<?php

namespace Psr\Log;

/**
 * Describes log levels
 */
class LogLevel
{
    const EMERGENCY = 'emergency';
    const ALERT     = 'alert';
    const CRITICAL  = 'critical';
    const ERROR     = 'error';
    const WARNING   = 'warning';
    const NOTICE    = 'notice';
    const INFO      = 'info';
    const DEBUG     = 'debug';
}
~~~
