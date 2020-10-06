<?php

namespace App\Providers;

use GuzzleHttp\Client;
use Illuminate\Support\ServiceProvider;

class NoonPaymentsService extends ServiceProvider
{
    private $reference;
    private $amount;
    private $name;

    public function __construct($reference, $amount, $name)
    {
        $this->reference = $reference;
        $this->amount = $amount;
        $this->name = $name;
    }

    public function INITIATE()
    {
        $payment_api = 'https://api.noonpayments.com/payment/v1/order';
        $payment_client = new Client();
        $payment_body = json_encode([
            'apiOperation' => 'INITIATE',

            'order' => [
                'reference' => $this->reference,
                'amount' => number_format($this->amount, 2),
                'currency' => env('NOON_PAYMENTS_CURRENCY','SAR'),
                'name' => substr($this->name, 0, 50),
                'channel' => env('NOON_PAYMENTS_CHANNEL','web'),
                'category' => env('NOON_PAYMENTS_CATEGORY',null)
            ],

            'configuration' => [
                'tokenizeCc' => true,
                'returnUrl' => env('NOON_PAYMENTS_RETURN_URL',null),
                'locale' => env('NOON_PAYMENTS_LOCALE','en')
            ]
        ]);

        $payment_parameter = [
            'headers' =>
                [
                    'Content-Type' => 'application/json',
                    'Authorization' => 'Key_'.env('NOON_PAYMENTS_MODE',null).' '.env('NOON_PAYMENTS_AUTH_KEY',null)
                ],
            'body' => $payment_body,
        ];

        $payment_request = $payment_client->request('POST', $payment_api, $payment_parameter);

        return json_decode($payment_request->getBody()->getContents(), true);;

    }

}
