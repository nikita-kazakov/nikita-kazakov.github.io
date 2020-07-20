---
id: 7019
title: Cleaning data and writing 14,000 rows to the database
date: 2020-03-05T23:51:27+00:00
author: Nikita Kazakov
layout: post
guid: https://nikitakazakov.com/?p=7019
permalink: /cleaning-data-and-writing-14000-rows-to-the-database/
site-sidebar-layout:
  - default
site-content-layout:
  - default
theme-transparent-header-meta:
  - default
categories:
  - Uncategorized
tags:
  - ruby
  - rubular fun
---
I needed car data for a Ruby on Rails project. I found a GitHub repository where someone generously shared 14,000 rows [of car model, makes, and year](https://github.com/n8barr/automotive-model-year-data).

The challenge was to import it into a Rails database running Postgresql.

I used Ruby to format each row to an array and then exported that into a CSV. Here&#8217;s how I did it.

## Cleaning Data with Ruby

I created a new file called `car_types.txt` in the Rails _project/lib_ folder.

I selected a few records from the github repo and pasted them into the `car_types.txt` file. We&#8217;ll process a few records now and wait until the end to process the rest.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/03/image-1024x343.png" alt="" class="wp-image-7021" srcset="https://nikitakazakov.com/wp-content/uploads/2020/03/image-1024x343.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-300x101.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-768x257.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-1536x515.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-2048x687.png 2048w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

I often use a debugger when I&#8217;m cleaning up data. Since I&#8217;m working in a Ruby on Rails project, I&#8217;ll be using [byebug](https://github.com/deivid-rodriguez/byebug) debugger.

In Rails, we use `seeds.rb` file to populate the database with test data. It makes sense to do data clean up there as well.

Let&#8217;s open up the `car_types.txt` file with the `File` class in Ruby. We&#8217;re going to read data line by line and transform it into CSV format.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">File.open('lib/car_types.txt').each do |line|
end</pre>

I&#8217;m going set a byebug breakpoint so that the application halts within the `File.open` block and we can see what is happening.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">File.open('lib/car_types.txt').each do |line|
  byebug
end</pre>

<pre class="EnlighterJSRAW" data-enlighter-language="shell" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group=""># Run the seeds.rb from the console.
rails db:seed</pre><figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/03/image-1.png" alt="" class="wp-image-7025" srcset="https://nikitakazakov.com/wp-content/uploads/2020/03/image-1.png 568w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-1-300x57.png 300w" sizes="(max-width: 568px) 100vw, 568px" /> <figcaption>Byebug halts runtime and you can start to modify data and see changes.</figcaption></figure> 

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group=""># In byebug mode.
line # "(1926, 'Chrysler', 'Imperial'),\n"
# We want to get each line looking like this:
# "1926,Chrysler,Imperial"</pre>

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">#create an empty array to store each line of record.
cars = []

File.open('lib/car_types.txt').each do |line|
  line
  # Remove the left parenthesis
  line.gsub!("(", "")
  # Remove the right parenthesis
  line.gsub!(")", "")
  # Remove the single quotes
  line.gsub!("'", "")
  # Remove the new line (\n)
  line.chomp!
  # Remove the comma at the end.
  line = line[0...-1]
  # Remove the any spaces.
  line.gsub!(", ", ",")
  #line is now properly formatted.
  line # "1926, Chrysler, Imperial"
  #Add the line into  the cars array.
  cars.push(line)
end</pre>

We successfully formatted each line and wrote all the results to the `cars` array. Let&#8217;s write that array to a csv file.

Let&#8217;s create a file `car_list_new.csv` in the _project/lib_ folder.

I won&#8217;t mention byebug with every example I show here but I highly encourage you to explore your code by using it to set breakpoints and see what Ruby is doing.

Create a `File.open` block which will open the new `car_list_new.csv` file and write the formatted car data to it.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">File.open('lib/car_list_new.csv', 'a') do |file|
  file.write(line)
  file.write("\n")
end</pre>

Open `car_list_new.csv` and you&#8217;ll see csv formatted car data on each line.

<pre class="EnlighterJSRAW" data-enlighter-language="no-highlight" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">1926,Chrysler,Imperial
1948,Citroën,2CV
1950,Hillman,Minx Magnificent
1953,Chevrolet,Corvette
1954,Chevrolet,Corvette
1954,Cadillac,Fleetwood
1955,Chevrolet,Corvette
1955,Ford,Thunderbird
1956,Chevrolet,Corvette
1957,Chevrolet,Corvette
1957,BMW,600
1958,Chevrolet,Corvette
1958,BMW,600
1958,Ford,Thunderbird</pre>

## Writing CSV to Postgresql

Let&#8217;s write the results to the database. In `seeds.db`, we&#8217;ll open `car_list_new.csv` and read each line within the block.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">File.open('lib/car_list_new.csv').each do |line|
  line # "Year,Make,Model\n"
  #Let's remove the new line (\n) and split each item into an array.
  vehicle = line.chomp.split(",")
  #Create a record in the database from each line.
  Car.create(year: vehicle[0].to_i, make: vehicle[1], model: vehicle[2])
end</pre>

I view the database with [Postico](https://eggerapps.at/postico/) and see the populated car records.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/03/image-2-1024x389.png" alt="" class="wp-image-7036" srcset="https://nikitakazakov.com/wp-content/uploads/2020/03/image-2-1024x389.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-2-300x114.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-2-768x292.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-2-1536x584.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/03/image-2.png 1574w" sizes="(max-width: 1024px) 100vw, 1024px" /> <figcaption>Viewing the cars table with Postico.</figcaption></figure> 

## Inserting all car records

Let&#8217;s insert all 14,000 cars in the database. Copy and paste all the car records into `car_types.txt` and delete all text from `car_list_new.csv` file. Before we run all our code in `seeds.db`, let&#8217;s clear out all the records from the `car` table by running `Car.delete_all`.

Here&#8217;s how the final `seeds.db` file looks like.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">Car.delete_all

cars = []
File.open('lib/car_types.txt').each do |line|
  line
  line.gsub!("(", "")
  line.gsub!(")", "")
  line.gsub!("'", "")
  line.chomp!
  line = line[0...-1]
  line.gsub!(", ", ",")
  cars &lt;&lt; line
end

File.open('lib/car_list_new.csv').each do |line|
  vehicle = line.chomp.split(",")
  Car.create(year: vehicle[0].to_i, make: vehicle[1], model: vehicle[2])
end</pre>

It took about 15 seconds to populate the database with over 14,000 rows of car data.

The way I&#8217;m writing to the database is inefficient. It&#8217;s slow. We&#8217;re pinging the database to create a row after reading each line of records. That&#8217;s over 14,000 hits to the database. You can use the [activerecord-import](https://github.com/zdennis/activerecord-import) gem to bring the time down to 2 seconds.

However, it doesn&#8217;t matter. I&#8217;m using this data in development environment and waiting 15 seconds isn&#8217;t a deal breaker. As a side benefit, I don&#8217;t have to use extra gems.