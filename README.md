# yii2-ensure-unique-behavior

[![Latest Stable Version](https://poser.pugx.org/jamband/yii2-ensure-unique-behavior/v/stable)](https://packagist.org/packages/jamband/yii2-ensure-unique-behavior) [![Total Downloads](https://poser.pugx.org/jamband/yii2-ensure-unique-behavior/downloads)](https://packagist.org/packages/jamband/yii2-ensure-unique-behavior) [![Latest Unstable Version](https://poser.pugx.org/jamband/yii2-ensure-unique-behavior/v/unstable)](https://packagist.org/packages/jamband/yii2-ensure-unique-behavior) [![License](https://poser.pugx.org/jamband/yii2-ensure-unique-behavior/license)](https://packagist.org/packages/jamband/yii2-ensure-unique-behavior) [![Build Status](https://travis-ci.org/jamband/yii2-ensure-unique-behavior.svg?branch=master)](https://travis-ci.org/jamband/yii2-ensure-unique-behavior)
This extension insert unique identifier automatically for the Yii 2 framework.

## Requirements

* PHP 5.5+
* Yii 2.x

## Installation

```
php composer.phar require --prefer-dist jamband/yii2-ensure-unique-behavior "*"
```

or add in composer.json (require section)
```
"jamband/yii2-ensure-unique-behavior": "*"
```

## Examples

Creates a post table:

```sql
CREATE TABLE `post` (
    `id` CHAR(11) NOT NULL,
    `title` VARCHAR(255) NOT NULL,
    `content` TEXT NOT NULL,
    `created_at` INT(11) NOT NULL,
    `updated_at` INT(11) NOT NULL,
    PRIMARY KEY (`id`)
) ENGINE=InnoDB CHARACTER SET=utf8 COLLATE=utf8_unicode_ci;
```

Settings EnsureUniqueBehavior in Model:

```php
<?php

namespace app\models;

use jamband\behaviors\EnsureUniqueBehavior;
use yii\behaviors\TimestampBehavior;
use yii\db\ActiveRecord;

class Post extends ActiveRecord
{
    public function behaviors()
    {
        return [
            TimestampBehavior::class,
            [
                'class' => EnsureUniqueBehavior::class,
                'attribute' => 'id', // default
                'length' => 11, // default
            ],
        ];
    }
}
```

And saves a new model:

```php
<?php

$model = new \app\models\Post();
$model->title = 'title';
$model->content = 'content';
$model->save();

// This values is eusure uniqueness.
var_dump($model->id); // string(11) "-ZRLSS-4vl_"
```

## License

This extension is licensed under the MIT license.
