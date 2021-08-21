---
title: How to pass foreign keys to Rails strong params.
date: 2021-07-28
layout: post
permalink: /passing-foreign-keys-rails-strong-params
tags: 
    - ruby on rails
---

We have a project and a project can have many tasks. Let's say we have a task form where a user can specify the project the task belongs to. How do you pass the project foreign key through Rails strong params?

{% include image_center_caption.html
    caption = "A project has many tasks."
    image = "/assets/images/2021/project_tasks_foreign_key.png"
%}

```haml
# tasks/new.html.haml
= simple_form_for @task do |form|
  = form.input :project_id, collection: Project.all.collect {|c| [c.name, c.id]}
  = form.input :title
  = form.button 'submit', class: 'btn btn-primary'
```
You want to send `:project_id` through the Rails form in this case. If you attempt to send `:project`, you'll get an error.

`Project.all.collect {|c| [c.name, c.id]}` maps each project into an array where the first element is the name and the last is the id. Rails form will display `name` as a dropdown for the user to select but will send the `id` to the create controller.

```ruby
# controllers/tasks_controller.rb

def create  
  @task = Task.new(task_params)  
  if @task.save  
    flash[:notice] = 'Task successfully created.'  
    redirect_to tasks_path  
  else  
    render :new  
  end  
end

private

def task_params  
  params.require(:task).permit(:title, :project_id)  
end
```

That's it.