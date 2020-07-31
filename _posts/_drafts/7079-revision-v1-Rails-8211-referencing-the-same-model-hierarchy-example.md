---
id: 7081
title: 'Rails &#8211; referencing the same model  (hierarchy example)'
date: 2020-05-08T19:28:48+00:00
author: Nikita Kazakov
layout: revision
guid: https://nikitakazakov.com/7079-revision-v1/
permalink: /7079-revision-v1/
---
(TEST ALL THIS OUT IN CONSOLE BEFORE PUBLISHING POST)

Let&#8217;s say you have employees and you want to implement a supervisor and staff hierarchy.

A supervisor has many staff. A staff member has one supervisor.

If you don&#8217;t have an Employee model in your database and add a `supervisor_id` column as an integer. That column is going to reference the Employee mode&#8217;s primary key `id`.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">rails g migration Employee supervisor_id:integer</pre>

In your `employee.rb` model add these relationships:

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">has_many :staff, class_name: 'Employee', foreign_key: :supervisor_id
belongs_to :supervisor, class_name: 'Designer'</pre>

Explain that belongs\_to looks for a supervisor\_id&#8230;rails magic, it sees `:supervisor` and assumes you&#8217;ll have a `supervisor_id` in the table.

It also has a has_many staff&#8230;