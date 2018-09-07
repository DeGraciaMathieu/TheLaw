<p align='center'>
  <img src='https://i1.wp.com/blog.degracia-mathieu.fr/wp-content/uploads/2018/05/ezgif.com-gif-maker.gif?zoom=0.8999999761581421&resize=500%2C211&ssl=1'>  
</p>

# TheLaw :boom:

## Structure d'une class
```php
# bad
class Foo {
    public function bar($var){
        //
    }
}
```
```php
# good
class Foo 
{    
    /**
     * Description
     * @param string $var
     * @throws \Full\Namespace\Exception
     * @return \Full\Namespace
     */
    public function bar() 
    {
        //
    }
}
```
## Organiser les namespaces 
```php
# bad
use My\Long\Ordened;
use My;
use My\Long\Ordened\Namespace;
use My\Long;
```
```php
# good
use My;
use My\Long;
use My\Long\Ordened;
use My\Long\Ordened\Namespace;
```
## Garder un code propre et aérer 
```php
# bad
public function getPage($url)
{
    $page = $this->pages()->where('slug', $url)->first();
    if (! $page) {
        return null;
    }
    if ($page['private'] && Auth::guest()) {
        return null;
    }
    return $page;
}
```
```php
# good
public function getPage($url)
{
    $page = $this->pages()->where('slug', $url)->first();

    if (! $page) {
        return null;
    }

    if ($page['private'] && Auth::guest()) {
        return null;
    }
    
    return $page;
}
```
## Ne jamais utiliser les structures simplifiées
```php
# bad
if (! $page)
    return null;
```
```php
# good
if (! $page) {
    return null;
}
```
## Attention à l'utilisation de la négation
```php
# bad
$dontDoIt = true;

if (! $dontDoIt) {
    //
}
```
```php
# good
$doIt = true;

if ($doIt) {
    //
}
```
## Diminuer l'imbriquation du code
```php
# bad
if (condition_1) {
    
    // foo

    if (condition_2) {
        return;
    }
    else {
        // foo
    }
}
else {
    return;
}
```
```php
# good
if (! condition_1) {
    return;
}

// foo

if (condition_2) {
    return;
}

// foo
```
## Limiter l'utilisation des flags
```php
# bad
function createFile($tmp = true)
{
    if ($temp) {
        // foo
    }
    else {
        // foo
    }
}
```
```php
# good
function createFile()
{
    //
}

function createTempFile()
{
    //
}
```
## Pas de cachet sur les classes
```php
# bad
/**
 * Created by PhpStorm.
 * User: Owen Grady
 * Date: 20/10/2018
 */
class RaptorPaddock
{
    ///
}
```
```php
# good
class RaptorPaddock
{
    ///
}
```
