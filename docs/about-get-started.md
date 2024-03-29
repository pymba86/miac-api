# Начало работы

## Установка библиотеки в проект
 
Прежде чем пытаться установить библиотеку, проверьте свою конфигурацию PHP:

 - Минимальная версия PHP - 5.4.
 - Следующие расширения PHP должны быть активированы: SOAP, DOM, XSL.
 
 Установите клиентскую библиотеку в своем PHP-проекте, для чего требуется пакет с Composer:
 
 ``composer require pymba86/miac-api``
 
## Настройте клиент

#### Список доступных клиентов:

- PortalClient : Сервис портала по приему данных от МО
- NsiClient : Сервис НСИ

Пример настройки клиента(PortalClient):

```php
<?php

use Miac\PortalClient;
use Miac\Client\Params;
use Miac\Client\Result;
use Miac\Client\RequestOptions\GetActualSpecialistListOptions;

//Настройка клиента с необходимыми параметрами:

$params = new Params([
    'sessionHandlerParams' => [
        'wsdl' => '', // Указывает на местоположение файла WSDL
        'stateful' => true, //Включить сообщения о состоянии по умолчанию
    ],
    'requestCreatorParams' => []
]);

$client = new PortalClient($params);

$result = $client->getActualSpecialistList(new GetActualSpecialistListOptions([
    'muCode' => '19123'
]));

if ($result->status === Result::STATUS_OK) {
    echo "Успешно получен список специалистов!";
    echo "Получена стока XML: <pre>" . $result->responseXml . "</pre>";
}
  ``` 

## Тестирование клиента без сервера

```php
<?php

use Miac\Client\Params;
use Miac\Client\Result;

//Настройка клиента для тестирование без запросов на сервер:

$params = new Params([
    'sessionHandlerParams' => [
        'wsdl' => '', // Указывает на местоположение файла WSDL
        'stateful' => true, //Включить сообщения о состоянии по умолчанию
        'dummy' => true //Включить заглушки
    ],
    'requestCreatorParams' => []
]);

  ``` 

## Настройка подключения через прокси сервер

```php
<?php

use Miac\Client\Params;
use Miac\Client\Result;

//Настройка клиента для тестирование без запросов на сервер:

$params = new Params([
            'sessionHandlerParams' => [
                'wsdl' => "",
                'stateful' => true,
                'soapClientOptions' => [
                    'proxy_host' => "127.0.0.1",
                    'proxy_port' => "44555"
                ]
            ],
            'requestCreatorParams' => []
        ]);

  ``` 
  
## Поддерживаемые сообщения

Смотрите [список поддерживаемых сообщений](list-of-supported-messages.md)

## Примеры сообщений

Смотрите [список примеров, как отправлять конкретные сообщения](samples.md)