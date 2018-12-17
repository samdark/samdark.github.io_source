+++
date = "2017-05-13T00:59:27+03:00"
title = "Hydrator"
draft = false
tags = ["php", "hydrator"]
+++

November 2016 I've implemented and released a [Hydrator library](https://github.com/samdark/hydrator) but never properly
announced it. As far as I know, the "hydrator" term was first used in [Hibernate Java ORM](http://hibernate.org/orm/).
The job of a hydrator is to fill an object with data or extract data from an object without calling constructor or extra
getter-setter methods. It allows you to directly work with private properties which should be persisted to database
or loaded from database while not exposing these properties thus keeping public interface clean.

Internally it uses [PHP reflection](http://php.net/manual/en/book.reflection.php).

![](/img/posts/hydration.png)

## Usage

Consider we have a `Post` entity which represents a blog post. It has a title and a text. A unique id is generated to
identify it.

```php
class Post
{
    private $id;
    protected $title;
    protected $text;

    public function __construct($title, $text)
    {
        $this->id = uniqid('post_', true);
        $this->title = $title;
        $this->text = $text;
    }
   
    public function getId()
    {
        return $this->id;
    }
    
    public function getTitle()
    {
        return $this->title;
    }
    
    public function setTitle($title)
    {
        $this->title = $title;
    }
    
    public function getText()
    {
        return $this->text;
    }
    
    public function setText()
    {
        return $this->text;
    }
}
```

Saving a post to database:

```php
$post = new Post('First post', 'Hell, it is a first post.');

$postHydrator = new \samdark\hydrator\Hydrator([
    'id' => 'id',
    'title' => 'title',
    'text' => 'text',
]);

$data = $postHydrator->extract($post);
save_to_database($data);
```

Loading post from database:

```php
<?php
$data = load_from_database();

$postHydrator = new \samdark\hydrator\Hydrator([
    'id' => 'id',
    'title' => 'title',
    'text' => 'text',
]);

$post = $postHydrator->hydrate($data, Post::class);
echo $post->getId();
```

Filling existing post object with data:

```php
$data = load_from_database();

$postHydrator = new \samdark\hydrator\Hydrator([
    'title' => 'title',
    'text' => 'text',
]);

$post = get_post();
$post = $postHydrator->hydrateInto($data, $post);
echo $post->getTitle();
``` 

## Usage in Yii

It's not currently used in Yii in any way. One may use it to implement his own data mapping
in a repository in case of pursuing
[clean architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html)
and [domain driven design](https://en.wikipedia.org/wiki/Domain-driven_design) where encapsulation is uber-important.
