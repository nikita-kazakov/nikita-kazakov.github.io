---
title: Join tables in Rails
date: 2023-03-02
layout: post
permalink: /join-tables-in-rails
tags:
- ruby on rails
---

Let's say you have a users table and a shows table. A user `has_many` shows and a show can `have_many` users. You'd need to set up a join table for this.

{% include image_center_caption.html
    caption = "Join table for users and shows."
    image = "/assets/images/2023/users_shows_db.png"
%}

In our example, we'll first generate a join table migration by running `rails generate migration add_users_shows_join_table` in the terminal.

```ruby
class AddUsersShowsJoinTable < ActiveRecord::Migration[7.0]  
  def change  
      create_table :users_shows do |t|  
          t.references :user  
          t.references :show  
      end
  end  
end
```

I'd rather use a `has_many :through` association. I'm going to create a model for the `users_shows` table. The tricky part is that the model has to be singular. The table is `users_shows` but the model has to be called `users_show.rb`.

```ruby
# users_show.rb
class UsersShow < ApplicationRecord  
  belongs_to :user  
  belongs_to :show  
end

# user.rb
class User < ApplicationRecord  
  has_many :users_shows  
  has_many :shows, through: :users_shows  
end

# show.rb
class Show < ApplicationRecord  
  has_many :users_shows  
  has_many :users, through: :users_shows  
end
```
