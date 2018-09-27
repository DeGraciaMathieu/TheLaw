<p align='center'>
  <img src='https://i1.wp.com/blog.degracia-mathieu.fr/wp-content/uploads/2018/05/ezgif.com-gif-maker.gif?zoom=0.8999999761581421&resize=500%2C211&ssl=1'>
</p>

# TheLaw :boom:

## Structure d'une class
**Bad:** :thumbsdown: 
```php
class Foo {
    public function bar($var){
        //
    }
}
```
**Good:** :heart: 
```php
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
**Bad:** :thumbsdown: 
```php
use My\Long\Ordened;
use My;
use My\Long\Ordened\Namespace;
use My\Long;
```
**Good:** :heart: 
```php
use My;
use My\Long;
use My\Long\Ordened;
use My\Long\Ordened\Namespace;
```
## Garder un code propre et aérer
**Bad:** :thumbsdown: 
```php
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
**Good:** :heart: 
```php
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
**Bad:** :thumbsdown: 
```php
if (! $page) return null;
```
**Good:** :heart:
```php
if (! $page) {
    return null;
}
```
## Attention à l'utilisation de la négation
**Bad:** :thumbsdown: 
```php
$dontDoIt = true;

if (! $dontDoIt) {
    //
}
```
**Good:** :heart:
```php
$doIt = true;

if ($doIt) {
    //
}
```
## Diminuer l'imbriquation du code
**Bad:** :thumbsdown: 
```php
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
**Good:** :heart:
```php
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
**Bad:** :thumbsdown: 
```php
function createFile($tmp = true)
{
    if ($tmp) {
        // foo
    } else {
        // foo
    }
}
```
**Good:** :heart:
```php
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
**Bad:** :thumbsdown: 
```php
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
**Good:** :heart:
```php
class RaptorPaddock
{
    //
}
```
## Toutes les classes en dehors du namespace courant doivent se trouver dans les uses
**Bad:** :thumbsdown: 
```php
namespace Foo;

\File::copy();
```
**Good:** :heart:
```php
namespace Foo;

use File;

File::copy();
```
## Respectez vous et ceux qui vous lisent
**Bad:** :thumbsdown: 
```php
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
**Good:** :heart:
```php
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
**Bad:** :thumbsdown: 
```php
foreach ($pList as $p) {
    $projectServ->standardise($p);
}
```
**Good:** :heart:
```php
foreach ($projects as $project) {
    $projectService->standardise($project);
}
```
## Injection de dépendances
**Good:** :heart:
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
**Bad:** :thumbsdown: 
```php
<p>Bonjour mon nom est <?php echo $userName; ?></p>
```
**Good:** :heart:
```php
<p><?php echo Lang::get('hello', ['userName' => $userName]); ?></p>

```
## Pluralisations
**Good:** :heart:
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
**Good:** :heart:
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
**Good:** :heart: 
```php
# les classes
class FooBar extends FooBase implements FooContract {}

# les interfaces sont suffixés de Contract
interface FooContract {}
```

## les noms des variables sont en anglais, en camelCase et surtout elles sont explicites
**Bad:** :thumbsdown: 
```php
$__ma_super_var = $r = $listeDesCars = $result = Car::all(); 
```
**Good:** :heart: 
```php
$cars = Car::all(); 
```
## Utilisation de configuration
**Bad:** :thumbsdown: 
```php
class Service
{
    const SERVICE_URL = 'http://service.com'

    public function callMe()
    {
        // ...
        $client->get(self::SERVICE_URL . '/api');
    }
}
```
**Good:** :heart: 
```php
class Service
{
    public function callMe()
    {
        // ...
        $baseUrl = config('service.url');
        $client->get($baseUrl . '/api');
    }
}
```
**Perfect:** :heartpulse: 
```php
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
**Bad:** :thumbsdown: 
```php
$user = auth()->user();
```
**Good:** :heart:
```php
use Facades\Auth;

$user = Auth::user();
```
## Ne compensez pas du mauvais code par des commentaires
**Bad:** :thumbsdown: 
```php
# Vérifie que le client peut bénéficier des avantages 
if (($customer->flag && HOURLY_FLAG) && $customer->age > 65) {
    //
}
```
**Good:** :heart:
```php
if ($customer->isEligibleForBenefits()) {
    //
}
```
## Diminuez la charge cognitive de votre code
**Bad:** :thumbsdown: 
```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Wait, what is `$li` for again?
    dispatch($li);
}
```
**Good:** :heart:
```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```
## Attention à l'utilisation de la classe Exception
**Bad:** :thumbsdown: 
```php
if (condition) {
    throw new Exception();
}
```
**Good:** :heart:
```php
if (condition) {
    throw new MySpecificException();
}
```
## Ne pas hesiter à créer des formes négatives des méthodes
**Bad:** :thumbsdown: 
```php
if (! $user->haveRight('...')) {
    //
}
```
**Good:** :heart:
```php
if ($user->dontHaveRight('...')) {
    //
}
```
## Ne pas utiliser directement les valeurs de l'environnement
**Bad:** :thumbsdown: 
```php
$host = env('HOST');
```
**Good:** :heart:
```php
# app/config/app.php
return [
  'host' => env('HOST'),
];

$host = config('app.host');
```
## Attention aux accidents ferroviaires
**Bad:** :thumbsdown: 
```php
$user->getAccount()->getBalance()->deductAmount($orderTotal);
```
**Good:** :heart:
```php
$account = $user->getAccount();
$balance = $account->getBalance();
$balance->deductAmount($orderTotal);
```
