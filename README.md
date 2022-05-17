Tasker
===

A simple task manager for php.

## Getting started

```sh
wget https://github.com/samweru/strukt-tasker/releases/download/v1.0.0-alpha/tasker.phar #download
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

		$changes = [];
		foreach($files as $file)
			$changes[] = sprintf("%s\n", $file);

		print_r(implode("\n", $changes));
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

## Boxing

First you'll need to install [phive](https://github.com/phar-io/phive)

```sh
wget -O phive.phar https://phar.io/releases/phive.phar
wget -O phive.phar.asc https://phar.io/releases/phive.phar.asc
gpg --keyserver hkps://keys.openpgp.org --recv-keys 0x9D8A98B29B2D5D79
gpg --verify phive.phar.asc phive.phar
chmod +x phive.phar
sudo mv phive.phar /usr/local/bin/phive
```

Then, install [Box](https://github.com/box-project/box) globally.

```sh
phive install humbug/box --force-accept-unsigned
```

..and update.

```sh
phive update humbug/box --force-accept-unsigned
```

..or install `Box` locally.

```sh
composer require --dev bamarni/composer-bin-plugin
composer bin box require --dev humbug/box

vendor/bin/box
```

..or 

```sh
$ curl -LSs https://box-project.github.io/box2/installer.php | php
```