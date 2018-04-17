+++
date = "2017-04-17T13:49:29+03:00"
title = "Are traits evil?"
draft = false
tags = ["php", "trait", "yii"]
+++

When I have started [a Patreon campaign](https://www.patreon.com/samdark), I have promised to answer questions.
First question came from Daniel Fly and is about [PHP traits](http://php.net/manual/en/language.oop5.traits.php):

> What do you think about Traits in PHP? Do you think they are evil and should avoid using them? If using them what
  are some common pitfalls fx where not to use them? Maybe you got some bad or good experience?

## What are traits?

PHP manual defines traits as the following:

> Traits are a mechanism for code reuse in single inheritance languages such as PHP. A Trait is intended to reduce some
> limitations of single inheritance by enabling a developer to reuse sets of methods freely in several independent
> classes living in different class hierarchies. The semantics of the combination of Traits and classes is defined
> in a way which reduces complexity, and avoids the typical problems associated with multiple inheritance and Mixins.
>  
> A Trait is similar to a class, but only intended to group functionality in a fine-grained and consistent way. It is
> not possible to instantiate a Trait on its own. It is an addition to traditional inheritance and enables horizontal
> composition of behavior; that is, the application of class members without requiring inheritance.

That is a way lengthy description. In simple words, if we are not touching inheritance aspect, traits are an enhanced way
to copy-paste.

```php
<?php
trait Dumper
{
    public function dump($var)
    {
        echo '<pre>' . print_r($var, true) . '</pre>';
    }
}
 
class MyClass
{
    use Dumper;
}
 
$myClass = new MyClass();
$myClass->dump('test');
```

The code above would work similar to:

```php
<?php
class MyClass
{
    public function dump($var)
    {
        echo '<pre>' . print_r($var, true) . '</pre>';
    }
}
```

## Traits and Yii

Yii uses traits for low level functionality and common database layer code. Traits were considered to be used for
behaviors in 2.0 and will be considered again for 2.1.

### Behaviors

I have started looking at traits in [August 2010](https://rmcreative.ru/blog/post/traits-v-trunk-php) when they were merged
into PHP `trunk` (that is how `master` was called in CVS/SVN). By that time Yii 1.x had behaviors concept which is similar
to Ruby mixins and is handy for seamlessly adding extra abilities such as `SoftDeleteable` or `Versionable` to
a class. The main difference is that behavior has its own state and could be attached/detached in runtime while trait
has no own state at all.

Traits were released before Yii 2.0 so when designing it we considered using them instead of 1.1 behaviors and decided
not to. At that time there were no good ideas on how to make trait powered behavior configurable and
attachable/detachable at runtime.

For 2.1 the idea popped up again. We have found ways to solve configurability by using abstract methods.
Attaching/detaching proved to be unsolvable but enabling/disabling via subscribing and unsubscribing to/from events is
possible. Final decision is still to be made...

### Low level functionality

Yii uses traits for common low level functionality:

- [ArrayableTrait](https://github.com/yiisoft/yii2/blob/master/framework/base/ArrayableTrait.php)
- [ArrayAccessTrait](https://github.com/yiisoft/yii2/blob/master/framework/base/ArrayAccessTrait.php)

That is the most straightforward and correct use for traits.

### Database layer common code

A bit less straightforward is use of traits in Yii's database layer:

- [ActiveQueryTrait](https://github.com/yiisoft/yii2/blob/master/framework/db/ActiveQueryTrait.php)
- [ActiveRelationTrait](https://github.com/yiisoft/yii2/blob/master/framework/db/ActiveRelationTrait.php)
- [QueryTrait](https://github.com/yiisoft/yii2/blob/master/framework/db/QueryTrait.php)
- [SchemaBuilderTrait](https://github.com/yiisoft/yii2/blob/master/framework/db/SchemaBuilderTrait.php)
- [ViewFinderTrait](https://github.com/yiisoft/yii2/blob/master/framework/db/ViewFinderTrait.php)

Database layer in Yii 2.0 has the same interface for both relational databases and noSQLs.
Common parts in interface implementations are extracted into traits to keep inheritance tree
smaller and to be able not to override too many methods for noSQLs which are different from traditional databases.

Personally I am not happy with this implementation looking from pure object-oriented perspective.
It could have been done using composition and normal classes to be more testable and easier to read. Still, traits usage
is justifiable because it saves tons of method calls thus making database layer significantly faster. Additionally,
we dealt with testing it despite it not being straightforward.

## Common pitfalls

When you think about using a trait, think twice.

### No encapsulation

When using traits, you should understand the copy-paste aspect of it. Everything inside the trait is magically copied
to the class as is. Of course, you can deal with naming conflicts when using a trait but that does not change the fact
much. Because of that, it is wise to keep amount of code a trait contains to the minimum.

Ideal usage of traits is about small and simple pieces of code.

### State

Since traits lack proper encapsulation, in order to deal with state you either should add private properties to
the trait or declare `static` variables inside a method. Both could lead to issues.

Private properties are copied to the class using a trait. Possible issues are naming conflicts and accidental
modification of the property. Because in runtime properties are copied into class, class has access to private ones.

Using `static` means all your objects using a trait would share the same state which is not always desired.  

## Are traits evil?

Short answer: depending on how you use traits.

Same as copy-paste they are evil to some degree but there is nothing absolutely evil or absolutely good.

Traits are useful for reusable interface implementations without the need for a base class. In other cases it is
better to stick with objects composition.

## Further reading

- [Using Traits in PHP 5.4](https://www.sitepoint.com/using-traits-in-php-5-4/)
- [PHP Traits: Good or Bad?](https://www.sitepoint.com/php-traits-good-or-bad/)
- [How I Use Traits](http://rosstuck.com/how-i-use-traits/)
- [Comments for this very post at reddit](https://www.reddit.com/r/PHP/comments/65uyv3/are_traits_evil/)
