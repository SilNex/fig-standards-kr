오토로딩 표준
====================

> **사용되지않음** - 2014-10-21에 PSR-0는 deprecated으로 마크 되었다.  
이제 [PSR-4]이 대안으로 채택 되었다.

[PSR-4]: http://www.php-fig.org/psr/psr-4/

다음은 오토로딩 상호 운용성을 위해 반드시 준수해야하는 필수 요구 사항에 대해 설명한다.

필수 요구 사항
---------

* 정규화된 네임스페이스와 클래스는 반드시
  `\<Vendor Name>\(<Namespace>\)*<Class Name>`와 같은 구조를 이뤄야한다. 
* 각각 네임스페이스는 반드시 Top-Level 네임스페이스("Vendor Name")를 가져야한다.
* 각각 네임스페이스는 원하는 만큼 하위 네임스페이스를 가질 수 있다.
* 각각 네임스페이스 분리기호는 파일시스템에서 로드할 때 사용되는 `DIRECTORY_SEPARATOR`(디렉터리 분리기호)로 변환된다.
* 각각 클래스 이름 안에 있는 기호 `_`는 `DIRECTORY_SEPARATOR`로 변환된다.
  네임스페이스에서 `_` 기호는 아무런 의미를 갖지않는다.
* 정규화된 네이스페이스와 클래스를 파일 시스템에서 로드할때 접미사 `.php`가 붙는다.
* vendor names(밴더 이름), 네임스페이스, 클래스 이름들은 알파뱃 소문자와 대문자 문자열로 구성 될 수 있다.

예시
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

네임스페이스와 클래스 이름에서 언더바(`_`)
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

여기서 설정된 표준은 고통없는 오토로더의 상호 운용성을 위해 공통 요소가 가장 적어야합니다.  
PHP 5.3 클래스를 로드 할 수 있닌지 이런 표준을 잘 따르고 있는지 `utilizing this sample SplClassLoader`를 구현해 테스트 할 수 있습니다

구현 예시
----------------------
다음은 위에서 제안된 표준이 자동으로 로드 되는 방식을 간단히 보여주는 함수 예제다.

~~~php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
spl_autoload_register('autoload');
~~~

SplClassLoader 구현
-----------------------------
다음은 제안된 오토로더가 상호 운용성 표준을 따르는 경우 클래스를 로드할 수 있는 간단히 구현한 SplClassLoader입니다.  
이러한 표준을 따르는 PHP 5.3 클래스를 로드하는 권장되는 방법입니다.

* [http://gist.github.com/221634](http://gist.github.com/221634)

