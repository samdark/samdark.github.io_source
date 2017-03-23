+++
date = "2017-03-23T11:41:26+03:00"
title = "bcrypt hash"
+++

bcrypt is a good way to deal with password authentication. In PHP it is available via
[crypt](https://secure.php.net/manual/en/function.crypt.php) with blowfish algorithm or a shortcut
[password_hash](https://secure.php.net/manual/en/function.password-hash.php) function current PHP versions are providing.

Yii framework project templates are using bcrypt for handling passwords. Framework components
are [providing polyfills ensuring bcrypt is used correctly](http://www.yiiframework.com/doc-2.0/yii-base-security.html#generatePasswordHash()-detail).
 
bcrypt produces a compound hash that looks like the following:

$<strong style="color: #f00">2y</strong>$<strong style="color: #0a0">13</strong>$<strong style="color: #00f">YUUgrko03UmNU/fe6gNcO.</strong><strong style="color: #00a">Hka4lrdRlkq0iJ5d4bv4fK.sKS.6jXu</strong>

The string is always 60 characters long.

- <strong style="color: #f00">2y</strong> indicates algorithm. We are using blowfish so in current PHP versions it should
  always be `2y`.
- <strong style="color: #0a0">13</strong> is computation cost. 2^13 iterations of [key derivation function](https://en.wikipedia.org/wiki/Key_derivation_function).
- Rest of the string is concatenated salt, and hash encoded with base64 with a custom set of characters.
  First 22 symbols are <strong style="color: #00f">16 bytes salt</strong>. The rest are <strong style="color: #00a">the hash itself</strong>.

When verifying a password input bcrypt extract algorithm version, cost, salt and hash from compound hash string of
a saved password. Then, using the data extracted, it calculates a hash of the input and compares it with the hash
we store.
