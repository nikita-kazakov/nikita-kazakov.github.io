---
title: Intermediate Debugging Ruby on Rails with Pry
date: 2021-02-24
layout: post
permalink: /pry-debugging/
tags: 
    - ruby on rails
---

I use Pry on a daily basis while writing / debugging code. I want to show you how to go beyond a simple breakpoint with pry. I'll show you how I use it to learn about unfamiliar code and how to debug code.

Pry is a powerful Ruby debugger that is also available as a debugger for Rails using the [pry-byebug](https://github.com/deivid-rodriguez/pry-byebug) gem.

But Ruby on Rails already ships with the byebug debugger. Why use pry? Pry adds awesome syntax highlighting, allows scoping into a method or class, running through stack traces, and adding dynamic breakpoints.

## Adding Pry to a Rails Project

Open your `Gemfile` and add `gem pry-byebug` to your development and test block. Why those two block? Because I also use pry to figure out why my tests are failing.

```ruby
group :development, :test do
  gem 'pry-rails'
  gem 'pry-byebug'
end
```

Run `bundle install`in the terminal to update the `Gemfile`.


## Disabling Pry Pager

I disable the pry pager as it drove me nuts because pry seemed unresponsive when outputting long results in the terminal.
If you don't disable the pager and encounter the unresponsive `:`, press q.

Create a `.pryrc` file in your root Rails project folder, disable the pager, and add a few aliased shortcuts. This file will load up automatically each time pry is started.
 
```ruby
if defined?(PryByebug)
  Pry.config.pager = false
  Pry.commands.alias_command 'c', 'continue'
  Pry.commands.alias_command 's', 'step'
  Pry.commands.alias_command 'n', 'next'
end
```

To avoid pressing `q` all the time, create a `.pryrc` file in your root Rails project folder. I like to disable the pager and alias the continue, step and break commands to single letters.

# Binding.pry 

Put `binding.pry` anywhere you want to pry to stop ruby code and open the debugger. You can put it in a controller, model, or even a view! If Rails hits `binding.pry`, it will open the debugger.

## Summary Commands

- `@` or `whereami` - to see where you are in the stack.
- `break` to set breakpoint. Example `break 13` to set a breakpoint on line 13 in the current stack.
- `break` to view current break points.
- `break -e 3` - to enable third break point.
- `break -d 3` - to disable third breakpoint.
- `break --delete-all` - to delete all breakpoints.
- `next` to skip over a lengthy method instead of stepping into it.
- `backtrace` - shows the trace of all the stacks.
- `frame 5` - selects the stack trace number to go into.
- `up` - to go up the stack trace.
- `down` - to go down the stack trace.

# Leave management example

Let's say we're working with a leave management system and there's a controller that approves a day off. We want to investigate what it does.

Let's add a `binding.pry` in the controller where we want the debugger to open.

```ruby
  def approve
    @pending_leave_day.update_attributes(approved_1: true, approved_2: true)
    respond_with(:admin, @pending_leave_day, location: admin_pending_leave_days_path, notice: "Leave Request for #{@pending_leave_day.designer.name} was approved.")
    binding.pry # Add a pry breakpoint.
    @pending_leave_day.update_leave_days_table
    @pending_leave_day.notify_leave_approved
  end
```

```ruby
    38: def approve
    39:   @pending_leave_day.update_attributes(approved_1: true, approved_2: true)
    40:   respond_with(:admin, @pending_leave_day, location: admin_pending_leave_days_path, notice: "Leave Request for #{@pending_leave_day.designer.name} was approved.")
    41:   binding.pry
 => 42:   @pending_leave_day.update_leave_days_table
    43:   @pending_leave_day.notify_leave_approved
    44: end
```

Notice the arrow on line 42. That's where we are in the code. 

What exactly does does the `update_leave_days_table` method do? I don't know. Let's `step` into it.

```ruby
From: /Users/admin/RubymineProjects/project/app/models/pending_leave_day.rb @ line 48 PendingLeaveDay#update_leave_days_table:

    47: def update_leave_days_table
 => 48:   days_without_holidays.each do |day|
    49:     self.leave_days.create(day_off:day, designer:designer, half_day:half_day)
    50:   end
    51: end
```

Pry tells me the file location and the line it is on. I open that up in my editor. Now I can explore methods at this breakpoint.

```ruby
days_without_holiday # => [Thu, 25 Jun 2020, Fri, 26 Jun 2020]
```

But how is `days_without_holiday` method work? Let's `step` into this line again!

```ruby
From: /Users/admin/RubymineProjects/project/app/models/pending_leave_day.rb @ line 40 PendingLeaveDay#days_without_holidays:

    39: def days_without_holidays
 => 40:   valid_days = []
    41:   (start_date..end_date).each do |day|
    42:     valid_days << day unless  day.in?(Holiday.all_future_dates)
    43:   end
    44:   valid_days
    45: end

```

If there's some variable here that you want to know more about, just type it into the pry console. What is the `start_date` value?

```ruby
start_date # => Thu, 25 Jun 2020
end_date # => Thu, 25 Jun 2020
Holiday.all_future_dates # []
```

Do you see how powerful pry is for investigative purposes?

Anytime you want to comeback to where you were, just type in `whereami` or `@`.

Let's say I want to `break` on line 42, right inside the each block.

One way is to keep stepping through code until you get to that line. However, you'll notice that you begin stepping through Rails framework classes which aren't relevant to you. 

```ruby
From: /Users/admin/RubymineProjects/project/app/models/pending_leave_day.rb @ line 41 PendingLeaveDay#days_without_holidays:

    39: def days_without_holidays
    40:   valid_days = []
 => 41:   (start_date..end_date).each do |day|
    42:     valid_days << day unless  day.in?(Holiday.all_future_dates)
    43:   end
    44:   valid_days
    45: end
```

You'll hit `step` and you'll get something cryptic like this:

```ruby
From: /Users/admin/.rvm/gems/ruby-2.4.10@designpickle/gems/activerecord-5.2.4.3/lib/active_record/attribute_methods/read.rb @ line 39 self.__temp__3747162747f546164756:
    34:             sync_with_transaction_state = "sync_with_transaction_state" if name == primary_key
    35: 
    36:             generated_attribute_methods.module_eval <<-STR, __FILE__, __LINE__ + 1
    37:               def #{temp_method}
    38:                 #{sync_with_transaction_state}
 => 39:                 name = ::ActiveRecord::AttributeMethods::AttrNames::ATTR_#{safe_name}
    40:                 _read_attribute(name) { |n| missing_attribute(n, caller) }
    41:               end
    42:             STR
    43: 
    44:             generated_attribute_methods.module_eval do
```

I can quickly tell I'm in the wrong place by looking at the first line and seeing the file is `From: ...rvm/gems`. It's framework code. It's not relevant to us right now.

Don't despair. You can move `up` and `down` stacks in pry. Simply move `up` in your pry console.

```ruby
From: /Users/admin/RubymineProjects/project/app/models/pending_leave_day.rb @ line 41 PendingLeaveDay#days_without_holidays:

    39: def days_without_holidays
    40:   valid_days = []
 => 41:   (start_date..end_date).each do |day|
    42:     valid_days << day unless  day.in?(Holiday.all_future_dates)
    43:   end
    44:   valid_days
    45: end
```
You're back! We want to run all the code and only break on line 42. Type in `break 42` in the pry console.

Pry just added a breakpoint to line 42. It essentially added a `binding.pry` to that line.

From here on out, we can simply `continue` or `c` in the pry console to run code until that line 42 breakpoint.

```ruby
From: /Users/admin/RubymineProjects/jar_legacy/app/models/pending_leave_day.rb @ line 42 PendingLeaveDay#days_without_holidays:

    39: def days_without_holidays
    40:   valid_days = []
    41:   (start_date..end_date).each do |day|
 => 42:     valid_days << day unless  day.in?(Holiday.all_future_dates)
    43:   end
    44:   valid_days
    45: end
```

Success! We skipped through the un-needed framework classes and got to line 42. On this line, let's investigate what some variables are.

```ruby
day # => Thu, 25 Jun 2020
day.in?(Holiday.all_future_dates) # => false
```

Let's add another break on line 44 to get out of this loop and continue.

`break 44`
`continue`

## Help

Type in `help` in your pry console. Pry shows you all the available commands. There are a lot of them and this is a great area for exploration

```text
Help
  help               Show a list of commands or information about a specific command.

Context
  cd                 Move into a new context (object or scope).
  find-method        Recursively search for a method within a class/module or the current namespace.
  ls                 Show the list of vars and methods in the current scope.
  pry-backtrace      Show the backtrace for the pry session.
  raise-up           Raise an exception out of the current pry instance.
  reset              Reset the repl to a clean state.
  watch              Watch the value of an expression and print a notification whenever it changes.
  whereami           Show code surrounding the current context.
  wtf?               Show the backtrace of the most recent exception.

Editing
  /^\s*!\s*$/        Clear the input buffer.
  amend-line         Amend a line of input in multi-line mode.
  edit               Invoke the default editor on a file.
  hist               Show and replay readline history.
  play               Playback a string variable, method, line, or file as input.
  show-input         Show the contents of the input buffer for the current multi-line expression.

Introspection
  ri                 View ri documentation.
  show-doc           Show the documentation for a method or class.
  show-source        Show the source for a method or class.
  stat               View method information and set _file_ and _dir_ locals.

Gems
  gem-cd             Change working directory to specified gem's directory.
  gem-install        Install a gem and refresh the gem cache.
  gem-list           List and search installed gems.
  gem-open           Opens the working directory of the gem in your editor.
  gem-readme         Show the readme bundled with a rubygem
  gem-search         Search for a gem with the rubygems.org json api
  gem-stat           Show the statistics of a gem (requires internet connection)

Commands
  import-set         Import a pry command set.
  install-command    Install a disabled command.

Aliases
  !!!                Alias for `exit-program`
  !!@                Alias for `exit-all`
  $                  Alias for `show-source`
  (?-mix:whereami[!?]+) Alias for `whereami`
  ?                  Alias for `show-doc`
  @                  Alias for `whereami`
  c                  Alias for `continue`
  clipit             Alias for `gist --clip`
  file-mode          Alias for `shell-mode`
  find-routes        Alias for `find-route`
  history            Alias for `hist`
  n                  Alias for `next`
  quit               Alias for `exit`
  quit-program       Alias for `exit-program`
  reload-method      Alias for `reload-code`
  s                  Alias for `step`
  show-method        Alias for `show-source`

Byebug
  backtrace          Display the current stack.
  break              Set or edit a breakpoint.
  continue           Continue program execution and end the pry session.
  down               Move current frame down.
  finish             Execute until current stack frame returns.
  frame              Move to specified frame #.
  next               Execute the next line within the current stack frame.
  step               Step execution into the next line or method.
  up                 Move current frame up.

Input and output
  .<shell command>   All text following a '.' is forwarded to the shell.
  cat                Show code from a file, pry's input buffer, or the last exception.
  change-inspector   Change the current inspector proc.
  change-prompt      Change the current prompt.
  clear-screen       Clear the contents of the screen/window pry is running in.
  fix-indent         Correct the indentation for contents of the input buffer
  list-inspectors    List the inspector procs available for use.
  save-file          Export to a file using content from the repl.
  shell-mode         Toggle shell mode. bring in pwd prompt and file completion.

Misc
  gist               Upload code, docs, history to https://gist.github.com/.
  pry-version        Show pry version.
  reload-code        Reload the source file that contains the specified code object.
  toggle-color       Toggle syntax highlighting.

Navigating pry
  !pry               Start a pry session on current self.
  disable-pry        Stops all future calls to pry and exits the current session.
  exit               Pop the previous binding.
  exit-program       End the current program.
  jump-to            Jump to a binding further up the stack.
  nesting            Show nesting information.
  switch-to          Start a new subsession on a binding in the current stack.

Rails
  find-route         See which urls match a given controller.
  recognize-path     See which route matches a url.
  show-middleware    Show all middleware (that rails knows about).
  show-model         Show the given model.
  show-models        Show all models.
  show-routes        Show all routes in match order.
```

# ls command

Pry let's you analyze what is going on in your current scope. This is like the list directory command in linux.
Just type in `ls` and you'll see local variables, instance variables, and available methods.

Let's say you want to see what you can do with an array.
```ruby
ls [1,2,3]
```

You quickly see all the array methods available for you to use! This is powerful for exploration.

# cd command

Pry allows you to enter any object to see within it. It's analogous to changing directories in linux. You 'change directory' to change the scope to inside an object.

```ruby
cd [1,2,3]
[47] pry(#<Array>):1>
```

Note that the pry prompt is now showing the Array class. Run `ls` and you'll see all the methods within the Array object! Let's say there's a method you want to see documentation for, use the `?` to explore documentation for that method.

```ruby
? deep_dup
```

```text
From: /Users/admin/.rvm/gems/ruby-2.4.10@designpickle/gems/activesupport-5.2.4.3/lib/active_support/core_ext/object/deep_dup.rb @ line 21:
Owner: Array
Visibility: public
Signature: deep_dup()
Number of lines: 8

Returns a deep copy of array.

  array = [1, [2, 3]]
  dup   = array.deep_dup
  dup[1][2] = 4

  array[1][2] # => nil
  dup[1][2]   # => 4
```

It returns documentation with examples for using that method.

If you want to see the source code of the particular method, use the `$` command.

```text
$ deep_dup

From: /Users/admin/.rvm/gems/ruby-2.4.10@designpickle/gems/activesupport-5.2.4.3/lib/active_support/core_ext/object/deep_dup.rb @ line 29:
Owner: Array
Visibility: public
Number of lines: 3

def deep_dup
  map(&:deep_dup)
end
```

To step out of the object, `cd ..` as you would in linux.


## Exploring Breaks

From the `help` command, I discovered the `break` command.

Type in `break`
```ruby
# Enabled At 
  -------------
  3 Yes     /Users/admin/RubymineProjects/project/app/models/pending_leave_day.rb @ 42
  4 Yes     /Users/admin/RubymineProjects/project/app/models/pending_leave_day.rb @ 44
```

Notice the two breakpoints from before. They are both enabled. This suggests that it's possible to disable them. But how do we do that?

Let's use pry to investigate the break source code for clues!

```ruby
$ break # Shows the source code for the pry break command.
```

Scroll up and you'll see example code
```text
Examples:
      break SomeClass#run         Break at the start of `SomeClass#run`.
      break Foo#bar if baz?       Break at `Foo#bar` only if `baz?`.
      break app/models/user.rb:15 Break at line 15 in user.rb.
      break 14                    Break at line 14 in the current file.

      break --condition 4 x > 2   Add/change condition on breakpoint #4.
      break --condition 3         Remove the condition on breakpoint #3.

      break --delete 5            Delete breakpoint #5.
      break --disable-all         Disable all breakpoints.

      break --show 2              Show details about breakpoint #2.
      break                       List all breakpoints.
```

Even better, there's an `options` method with more clues

```ruby
def options(opt)
      defaults = { argument: true, as: Integer }
      opt.on :c, :condition, "Change condition of a breakpoint.", defaults
      opt.on :s, :show, "Show breakpoint details and source.", defaults
      opt.on :D, :delete, "Delete a breakpoint.", defaults
      opt.on :d, :disable, "Disable a breakpoint.", defaults
      opt.on :e, :enable, "Enable a disabled breakpoint.", defaults
      opt.on :'disable-all', "Disable all breakpoints."
      opt.on :'delete-all', "Delete all breakpoints."
    end
```

It appears that we can pass arguments to the break command. Let's try to disable all the breakpoints.

```text
break --disable-all
```

```text
[60] pry(#<PendingLeaveDay>)> break --disable-all

  # Enabled At 
  -------------

  3 No      /Users/admin/RubymineProjects/jar_legacy/app/models/pending_leave_day.rb @ 42
  4 No      /Users/admin/RubymineProjects/jar_legacy/app/models/pending_leave_day.rb @ 44

```

It worked. This is how you leverage pry to explore / debug / review code on a daily basis.


# More Resources on Pry

I learned a lot from Conrad Irwin's and Joel Turnbull's pry videos below. I highly recommend watching these to see real pry workflows.

Ruby Conf 2013 - REPL driven development with Pry by Conrad Irwin
{% include embed_youtube.html id="D9j_Mf91M0I" %}

RailsConf 2014 - Debugger Driven Developement with Pry by Joel Turnbull
{% include embed_youtube.html id="4hfMUP5iTq8" %}
