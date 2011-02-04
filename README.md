# Welcome!

`Nake` is a [Ruby Rake](http://rake.rubyforge.org) like tasks manager for
[NodeJS](http://nodejs.com)

## Usage Basics

`Nake` provides you with some options how you can hook it up. First of all you
can install `Nake` with [npm](htp://npmjs.org)

    npm install nake

And after that create a `Nakefile` inside of your project

    var Nake = require('nake');

    Nake.task('taskname'[, 'description',] function() {
      // the task code in here
    });

Then run `nake` command in the terminal

    nake taskname

Call `-h` for the command line options

    nake -h

## Using Without NPM

If you don't have [npm](htp://npmjs.org) or want to use `Nake` as a standalone
library, then just call `Nake.start()` the following way

    var Nake = require('nake');

    Nake.task(...);
    Nake.task(...);

    Nake.start(); // <- kicking in

After that just run your file with [NodeJS](http://nodejs.com)

    node ./myfile


## Namespaces

You also can create namespaces for tasks by using the `Nake.namespace` call

    Nake.namespace('boo', function() {
      Nake.task('task1', 'task1 description', function() {
        // task 2 code
      });

      Nake.task('task2', 'task2 description', function() {
        // task 2 code
      })
    });

After that you'll have those tasks registered within the `boo:` namespace

    nake boo:task1
    nake boo:task2


## Default Task

To specify a default task that should be executed if the `nake` tool was
called without any options, specify the task name with the `Nake.Default`
attribute

    Nake.Default = 'task_name';


## Invoking Other Tasks

You can invoke any tasks by name via the `Nake.run` call

    Nake.run('taskname');
    Nake.run('taskname', true); // <- quiet run

Or you can save your tasks into local variables and run them directly

    var task1 = Nake.task('name1', function() {});
    var task2 = new Nake.Task('name2', function() {});

    task1.run();
    task2.run(true); // <- quiet run


## Logging The Steps

And you also can report the steps that your task is currently working on

    Nake.task('task', 'Task Description', function() {
      this.step('Doing something 1');
      // ....

      this.step('Doing something 2');
      // ....

      this.step('Doing something 3');
      // ....
    });

This will result the following log in the console

    == Task Description =======================================
     - Doing something 1
     - Doing something 2
     - Doing something 3
    DONE




## License

This project is released under the terms of the MIT license.

Copyright (C) 2011 Nikolay Nemshilov

