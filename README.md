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
    } else {
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
    if ($tmp) {
        // foo
    } else {
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
    //
}
```
```php
# good
class RaptorPaddock
{
    //
}
```
## Toutes les classes en dehors du namespace courant doivent se trouver dans les uses
```php
# bad
namespace Foo;

\File::copy();
```
```php
# good
namespace Foo;

use File;

Foo::copy();
```
## Respectez vous et ceux qui vous lisent
```php
# bad
public function handle(ProjectRepository $projectRepository, ProjectService $projectService )
{

    $projects = $projectRepository->waitingForStandardisation();
    if(! $projects) {
        return $this->info('No project to standardize');

    }

  foreach($projects as $project) {

        $projectService->standardise($project);

        $this->ready($project);

    }
}
```
```php
# good
public function handle(ProjectRepository $projectRepository, ProjectService $projectService)
{
    $projects = $projectRepository->waitingForStandardisation();

    if (! $projects) {
        return $this->info('No project to standardize');
    }

    foreach ($projects as $project) {
        $projectService->standardise($project);

        $this->ready($project);
    }
}
```
## Ne jamais utiliser d'acronyme
```php
# bad
foreach ($pList as $p) {
    $projectServ->standardise($p);

    $this->ready($p);
}
```
```php
# good
foreach ($projects as $project) {
    $projectService->standardise($project);
}
```
## Injection de dépendances
```php
use Contracts\MyService;

class AnotherService
{
    /**
     * @var \Contracts\MyService
     */
    protected $myService;

    /**
     * @param \Contracts\MyService $myService
     */
    public function __construct(MyService $myService)
    {
        $this->myService = $myService;
    }
}

```
## Les textes toujours incluent dans les fichies de langue
```php
# bad
<p>Bonjour mon nom est <?php echo $userName; ?></p>
# good
<p><?php echo Lang::get('hello', ['userName' => $userName]); ?></p>

```
## Pluralisations
```php
# Le modèle est au singulier, sa table est quant à elle au pluriel
App\Models\Car;
# Le contrôleur, le repository, le seeder, etc est au pluriel
App\Controllers\CarsController;
App\Repositories\CarsRepository;
App\Seeders\CarsSeeder;
# Les routes sont au pluriel
Route::get('cars', 'CarsControllers@index')->name('cars.index');
```
## Cohérence entre les routes, les contrôleurs, le nom des vues et les traductions
```php
# app/Controllers/CarsController :
class CarsController
{
    public function index();
    public function create();
    public function edit();
    // ...
}
# app/routes/web.php
Route::resource('cars', 'CarsController')->name('cars.');
# app/resources/views/cars/index.blade.php
@section('content')
    <h1>@lang('cars.index.title')</h1>
    <a href="{{ route('cars.create') }}">@lang('cars.index.create_a_car')</a>
    // ...
# app/resources/views/cars/create.blade.php
    // ...
# app/resources/views/cars/edit.blade.php
    // ...
# app/resources/lang/fr/layouts.php
return [

    'cars' => [
        'index' => [
            'title' => "Titre de la page d'index",
            'create_a_car' => "Ajouter une voiture",
        ],
        // ...
    ],

];
```
## Convention de nommage
```php
# les classes
class FooBar extends FooBase implements FooContract {}

# les interfaces sont suffixés de Contract
interface FooContract {}

# les noms des variables sont en anglais, en camelCase et surtout elles sont explicites
$__ma_super_var = $r = $listeDesCars = $result = Car::all(); # bad
$cars = Car::all(); # good
```
## Utilisation de configuration
```php
# bad
class Service
{
    const SERVICE_URL = 'http://service.com'

    public function callMe()
    {
        // ...
        $client->get(self::SERVICE_URL . '/api');
    }
}
# good
class Service
{
    public function callMe()
    {
        // ...
        $baseUrl = config('service.url');
        $client->get($baseUrl . '/api');
    }
}
# perfect
use Support\Config;

class Service
{
    protected $config;

    public function __construct(Config $config)
    {
        $this->config = $config;
    }

    public function callMe()
    {
        // ...
        $baseUrl = $this->config->get('service.url');
        $client->get($baseUrl . '/api');
    }
}
```
## Utilisation des façades
```php
# bad
$user = auth()->user();

# good
use Facades\Auth;
$user = Auth::user();
```
