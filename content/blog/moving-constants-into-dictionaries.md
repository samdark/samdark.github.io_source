+++
date = "2017-06-02T03:03:04+03:00"
title = "Moving constants into dictionaries"
draft=false
tags=["php", "refactoring", "constants"]
+++

Extracting constants makes code much cleaner compared to using values directly. It eliminates typos and makes it possible
to use IDE autocomplete and refactoring.
 
Typically, after extraction is done, it looks like the following:

```php
namespace app\models;

class User
{
    const GENDER_FEMALE = 'female';
    const GENDER_MALE = 'male';
    
    public static function listGenders()
    {
        return [
            self::GENDER_FEMALE => Yii::t('app', 'Female'),
            self::GENDER_MALE => Yii::t('app', 'Male'),
        ];
    }
    
    public static function getGenderAsString($gender)
    {
        $all = self::listGenders();

        if (isset($all[$gender])) {
            return $all[$gender];
        }

        return Yii::t('app', 'Not set');
    }
    
    // ...
}
```

or another example from Stay.com project:

```php
namespace app\models;

class Guide
{
    const THEME_SHOPPING = 2;
    const THEME_ART_AND_CULTURE = 3;
    const THEME_AFTER_DARK = 4;
    const THEME_FAMILY = 5;
    const THEME_COFFEE = 8;
    const THEME_ON_A_BUDGET = 9;
    const THEME_FOOD = 10;
    const THEME_SPORTS_AND_OUTDOORS = 11;
    const THEME_24_HOURS = 12;
    
    public static function listThemes()
    {
        return [
            self::THEME_SHOPPING => Yii::t('app', 'Shopping'),
            // ...
        ];
    }
    
    public static function getThemeAsString($theme)
    {
        $all = self::listThemes();

        if (isset($all[$theme])) {
            return $all[$theme];
        }

        return Yii::t('app', 'Not set');
    }
    
    // ...
}
```

It is more or less OK but some issues are still there:

1. It bloats the class.
2. Constants could not be reused in different context.
3. It creates unnecessary dependency when used with different classes such as form models.

In both examples above it's possible to extract constants into its own class. User case:

```php
namespace app\dictionaries;

abstract class Gender
{
    const FEMALE = 0;
    const MALE = 1;

    public static function all()
    {
        return [
            self::MALE => Yii::t('app', 'Male'),
            self::FEMALE => Yii::t('app', 'Female'),
        ];
    }
    
    public static function get($gender)
    {
        $all = self::all();

        if (isset($all[$gender])) {
            return $all[$gender];
        }

        return Yii::t('app', 'Not set');
    }
}
```

Stay.com case:

```php
namespace app\dictionaries;

abstract class GuideTheme
{
    const SHOPPING = 2;
    const ART_AND_CULTURE = 3;
    const AFTER_DARK = 4;
    const FAMILY = 5;
    const COFFEE = 8;
    const ON_A_BUDGET = 9;
    const FOOD = 10;
    const SPORTS_AND_OUTDOORS = 11;
    const 24_HOURS = 12;
    
    public static function all()
    {
        return [
            self::SHOPPING => Yii::t('app', 'Shopping'),
            // ...
        ];
    }
    
    public static function get($theme)
    {
        $all = self::all();

        if (isset($all[$theme])) {
            return $all[$theme];
        }

        return Yii::t('app', 'Not set');
    }    
}
```

In both cases, additionally to solving issues listed above, it looks either equally good or better than originally:

```php
$user->gender = Gender::MALE;
// instead of
$user->gender = User::GENDER_MALE;


$guide->theme = GuideTheme::COFFEE;
// instead of
$guide->theme = Guide::THEME_COFFEE;
```
