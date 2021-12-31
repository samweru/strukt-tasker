Tasker
===

A simple task manager for php.

## Getting started

```sh
wget https://github.com/pitsolu/strukt-tasker/releases/download/v1.0.0-alpha/tasker.phar #download
chmod a+x tasker.phar #make executable
mv tasker.phar tasker #rename
```

## Usage

By default, task manager will create `tasker.php` file if one isn't found when you execute the tasker command.

The intial `tasker.php` file contains a single command `test`. 

How to list commands:

```sh
$ tasker list

 version         Tasker version
 list            List commands
 test            Sample task
```
Below is sample `tasker.php`

```php

/**
 * Show today's date
 */
task('date', function(){

	$date = new \DateTime();

	echo(sprintf("Now: %s\n", $date->format("Y-m-d H:i:s")));
});

/**
 * Say hello to someone
 */
task("hello", function(string $name){

    writeln(sprintf("Hello %s!", $name));
});

/**
 * Say hello to the world
 */
task('test', function(){

    go("hello", " World!");
});

/**
 * Watch changes in javascript files
 */ 
task("watch:js", function(){

	watch("app/js", function($files){

		print_r(implode("\n", $files));
	});
});

/**
 * List directories
 */
task("lsdir", function(){

	list($output, $error) = run("ls -al", function($output){

		echo $output;
	});
});
```