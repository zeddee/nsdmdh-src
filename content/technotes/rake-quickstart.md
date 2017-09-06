---
author: zeddified
comments: true
excerpt: 'Rake quickstart'

slug: rake-quickstart
title: Getting Started with Rake
categories:
- Technotes
tags:
- Technotes
- Zed

image_path: "/img/colours/goldfish.png"
---

Rake is a task runner that uses [Ruby](https://www.ruby-lang.org/en/).

To get rake up and running, just run:

``` gem install rake ```

It's useful for running deploy scripts and generally getting things up and running in your dev environments.

What you need is a ```Rakefile``` in your dev environment's root folder (or wherever you want to run the ```rake``` command).

Write a Ruby script in the ```Rakefile``` and run ```rake``` — and it'll get to work.

## Rakefile Syntax

The basic unit of a Rakefile is a ```task``` function.

At the top level, you can define a "default" ```task``` that will run when you run ```rake``` with no arguments.

E.g.
{% highlight ruby %}
task :default => [:taskone, :tasktwo]

task :taskone do
    puts "this is task one"
end

task :tasktwo do
    puts "this is task two"
end
{% endhighlight %}

Running:
```
$ rake
```

Outputs:
{% highlight bash %}
this is task one
this is task two
{% endhighlight %}

You can also run:
```
$ rake tasktwo
```

Which will output:
```
this is task two
```

## Rake Namespaces

If you're making rakefiles which have to be merged with a larger project, you can set ```namespaces``` to prevent name conflicts with existing tasks in the project.

You set a ```namespace``` with the following syntax:
{% highlight ruby %}
namespace :namespace_one do
    task :taskone do
        puts "this _task one_ coexists with the other taskone"
    end
end

task :default => [:taskone]

task :taskone do
    puts "this is task one"
end
{% endhighlight %}

Running ```rake``` will output:

```
this is task one
```

But running ```rake namespace_one:taskone``` will output:
```
this _task one_ coexists with the other taskone
```

NB:
```namespaces``` are not functions and will not run like a ```task```

## Running Shell Commands with Rake

You can get Rake to run shell commands with the following syntax:

```
task :runshell do
    sh "touch raketest.rb"
    sh 'echo "p :hahahaha" > raketest.rb'
    ruby "./raketest.rb"
    sh "rm ./raketest.rb"
end
```

This will output:
```
touch raketest.rb
echo "p :hahahaha" > raketest.rb
/Users/zed/.rvm/rubies/ruby-2.3.0/bin/ruby ./raketest.rb
:hahahaha
rm ./raketest.rb
```

## Adding in-rake Documentation

In-line comments are always a good way of documenting your code.

You can add in-rake documentation with the ```desc``` function.

Just add a ```desc``` before a task as such:

```
desc "this describes what task one does"
task :taskone do
    puts "this is task one"
end
```

Running ```rake --tasks``` will output a list of tasks with their ```desc```s attached.

E.g.
```
taskone # this describes what task one does
```
