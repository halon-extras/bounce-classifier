# Halon Bounce Classifier client

This plugin will query the [bounce-classifier](https://docs.halon.io/bounce-classifier/) service. It uses a internal cache of the normalized message.

## Installation

Follow the [instructions](https://docs.halon.io/manual/comp_install.html#installation) in our manual to add our package repository and then run the below command.

### Ubuntu

```
apt-get install halon-extras-bounce-classifier
```

### RHEL

```
yum install halon-extras-bounce-classifier
```

## Exported functions

These functions needs to be [imported](https://docs.halon.io/hsl/structures.html#import) from the `extras://bounce-classifier` module path.

### bounce_classifier(message[, url[, options]])

Classify a bounce message.

**Params**

- message `string` - The bounce message to classify
- url `string` - The URL of the bounce classfier endpoint. The default is ``http://127.0.0.1:8000/v1/bnac/single``
- options `array` - Options array

The following options are available in the **options** array.

- http_background `string` - If configured it will use this ``halon-extras-http-background`` profile. If not the regular (blocking) ``http`` function will be used.
- http_options `array` - Additional ``http`` function options.
- cache_size `number` - The cache size. The default is `65536` (LRU).
- cache_ttl_good `number` or `none` - The cache TTL for successful lookups. The default is `none` (no TTL expiration).
- cache_ttl_bad `number` - The cache TTL for failed lookups. The default is `30`.

**Returns** The classifier result (JSON) or none on errors 

**Example**

```
import { bounce_classifier } from "extras://bounce-classifier";

echo bounce_classifier("451 4.7.1 <bla.candy@fish.sk>: Recipient address rejected: Greylisting in effect, please come back later");
```