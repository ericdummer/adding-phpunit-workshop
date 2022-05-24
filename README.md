# Adding PHPUnit for the first time
1. Load the container (see "Loading and connecting to the docker container".)
2. While in the container run the following command:

```shell
composer required --dev phpunit/phpunit
```

3. Add the scripts attribute with `"tests": "phpunit"` to composer.json. If the scripts attribute is already there, just add the `"test": phpunit` to scripts

```json
{
  "scripts": {
    "test": "phpunit"
  }
}
```
4. Create the file `phpunit.xml.dist` and past in the followint contents:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit backupGlobals="false"
         backupStaticAttributes="false"
         bootstrap="vendor/autoload.php"
         colors="true"
         convertDeprecationsToExceptions="true"
         convertErrorsToExceptions="true"
         convertNoticesToExceptions="true"
         convertWarningsToExceptions="true"
         processIsolation="false"
         stopOnFailure="false"
>
    <testsuites>
        <testsuite name="Test Suite">
            <directory suffix=".php">./tests/</directory>
        </testsuite>
    </testsuites>
</phpunit>
```
5. In the `src` folder add a new folder called `tests`
6. In PHPStorm, right-click on the `tests` folder and click on `Mark Directory as > Test Sources Root`
7. In PHPStorm, navigate to `src/MySite/Example.php`
8. Put your cursor on the method `helloWorld` and press `Ctrl+Shift+T` or `⇧⌘T` in macOS.
This will create a new file at `tests/MySite/ExampleTest.php`
9. Add a test to prove `helloWorld` is working correctly, i.e. should return `Hello World!`)
10. In the container, type `composer test` to see run the tests.

### Running just one test on the commandline

See [Writing custom commands](https://getcomposer.org/doc/articles/scripts.md#writing-custom-commands).

You can run tests through composer and still pass arguments to `phpunit`.
Adding a double dash (`--`) tells composer to use the remaining options as the phpunit's options.
For example, to run just one test you can type the following command
```shell
composer test -- --filter Example
```

## Loading and connecting to the docker container
To launch the container:

```docker compose up -d --build```

To rebuild it after a Docker change:

```docker compose up -d --build --remove-orphans```

To connect to the container (using bash)

```docker exec -it docker-php-composer-core-1 /bin/bash```
