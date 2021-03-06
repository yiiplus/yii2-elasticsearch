Установка
============

## Требования

Требуется версия Elasticsearch 1.0 или выше.

## Получение с помощью Composer

Предпочтительный способ установки расширения через [composer](http://getcomposer.org/download/).

Для этого запустите
```
php composer.phar require --prefer-dist yiisoft/yii2-elasticsearch
```

или добавьте

```json
"yiisoft/yii2-elasticsearch": "~2.0.0"
```

в секцию **require** вашего composer.json.

## Настройка приложения

Для использования расширения, просто добавьте этот код в конфигурацию вашего приложения:

```php
return [
    //....
    'components' => [
        'elasticsearch' => [
            'class' => 'yii\elasticsearch\Connection',
            'nodes' => [
                ['http_address' => '127.0.0.1:9200'],
                //настройте несколько хостов, если у вас есть кластер
            ],
        ],
    ]
];
```

Соединение поддерживает автоматическое обнаружение кластера Elasticsearch, который включен по умолчанию.
Вам не нужно указывать все узлы кластера вручную, Yii будет обнаруживать другие узлы кластера и подключаться к случайно выбранному узлу по умолчанию. Вы можете отключить эту функцию, установив [[yii\elasticsearch\Connection::$autodetectCluster]] в `false`.

> **NOTE:** для корректной работы автоматического обнаружения кластера, запрос узлов `GET /_nodes` должен возвращать поле `http_address` для каждого узла.
По умолчанию они возвращаются настоящими экземплярами Elasticsearch, но, они недоступны в таких средах как AWS.
В этом случае вам необходимо отключить обнаружение кластера и указать хосты вручную.