---
layout: documentation
class: page-docs page-docs-concepts-registry
title:  "Registries - Documentation Concepts - Cradle"
description: "A registry object contains methods to easily manage a multidimensional arrays"
menu_title: Registry
menu:
  api: API (5)
---
# Registry

A registry object contains methods to easily manage multidimensional arrays.
Ideally registries are designed to organize all sorts of configurations and
works well with JSON objects. Implementing this object can be done like so.

 - [API (5)](#api)

###### Instantiating

```php
use Cradle\Data\Registry;

$registry1 = new Registry;

//or

$registry2 = new Registry(['zoo' => ['foo' => ['bar']]]);
```

<a name="api"></a>
## API

A registry object mounts `ArrayAccessTrait`, `CountableTrait`, `GeneratorTrait`,
`IteratorTrait`, `MagicTrait`, `DotTrait`
*(see [Data Traits](/docs/traits/data.html))* and implements 5 additional methods.

`exists` - Returns true if the data has the given key path or whether
if there is data at all.

```php
$registry1->exists(); //--> false
$registry2->exists(); //--> true

$registry2->exists('zoo'); //--> true
$registry2->exists('zoo', 'foo'); //--> true
$registry2->exists('foo', 'bar'); //--> false
```

----

`get` - Returns part of the data given the key path or the entire data set.

```php
$registry2->get(); //--> ['zoo' => ['foo' => ['bar']]]

$registry2->get('zoo'); //--> ['foo' => ['bar']]
$registry2->get('zoo', 'foo'); //--> ['bar']
$registry2->get('zoo', 'foo', 0); //--> 'bar'
```

----

`isEmpty` - Returns true if the data, given key path is empty or whether
if there is data at all.

```php
$registry1->isEmpty(); //--> true
$registry2->isEmpty(); //--> false

$registry2->isEmpty('zoo'); //--> false
$registry2->isEmpty('zoo', 'foo'); //--> false
$registry2->isEmpty('foo', 'bar'); //--> true
```

----

`remove` - Removes part of the data given the key path or the entire data set.

```php
$registry2->remove('zoo', 'foo', 0); // 'bar'
$registry2->remove('zoo', 'foo'); // ['bar']
$registry2->remove('zoo'); // ['foo' => ['bar']]
$registry2->remove(); // ['zoo' => ['foo' => ['bar']]]

$registry2->remove('foo', 'bar'); // does nothing because it doesn't exist
```

----

`set` - Sets part of the data given the key path or the entire data set.

```php
$registry2->set('zoo', 'foo', 0, 'bar'); // ['zoo' => ['foo' => ['bar']]]
```
