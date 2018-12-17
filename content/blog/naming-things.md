+++
date = "2018-12-16T18:46:23+03:00"
title = "Naming things"
draft = false
+++

> There are only two hard things in Computer Science: cache invalidation
> and naming things.
>
> -- <cite>Phil Karlton</cite>

We, developers, spend more time reading code than writing it.
It is important for the code to be readable and clear about its intent.

Below are some advice based on my experience naming things.

# Meaning

A name, be it a variable, a property, a class, or an interface, should reflect
the purpose of why it's being introduced and how it's used.

## Use accurate names

If one can not get an idea about usage and purpose without extra comments
the name is not good enough. If immediate usage or purpose
idea based on naming is wrong then the naming is unacceptable.

The worst possible naming is when a method name lies to the one who reads it.

## Avoid meaningless names

These are names like `$i`, `$j`, `$k` etc. While these are OK to use in cycles,
in other cases they are wasting readability.

A common source of such names is classic science where most formulas use
one-letter variables so it is faster to write. As a consequence, you can not
make sense of these formulas without an introductory paragraph explaining
naming. Often this paragraph is hard to find.

Since computer science education includes significant number of classic science
disciplines, students are getting used to such naming and bring it to programming.

## Naming classes, interfaces, properties and methods

Class name should be one or several nouns. There should be no verbs.
Try avoiding "data", "manager", "info", "processor", "handler", "maker",
"util" etc. as these usually an indicator of vague naming.

Interfaces are usually either nouns or adjectives. Some teams, including
[PHP-FIG](https://www.php-fig.org/), chose to postfix interfaces with `Interface`.
Some do it with `I` prefix and some use no prefix or postfix. I find
all these acceptable in case you are consistent.

Properties should be named with nouns or adjectives. For booleans use affirmative
phrases prefixing with "Is", "Can", or "Has" where appropriate.

Method names should contain one or more verbs as they are actions. Choose verb
that describes what the method does, not how it does it.

While it is not strictly necessary, it is a good idea to end derived
class name with the name of the base class:

```php
class Exception {}

class InvalidArgumentException extends Exception {}
```

# Consistency

Use a single name for a single concept. Be consistent.

A good example is using `begin`/`end` everywhere instead of mixing it with `start`/`finish`.

## Follow code style conventions

When developing a project, a team must agree on code style and naming conventions
they use and follow these. If a part of conventions is not accepted by
some team members then it should be reviewed, changed and new rule should be set.

For PHP the most common convention is currently PSR-2 and most internal project
conventions are based on it.

# Verbosity

## Avoid reusing names

Using same name for many concepts should be avoided if possible as it brings
two problems:

- When reading, you have to keep context in mind. Usually that means getting to
  namespace or package declaration constantly.
- Searching for such names is a pain.

## Avoid contractions

Do not use contractions. Common examples are:

- `cnt`
- `iter`
- `amnt`
- `impl`

```php
function cntBigWrds($data, $length)
{
    $i = 0;
    foreach ($data as $iter) {
        if (mb_strlen($iter) > $length) {
            $i++;
        }
    }
    return $i;
}

$data = ['I', 'am', 'word'];
echo cntBigWrds($data, 3);
```

The code above when named properly becomes:

```php
function countWordsLongerThan(array $words, int $minimumLength)
{
    $count = 0;
    foreach ($words as $word) {
        if (mb_strlen($word) > $minimumLength) {
            $count++;
        }
    }
    return $count;
}

$words = ['I', 'am', 'word'];
echo countWordsLongerThan($words, 3);
```

Note still that short explanatory names without contractions are better than
long explanatory names so do not take verbosity to extreme ending up with names
like `processTextReplacingMoreThanASingleSpaceWithASingleSpace()`.

If the name is too long it either means it could be re-worded to make it shorter
or the thing you are naming is doing too much and should be refactored into
multiple things.

## Avoid acronyms

Avoid acronyms and abbreviations except commonly known ones such as HTML. [Elon Musk](https://en.wikipedia.org/wiki/Elon_Musk) sent an email titled
"Acronyms Seriously Suck" to all SpaceX employees in May 2010:

> There is a creeping tendency to use made up acronyms at SpaceX. Excessive use of made up acronyms is a significant impediment to communication and keeping communication good as we grow is incredibly important. Individually, a few acronyms here and there may not seem so bad, but if a thousand people are making these up, over time the result will be a huge glossary that we have to issue to new employees. No one can actually remember all these acronyms and people don't want to seem dumb in a meeting, so they just sit there in ignorance. This is particularly tough on new employees.
>
> That needs to stop immediately or I will take drastic action - I have given enough warning over the years. Unless an acronym is approved by me, it should not enter the SpaceX glossary. If there is an existing acronym that cannot reasonably be justified, it should be eliminated, as I have requested in the past.
>
> For example, there should be not "HTS" [horizontal test stand] or "VTS" [vertical test stand] designations for test stands. Those are particularly dumb, as they contain unnecessary words. A "stand" at our test site is obviously a test stand. VTS-3 is four syllables compared with "Tripod", which is two, so the bloody acronym version actually takes longer to say than the name!
>
> The key test for an acronym is to ask whether it helps or hurts communication. An acronym that most engineers outside of SpaceX already know, such as GUI, is fine to use. It is also ok to make up a few acronyms/contractions every now and again, assuming I have approved them, e.g. MVac and M9 instead of Merlin 1C-Vacuum or Merlin 1C-Sea Level, but those need to be kept to a minimum.

I agree with him.

# Readability

Code should be able to be read as easily as prose. Choose words that you would
choose writing an article or a book. For example, a property named
`TotalAmount` is more readable in English than `AmountTotal`.

## Hiding implementation details

That is more about object oriented design but it affects readability much if
implementation details are exposed. Try not to expose methods named like:

- `initialize`
- `init`
- `create`
- `build`

## Domain language

Code should use the same names as used in the business or domain model automated.

For example, if a travel business using "venue" as a general name for cafes,
hotels and tourist attractions, it is a bad idea to use "place" in the code
because you and your users will speak two different languages making it more complicated than it should.

Such a language is often called "The Ubiquitous Language". You can learn more from
"[Domain Driven Design Quickly](https://www.infoq.com/minibooks/domain-driven-design-quickly)"
mini-book by InfoQ.

## English

Majority of programming languages use English for built-in constructs and it is
a good practice to name things in English as well. It is extremely important
for a developer to learn English at least on the basic level and,
what is more important, to have good vocabulary that one can use for
finding a good name.

Some useful tools:

- [thesaurus.com](http://www.thesaurus.com/) - for finding synonyms.
- [wordassociations.net](https://wordassociations.net/en) - for finding associations.

# References

- [Microsoft Guidelines for Names](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/ms229002(v%3dvs.100))
- [TwoHardThings by Martin Fowler](https://martinfowler.com/bliki/TwoHardThings.html)
- [Domain Driven Design Quickly by InfoQ](https://www.infoq.com/minibooks/domain-driven-design-quickly)