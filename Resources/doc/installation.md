# Installation

## 1. Install the Bundle

You can add the Bundle by running [Composer](http://getcomposer.org) on your shell or adding it directly to your composer.json

``` bash
php composer.phar require dzunke/slack-bundle:dev-master
```

``` json
"require" :  {
    "dzunke/slack-bundle": "dev-master"
}
```

## 2. Register the Bundle to Symfony

The Namespace will be registered by autoloading with Composer but to use the integrated features for symfony you have to register the Bundle.

### Symfony 3
``` php
# app/AppKernel.php
public function registerBundles()
{
    $bundles = [
        // [..]
        new DZunke\SlackBundle\DZunkeSlackBundle(),
    ];
}
```

### Symfony 4 Flex
``` php
# config/bundles.php
# NOTE: Normally this is automatic, this may already be done for you
return [
    ...
    DZunke\SlackBundle\DZunkeSlackBundle::class => ['all' => true],
    ...
];
```

## 3. Add the Configuration for the Bundle

To use the Bundle without an Error you have to add the Connection-Data and finally one Identity to use with the Methods like MonologHandler or Messaging.

### Symfony 3
``` yaml
# app/config/config.yml
d_zunke_slack:
    token: "YOUR AUTH-TOKEN"
    identities:
        CoffeeBrewer: ~
```

### Symfony 4 Flex config
``` yaml
# config/packages/d_dunke_slack.yaml
d_zunke_slack:
    endpoint: slack.com/api/
    token: '%env(resolve:d_zunke_slack_api_tkn)%' # Required
    verify_ssl: true # ssl verification at guzzle client
    use_http_post: false # give the ability to send request as HTTP POST
    # The amount of retries for the connection if the Rate Limits of Slack are reached
    limit_retries: 3
    # Usernames to use for Communication inside the Messaging
    identities:
        # Prototype
        username:
            # An Url to a specific picture to use as Icon
            icon_url:             null
            # The Icon to use from an emoji like :smile:
            icon_emoji:           null
```

### Symfony 4 Flex Environment Variables file
``` 
# .env
...
###> dzunke/d_zunke_slack ###
d_zunke_slack_api_tkn=XXXXXXXX
###< dzunke/d_zunke_slack ###
...
```
