# NoonPaymentsService
Requirement :
Laravel 7.x & 8.x
GuzzleHttp Client

## .env file values 
"Test" for test mode & "Live" for live mode
```php
NOON_PAYMENTS_MODE="Test"
NOON_PAYMENTS_AUTH_KEY="aWJucm9zaGR91jknasdNpdGU6Mjg5MjQxOTM2Mjk3NDZmZWIwY2E0OTYxNzZkZGExMTg="
NOON_PAYMENTS_RETURN_URL="https://localhost/"
NOON_PAYMENTS_CURRENCY="SAR"
NOON_PAYMENTS_CHANNEL="web"
NOON_PAYMENTS_CATEGORY="pay"
NOON_PAYMENTS_LOCALE="ar"
```

## Usage
First Replace all .env value to your own Noon Account values.
to Initiate payment use the following code.
Replace OrderReference with your #Ref ( Example: Invoice Unique ID ).
Replace OrderAmount with Amount ( Example: 50 ).
Replace OrderNameOrDescription with Descriptions  ( Example: Product Nike 12022 ). max:50 char.

```php
$pay = new \App\Providers\NoonPaymentsService('{{ #OrderReference }}','{{ $OrderAmount }}','{{ $OrderNameOrDescription}}');
$result = $pay->INITIATE();
```
