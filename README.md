# Y

Класс-ярлык для часто употребляемых выражений [Yii framework](http://www.yiiframework.com)


## Получение

`git clone git://github.com/Svyatov/Yii-shortcut.git`


## Использование

### Установка

Положите файл `Y.php` в папку `protected/components` вашего приложения.


### Применение

1) в виджете нам нужно создать урл по роуту

```php
<?php
// стандартная запись
Yii::app()->controller->createUrl(...);

// мой класс
Y::url(...);
```

2) достаем/устанавлием значение какого-то кэша

```php
<?php
// стандартная запись
Yii::app()->cache->get(...);
Yii::app()->cache->set(...);

// мой класс
Y::cacheGet(...);
Y::cacheSet(...);
```

3) с куками аналогично;

4) достаем значение CSRF токена для вставки в форму или для ajax-запроса

```php
<?php
// стандартная запись
Yii::app()->request->csrfToken;

// мой класс
Y::csrf();
```

5) надо передать параметр CSRF в ajax-запросе jQuery?

```phtml
// стандартная запись
<script>
$.post('/bla/bla', {<?=Yii::app()->request->csrfTokenName;?>: '<?=Yii::app()->request->csrfToken;?>', ...} ... );
</script>

// мой класс
<script>
$.post('/bla/bla', {<?=Y::csrfJsParam();?>, ...} ... );
</script>
```

6) быстрый дамп с подсветкой:

```php
<?php
// стандартная запись
echo '<pre>';
CVarDumper::dump(...);
Yii::app()->end();

// мой класс
Y::dump(...);
```

7) выводим результат действия для ajax-запроса

```php
<?php
// стандартная запись
echo $result;
Yii::app()->end();
// или
echo json_encode($result);
Yii::app()->end();

// мой класс
Y::end($result);
// или соответственно
Y::endJson($result);
```

8) редиректы

```php
<?php
// стандартная запись
$this->redirect($this->createUrl(...)); // самая короткая запись
Yii::app()->request->redirect(Yii::app()->controller->createUrl(...)); // а это для компонента, например

// мой класс
Y::redir(...); // можно использовать в любом месте одинаково
```

9) определение статуса текущего юзера (авторизован или нет)

```php
<?php
// стандартная запись
if (Yii::app()->user->isGuest) ... // если гость
// или
if (!Yii::app()->user->isGuest) ... // если авторизован

// мой класс
if (Y::isGuest()) ... // гость
// или
if (Y::isAuthed()) ... // авторизован
// можно было обойтись одним методом, но так код получается нагляднее
```

Как видите количество кода сокращается минимум в 2 раза, что соответственно сокращает минимум в 2 раза время на его написание и отладку.


## Контакты

Проблемы, предложения, пожелания жду сюда: [leonid@svyatov.ru](mailto:leonid@svyatov.ru)


## История

* **v1.1.4** / 27.09.2011

    `fix` Исправлена ошибка, при которой не устанавливалась кука, если в методе cookieSet() был опущен аргумент $expire.

    `chg` Методы для работы с cookies теперь "нативнее" используют класс CCookieCollection.

* **v1.1.3** / 19.07.2011

    `new` Добавлены методы: getGet, getPost, getRequest, getPdo, hasFlash.

    `chg` В методы cache, cacheDelete, cacheGet, cacheSet добавлен параметр $cacheId, который позволяет указать произвольный кэш-компонент, а не только 'cache'.

    `chg` В метода endJson добавлен параметр $options, который позволяет передавать флаги функции json_encode.

    `chg` Убрано еще больше "магии", слегка оптимизированы некоторые методы.

* **v1.1.0** / 29.05.2011

    `new` Добавлены методы: isAjaxRequest, isPutRequest, isDeleteRequest, isPostRequest, isSecureConnection.

    `new` В README добавлена история версий. README.markdown переименован в README.md

    `chg` Максимально убрана вся "магия" внутри методов.

    `chg` В метод baseUrl() добавлен параметр $absolute, по умолчанию равный false. Параметр позволяет получить не относительный, а абсолютный URL.

    `chg` В метод cookieGet() добавлен параметр $default, по умолчанию равный null. Параметр позволяет вернуть произвольное значение, если куки с указанным именем не существует.

    `chg` В метод param() добавлен параметр $default, по умолчанию равный null. Параметр позволяет вернуть произвольное значение, если параметра приложения с указанным именем не существует. Также переработан код метода.

    `chg` Исправлены, улучшены и дополнены phpDoc комментарии.

* **v1.0.4** / 05.01.2011

    Небольшой рефакторинг, класс выложен на GitHub.

* **v1.0.3** / 16.12.2010

    `fix` Исправлен баг в функции param().

* **v1.0.2** / 16.12.2010

    `new` Добавлена функция hasAccess().

    `new` Доработана функция param() - теперь поддерживаются вложенные параметры (обращаться к вложенному параметру можно через точку: 'site.title' вернет значение param['site']['title']) - за идею спасибо sergebezborodov.

    `chg` Небольшой рефакторинг.