# Rake Snippets

This file contains snippets of rake files that have proven useful over the
years. The are listed here, together for ease of copy and pasting where needed.

### Tests

The standard unit test suite:

```ruby
require 'rake/testtask'

#Run the Fibonacci unit test suite.
Rake::TestTask.new do |t|
  #List out all the test files.
  t.test_files = FileList['tests/**/*.rb']
  t.verbose = false
  t.warning = true
end
```
The test suite is accessed via:

    $ rake test

Sometimes there are tests that you'd like to still have, but not run as part
of the standard unit tests. The following example shows a series of tests
called integration tests:

```ruby
#Run the fOOrth integration test suite.
Rake::TestTask.new(:integration) do |t|
  #List out all the integration test files.
  t.test_files = FileList['integration/*.rb']
  t.verbose = false
  t.warning = true
end
```

This example is accessed via:

    $ rake integration

#### Alternate Test

The test environment includes a lot of wierd, funky stuff that sometimes gets
in the way. The alternate test task runs tests with a minimum of extra baggage.
This often helps a lot.

```ruby
desc "Alternative test procedure"
task :alt_test do |t|
  here  = File.dirname(__FILE__)
  target = "#{here}/test/*.rb"
  puts "Target files = #{target}"
  puts

  block = "{|file| require file if File.basename(file) =~ /test/}"
  code  = "Dir['#{target}'].each #{block}"

  system "ruby -e\"#{code}\""
end
```

### Documentation

```ruby
require 'rdoc/task'

#Generate internal documentation with rdoc.
RDoc::Task.new do |rdoc|
  rdoc.rdoc_dir = "rdoc"

  #List out all the files to be documented.
  rdoc.rdoc_files.include("lib/**/*.rb", "license.txt", "README.md")

  #Make all access levels visible.
  rdoc.options << '--visibility' << 'private'
  #rdoc.options << '--verbose'
  #rdoc.options << '--coverage-report'

  #Set a title.
  #rdoc.options << '--title' << 'Title Goes Here'
end
```
This task is accessed via:

    $ rake rdoc


Note: I am moving away from rdoc on the grounds that it is often distracting
from understanding the code and is an extra maintenance burden and is often
out of date and thus misleading.


### Code Smells

The reek gem is a powerful tool for identifying areas of code that may be
improved. This snippet run a scan on the code library and records the results:

```ruby
desc "Run a scan for smelly code!"
task :reek do |t|
  `reek --no-color lib > reek.txt`
end
```

Run this via:

    $ rake reek

Note that the output is directed toward the file reek.txt without any fancy
colorization or other special effects. This is part of my workflow in that
I prefer to have a record of code smells at various points in the development
and saving results to a text file makes it easy to version control the smell
reports as the project progresses.

### Debug/Test Console

Now there are several ways to run an irb console from rake, with test code
"preloaded". There are also a number of problems with this. The most severe is
that rake really seems to mess up the console. The long and short of it that
rake should be used for batch tasks, not interactive ones. Here is my
workaround to this issue:

```ruby
desc "Run an IRB Session with fibonacci_rng loaded."
task :console do
  system "ruby irbt.rb local"
end
```

Now irbt.rb is a file that resides along with the rakefile.rb file. Here is an
example of this file for the fibonacci_rng mentioned above:

```ruby
# coding: utf-8
# An IRB + fibonacci_rng Test bed

require 'irb'

puts "Starting an IRB console with fibonacci_rng loaded."

if ARGV[0] == 'local'
  require_relative 'lib/fibonacci_rng'
  puts "fibonacci_rng loaded locally: #{FibonacciRng::VERSION}"

  ARGV.shift
else
  require 'fibonacci_rng'
  puts "fibonacci_rng loaded from gem: #{FibonacciRng::VERSION}"
end

IRB.start
```

This is accessed via:

    $ rake console

And yes, bundler uses a different approach, but I cannot use it since it uses
bash scripts to get things working.

### Versions

A tiny, useful task simply identifies the version that would be built next.

```ruby
desc "What version of the Fibonacci is this?"
task :vers do |t|
  puts
  puts "Fibonacci random number generator version = #{FibonacciRng::VERSION}"
end
```

This code only works because the bundler adds require "bundler/gem_tasks" at
the top of the rakefile. Otherwise you'll have to require_relative the
appropriate file on your own.

This task is accessed via:

    $ rake vers




































