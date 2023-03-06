---
title: "Laravel9から10にupgradeしてみる"
emoji: "🍣"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Laravel", "PHP", "初心者"]
published: true
---

Laravelの新しいバージョンがリリースされましたね！
https://laravel-news.com/laravel-10

手元に何もしていないLaravel9のプロジェクトがあったので、公式にしたがってupgradeしてみました

https://laravel.com/docs/10.x/upgrade

まずは現在のPHPのバージョン確認

```php
$ php -v
PHP 8.1.14 (cli) (built: Jan 11 2023 07:57:04) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.14, Copyright (c) Zend Technologies
    with Xdebug v3.2.0, Copyright (c) 2002-2022, by Derick Rethans

```

Laravelのバージョンも確認

```php
$ php artisan -V 
Laravel Framework 9.48.0
```

アップグレードガイドによると、PHPのver8.1以上のようなのでこの辺は行けそうですね
> PHP 8.1.0 Required
> Laravel now requires PHP 8.1.0 or greater.

composerのバージョンも確認

```php
$ composer -v
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 2.5.1 2022-12-22 15:33:54
```

2.2以上ということでここも問題なさそうですね

> Composer 2.2.0 Required
> Laravel now requires Composer 2.2.0 or greater.

composer.jsonを編集します

```jsx
{
    "name": "laravel/laravel",
    "type": "project",
    "description": "The Laravel Framework.",
    "keywords": ["framework", "laravel"],
    "license": "MIT",
    "require": {
        "php": "^8.1", // 変更
        "guzzlehttp/guzzle": "^7.2",
        "laravel/framework": "^10.0",　// 変更
        "laravel/sanctum": "^3.2",　// 変更
        "laravel/tinker": "^2.7"
    },
    "require-dev": {
        "fakerphp/faker": "^1.9.1",
        "laravel/pint": "^1.0",
        "laravel/sail": "^1.0.1",
        "mockery/mockery": "^1.4.4",
        "nunomaduro/collision": "^7.1",// 変更
        "phpunit/phpunit": "^10.0",　// 変更
        "spatie/laravel-ignition": "^2.0"
    },
    "autoload": {
        "psr-4": {
            "App\\": "app/",
            "Database\\Factories\\": "database/factories/",
            "Database\\Seeders\\": "database/seeders/"
        }
    },
    "autoload-dev": {
        "psr-4": {
            "Tests\\": "tests/"
        }
    },
    "scripts": {
        "post-autoload-dump": [
            "Illuminate\\Foundation\\ComposerScripts::postAutoloadDump",
            "@php artisan package:discover --ansi"
        ],
        "post-update-cmd": [
            "@php artisan vendor:publish --tag=laravel-assets --ansi --force"
        ],
        "post-root-package-install": [
            "@php -r \"file_exists('.env') || copy('.env.example', '.env');\""
        ],
        "post-create-project-cmd": [
            "@php artisan key:generate --ansi"
        ]
    },
    "extra": {
        "laravel": {
            "dont-discover": []
        }
    },
    "config": {
        "optimize-autoloader": true,
        "preferred-install": "dist",
        "sort-packages": true,
        "allow-plugins": {
            "pestphp/pest-plugin": true
        }
    },
    "minimum-stability": "stable",
    "prefer-stable": true
}
```

いざupgradeする！

```php
$ composer update
Loading composer repositories with package information
Info from https://repo.packagist.org: #StandWithUkraine
Updating dependencies
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - Root composer.json requires nunomaduro/collision ^7.1, found nunomaduro/collision[v7.x-dev] but it does not match your minimum-stability.

Use the option --with-all-dependencies (-W) to allow upgrades, downgrades and removals for packages currently locked to specific versions.
```

怒られましたね…よくみたらバージョンの指定を間違えていたようです。

> **`nunomaduro/collision`** to **`^7.0`**

再チャレンジ！

```php
$ composer update

INFO  Discovering packages.  

  laravel/sail ............................................................................. DONE
  laravel/sanctum .......................................................................... DONE
  laravel/tinker ........................................................................... DONE
  nesbot/carbon ............................................................................ DONE
  nunomaduro/collision ..................................................................... DONE
  nunomaduro/termwind ...................................................................... DONE
  spatie/laravel-ignition .................................................................. DONE

80 packages you are using are looking for funding.
Use the `composer fund` command to find out more!
> @php artisan vendor:publish --tag=laravel-assets --ansi --force

   INFO  No publishable resources for tag [laravel-assets].  

No security vulnerability advisories found
```

行けましたね！

```php
$ php artisan -V 
Laravel Framework 10.1.1
```

今回初めて自分でupgradeしてみましたが、さすがに何もしていないのでサクッと行けました。
でもやっぱり緊張しますね！