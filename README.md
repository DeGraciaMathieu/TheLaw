# TheLaw
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
