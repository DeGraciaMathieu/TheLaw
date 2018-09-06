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
class Foo {
    
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
    if ($page['private'] && ! Auth::check()) {
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

    if ($page['private'] && ! Auth::check()) {
        return null;
    }
    
    return $page;
}
```
