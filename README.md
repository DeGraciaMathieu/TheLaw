![...](https://i1.wp.com/blog.degracia-mathieu.fr/wp-content/uploads/2018/05/ezgif.com-gif-maker.gif?zoom=0.8999999761581421&resize=500%2C211&ssl=1)

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
## Ne jamais utiliser les structures simplifiées
```php
# bad
if (! $page) {
    return null;
if ($page['private'] && ! Auth::check()) {
    return null;
```
```php
# good
if (! $page) {
    return null;
}

if ($page['private'] && ! Auth::check()) {
    return null;
}
```
