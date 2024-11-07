---
title: Howto grab a domain that has been deleted
date: 2024-08-13
tags: [domains]
---

# gTLD lifecycle

![gTLD lifecycle](/img/gtld-lifecycle.jpg)
(source: [ICANN](https://archive.icann.org/en/registrars/gtld-lifecycle.jpg)

As you are probably aware of, a typical gTLD or nTLD domain runs through multiple phases after it's expiration date. The last of which is the pendingDelete status which typically lasts 5 days.

If you are serious about getting a domain, it is these very 5 days on which you should become active. (at latest).

Since I still have a reseller account with [1blu business GmbH](https://1blu-business.de/), I'm going to illustrate howto setup a cronjob for their domain robot. The steps required to set this up, will varry quite a bit.

# Code sample

```php {linenos=table,anchorlinenos=true}
<?php

require 'vendor/autoload.php';
$client = new GuzzleHttp\Client(['base_uri' => 'https://service.partner4trade.de/live/domain.svc/rest/']);

if (!file_exists(__DIR__ . "/register.lock")) {
    $response0 = $client->request('POST', 'DomainAvailable', ['json' => [
        'Transaction' => [
            'Username' => 'USERNAME',
            'Password' => 'PASSWORD!!!!!',
            'TargetAccount' => 'Accountnummer',
            'ClientTransactionId' => 'randoTransactionID'
        ],
        'Domain' => 'domain.tld'
    ]]);
    $domain_status = json_decode($response0->getBody())->Status;

    if ($domain_status != 0) {
        echo "domain not free! Status: " . $domain_status . "\n";
    } else {
        $response1 = $client->request('POST', 'DomainRegister', ['json' => [
            'Transaction' => [
                'Username' => 'USERNAME',
                'Password' => 'PASSWORD',
                'TargetAccount' => 'Accountnummer',
                'ClientTransactionId' => 'randoTransactionsID2'
            ],
            'Contact0' => 'HANDLE-ID',
            'Contact1' => 'HANDLE-ID',
            'Contact2' => 'HANDLE-ID',
            'Contact3' => 'HANDLE-ID',
            'Domain' => 'domain.tld',
            'Nameserver' => [
                ['Name' => 'ns1.nameserver.tld'],
                ['Name' => 'ns2.nameserver.tld']
            ]
        ]]);

        echo $response1->getBody();
        touch(__DIR__ . "/register.lock");
    }
} else echo "lockfile exists - domain registered hopefully";

```

## What does it do?

1. it requires an external dependency called GuzzleHttp which needs to be installed with `composer` prior to running
2. In the outer if we check if there is no lock file present and only then continue
3. we then do a DomainAvailability check on the domain and depending on the status (0 = Available) continue
4. If the status != 0 we give a message and stop execution
5. else we perform the Registration attempt
6. in the end we close the outer if with a message that a lockfile exists.

## Howto install it

You will need SSH access to your webserver in order to run these steps

1. create a empty directory to store the script
2. install composer: `curl -sS https://getcomposer.org/installer | php`
3. install Guzzle in your folder: `composer require guzzlehttp/guzzle:^7.0`
4. copy&paste the above script with the `$EDITOR` of your choice in a file named `register.php`
5. Create a cronjob with `crontab -e`
6. Include the following 2 lines:

```bash
MAILTO=your.mail@provider.tld
* * * * * php -f /root/folder/register.php
```

## Why Availability check?

You can decide that for your self. For me each registration attempt comes with an email from the 1blu domain robot which I guess my account manager also gets. In order to not fall under API abuse, I rather perform this extra step.

## Optimizations

Currently the script send an email per minute which can be a bit problematic if they end up in your phone notifications. To reduce the noise, you could use `fwrite(STDERR, "message");` to write the output of the registration attempt and for the cron redirect `STDOUT` to `/dev/zero`.
