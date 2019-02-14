Tasker
===

A simple task manager for php.

## Getting started

```sh
wget -c tasker.phar #download
chmod a+x tasker.phar #make executable
mv tasker.phar tasker #rename
```

## Usage

By default, task manager will create `tasker.php` file if one isn't found when you execute the tasker command.

The intial `tasker.php` file contains a single command `test`. 

How to list commands:

```sh
$ tasker list

 version
 list
 test
```
Below is sample `tasker.php`

```php

task('date', function(){

	$date = new \DateTime();

	echo(sprintf("Now: %s\n", $date->format("Y-m-d H:i:s")));
});

task('echo', function(){

	go('test');
});

task('test', function(){

    writeln('Hello world');
});

task("watch:js", function(){

	watch("app/js", function($files){

		print_r($files);
	});
});

task("apt:update", function(){

	list($output, $error) = run("apt update", function($output){

		echo $output;
	});
});
```