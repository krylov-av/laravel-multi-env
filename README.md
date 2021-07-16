# laravel-multi-env
About multi-env for project
Sometimes you need run your project in multi-environment mode. For example, for different domains you can use different databases.

How to do this.

1. You can use 
https://packagist.org/packages/casperwilkes/laravel-environment_detector
here is prity simple.

2. You can do this thing by you hands.
edit bootstrap/app.php and add before last line following code:
[code]
/*
|--------------------------------------------------------------------------
| Return The Application
|--------------------------------------------------------------------------
|
| This script returns the application instance. The instance is given to
| the calling script so we can separate the building of the instances
| from the actual running of the application and sending responses.
|
*/

if (isset($_SERVER['HTTP_HOST']) && !empty($_SERVER['HTTP_HOST']))
{
    $domain = $_SERVER['HTTP_HOST'];
    $dotenv = Dotenv\Dotenv::createImmutable(base_path(),'.env.'.$domain);
    try{
        $dotenv->load();
    } catch(\Dotenv\Exception\InvalidPathException $e){
        print "No Custom .env file!";
        exit;
    }
}
return $app;
[/code]

next step - add .env.{domain} files to your project and enjoy it
