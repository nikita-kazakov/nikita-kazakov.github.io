---
title: How Ruby on Rails Forms and Nested Forms Work.
date: 2020-12-19
layout: post
permalink: /forms-in-ruby-on-rails/
tags: 
    - ruby on rails
---

Forms are a huge part of a dynamic website. It’s through forms that you take user input and do something with it. It’s worth taking time to understand how to build different types of forms with rails.

# Forms for Models
You’ll store your data in the database. You’ll use rails models to work with database data. Let’s say you’re building a page that allows users to change their profile settings.

A person should be able to change things like their name, age. These fields are stored in the User table and accessible with the User model.

A `form_for` helper let's the user either:
- create a new record for a model in the database.
- update attributes of a specific model in the database.

The `form_for` method returns an html form object. Inside the `form_for` block, you'll use helper methods to add labels and fields to your form.

Let's create a user resource in `routes.rb` to give all REST routes.
```ruby
resources :users
```

Let's create a form that creates a user by taking the name attribute. One way we can do that is by calling `User.new` to create a blank User instance.

```haml
= form_for User.new do |form|
 = form.label :name
 = form.text_field :name
 = form.submit
```

This form use a POST http verb that routes to the create action in Rails. Let's create that action and put in a pry breakpoint to see what's happening.
```ruby
class UsersController < ApplicationController
  def create
    binding.pry
  end
end
```

Put in a name and submit the form. Let's jump into the pry console and see what's happening.

```bash
params
<ActionController::Parameters {"utf8"=>"✓", 
                               "authenticity_token"=>"C39DrozR2ODyI", 
                               "user"=>{"name"=>"Jack"}, 
                               "commit"=>"Create User", 
                               "controller"=>"users", 
                               "action"=>"create"} permitted: false>
```

params are fancy hashes that contain data that is passed back into the controller. Our form passed in `user` as a key with a hash value of `{"name"=>"Jack"}` to the params.

```bash
params[:user]   # like a ruby hash, call the user key to get the values
# => {"name"=>"Jack"}

params[:user][:name] # => "Jack"
```

We wanted to pass the users name and save the user. We have that information in the params. Let's save.

```ruby
  def create
      def create
        user = User.new # creates new instance of User
        user.name = params[:user][:name] # updated the name of the user object to what was passed in the params.
        user.save # save user to database.
      end
  end
```

Let's verify that it worked that that the user was saved through the rails console.
```ruby
rails console
User.count # 1
User.first # => id: 1, name: "Jack"
```

When you pass in a model instance as we did with `User.new`, the `form_for` helper will only accept attributes on that model.

```haml
= form_for User.new do |form|
 = form.label :name
 = form.text_field :name # This works because name is an attribute on User.
 = form.text_field :blah # This will NOT work because blah is not an attribute on User.
 = form.submit
```

# form_for object as string
Let's strip the magic of Rails down. You didn't have to pass in `User.new` as the object in the form. You could have passed in any symbol or string. Let's see that.

```haml
= form_for :whatever do |form|
  = form.label :name
  = form.text_field :name
  = form.submit
```

You could have also passed in `= form_for 'whatever' do |form|` as a string.

Take a look at your params in the create controller. You'll see that Rails passed in a `whatever` key with a value of `{"name"=>"Bill"}`. Let's use that to create the user.

```ruby
  def create
    user = User.new
    user.name = params[:whatever][:name]
    user.save
  end
```

Although you can pass in strings and symbols, you won't see often see this in real world rails applications.

# Expanding the form

Let's add age and email as fields in our form.

```haml
= form_for User.new do |form|
  = form.label :name
  = form.text_field :name

  = form.label :age
  = form.text_field :age

  = form.label :email
  = form.text_field :email

  = form.submit
```

Again, we'll use pry as a breakpoint so we can investigate what was passed to the params in the console.

```ruby
def create
  binding.pry
end 
```

You'll see that the form passed in a key of `user` with a value of `{"name"=>"Jack", "age"=>"15", "email"=>"jack@example.com"}`

```ruby
  def create
    user = User.new
    user.name = params[:user][:name]
    user.age = params[:user][:age]
    user.email = params[:user][:email]
    user.save
  end
```

I did the above scenarios in order to show you that forms don't have to be mystical. However, in real world Rails, you won't see the controller save model attributes like this. Imagine if there were twenty more attributes we had to save on the User. It would take a lot of typing to get there.

Rails magic comes in when we pass the entire user params hash to the User object and it updates all the passed values automatically.

```ruby
  def create
    user = User.new
    # Take the the entire hash value of `user` from params and update (saves to database) the user instance.
    user.update(params[:user])
  end
```

That is what you see used in real world rails. However, that gives us an error `ActiveModel::ForbiddenAttributesError: ActiveModel::ForbiddenAttributesError`.

# Strong Parameters

`ActiveModel::ForbiddenAttributesError` is there for good reason. Strong parameters were added to Rails to prevent from clients passing in unapproved parameters. We need to specifically permit parameters that we want to be passed into the User model.

We need to use two methods on params. The first is `permit` and the second is `require`.

```ruby
# Permit the name attribute to be saved from params.
params[:user].permit(:name)

# Permit name and age.
# Note that the output is the params with name and age only.
params[:user].permit(:name, :age)
```

Although it's enough to use `permit` to avoid the `ForbiddenAttributesError`, most Rails app go one step further. You can also specify which key from the params should be used by using `require` and then call `permit` on the specific values to be used.

```ruby
# notice that we call the entire params and the `require` calls the key.
params.require(:user).permit(:name, :age)
```

```ruby
def create
    user = User.new
    # Take the the entire hash value of `user` from params and update (saves to database) the user instance.
    user_params = params.require(:user).permit(:name, :age)
    user.update(user_params) # Success! Name and age are updated in 1 line.
end
```

Typically, the variable `user_params` is instead added as a private method in a Rails controller.

```ruby
def create
  user = User.new
  user.update(user_params)
end

private
def user_params
  params.require(:user).permit(:name, :age)
end
```

# Updating Models

Let's say we want to allow our users to change their name and age through a form. We'd have to call the correct instance of User and pass it into the `form_for` helper.

Many tutorials show you that forms are created on a 'new' page with a 'new' action. It doesn't matter where you create that form. Projects are not always as simple. Let's create a form to update a user on the Users index page.
Let's grab a user in our database and store it in `@user`:

```ruby
def index
  @user = User.first
end 
```

In our views, we'll pass in the `@user` instance variable that has the correct user selected.

Refresh your form and notice that Rails automatically loaded the correct name and age in the text fields! The submit button has also changed to say "Update User".

Let's change the name and hit submit. Uh oh. You get an error. Instead of going to the 'create' action, Rails is taking you to the 'update' action. It doesn't exist yet.

Why are we changing actions? When we create a resource, we use POST HTTP verb which routes to the 'create' action. When we passed in an existing user instance variable to `form_for`, Rails knows that your intention is to update that resource. The correct HTTP verb to update is PATCH, which takes you to the 'update' action in the User controller.

Let's create that action. Again, put in `binding.pry` in that action and try to submit and investigate what gets passed into the params.

```ruby
def update
  binding.pry
end
```

```bash
params
<ActionController::Parameters {"utf8"=>"✓", 
                               "_method"=>"patch", 
                               "authenticity_token"=>"JLyss4cBIK5/qkS", 
                               "user"=>{"name"=>"Jill", "age"=>"19", "email"=>"nothing@hi.com"}, 
                               "commit"=>"Update User", 
                               "controller"=>"users", 
                               "action"=>"update", 
                               "id"=>"2"} permitted: false>
```

You see the `user` key that has the updated user values. You also see the `id` of the User model that was update. That is what you're looking for.

```ruby
def update
  @user = User.find(params[:id])  # Find and load the user we're updating.
  @user.update(user_params)
end
```

That's it. That's all there is to updating an existing resource. Just pass in an instance variables of what you're updating to `form_for` and you're good to go.

# Form_for syntactic sugar

`form_for` somehow knew whether we were creating a resource or updating a resource. It added a lot of Rails magic to our form. Let's see what is possible to pass in manually to `form_for`.

When you write:
```ruby
form_for @user do |form|
```

Rails will actually run this:
```ruby
= form_for @user, as: :user, url: user_path(@user), method: :patch, html: {class: "edit_user", id: "edit_post_2"} do |form|
```

That's a mouthful. Let's break it down.
`as: :user` specified that the values passed the params will be stored in a `user` key. You'll be able to grab them with `params[:user]`.
`as: :whatever` will change that to `params[:whatever]`. I don't see a reason to do this.

`url: user_path(@user)` is telling the form to submit to this specific url.

`method: :patch` is very important. That's because if we take a look at all the routes `resource :user` has made for us, you'll notice the https verbs GET, PATCH, and DELETE are all on the user_path. In the case of deleting an object, you'll have to specify which method you're using. In our example, rails is specifically using the PATCH method to update the user resource.

You don't have to use all these options. You could, for example, use something like this:
```ruby
= form_for @user, url: user_custom_path do |form|
```

# Adding non-model fields to form_for

If you pass a model instance to `form_for`, it will allow you to create fields associated with that model. However, there are times when you want to collect information from users that's not mapped to the model.

```haml
= form_for @user do |form|
  = form.text_field :name
  = form.text_field :age
  = form.text_field :city # This won't work as it's not part of the User model.
```

We can use a few techniques to accomplish this:
- Field Tag
- Virtual Attributes

## Field Tag

You can use a field tag within `form_for` to collect fields that aren't relevant to the model. 

This is a powerful technique because in real world applications, forms aren't always limited to one model. Think about when you sign up for a service. You provide your name, email, address, payment information. All of that information should be stored on different tables in your database.

```haml
= form_for @user do |form|
  = form.text_field :name
  = form.text_field :age
  = form.fields_for :address do |f|
    = f.text_field :city
    = f.text_field :county
  = form.submit
```

Look at the params hash that is passed in. You'll see that a key of `address` with field values is passed into our user hash.
```bash
"user"=>{"name"=>"Jill", 
         "age"=>"43", 
         "address"=>
            {"city"=>"Brooklyn", 
             "county"=>"Nassau"}}, 
         "commit"=>"Update User", 
         "controller"=>"users", 
         "action"=>"update", 
         "id"=>"2"} permitted: false>
```

You can now grab those values and do whatever you want with them in the controller.

```ruby
params[:user][:address][:city] # => Brooklyn
params.require(:user).permit(:name, :age, address: {}) # Permit all the values in the address key.
params.require(:user).permit(:name, :age, address: (:city)) # Permit only city from the address key.
```

## Virtual Attributes

Let's say you need to pass in only one or two variables into the form. Since our `user.rb` is a Ruby file, we can simply create a virtual attribute without adding that attribute to the database.

An example where this can be used is to pass a payment token to the controller. A payment token is not a field on the User model.

Let's play around with this first.

```ruby
# In ruby.rb
attribute :payment_token
```

```bash
rails console
user = User.first
user.payment_token # nil
user.payment_token = 111 # We can set a value
user.payment_token # => 111 # We can get that value
```

```haml
= form_for @user do |form|
  = form.text_field :name
  = form.text_field :age
  = form.text_field :payment_token # It's a virtual attribute and should work.
  = form.submit
```

If you submit the form and check params, you'll see:
```haml
"user"=>{"name"=>"Jill", "age"=>"55", "payment_token"=>"912391823"}
```

## Hidden Fields

Isn't it weird to pass the payment token as a visible field? It shouldn't be visible to the client. In fact, the payment token isn't something that should be entered by the client.

We want to pass it in the form but keep it hidden. The client should not see the payment token input field. We can do this with a `hidden_field`.

```haml
= form_for @user do |form|
  = form.text_field :name
  = form.text_field :age
  = form.hidden_field :payment_token, value: "1111111111"
  = form.submit
```

# Nested Forms
Let's try building a complex form that updates two tables. I'm going to add an address table with a city, state, and user_id column.

## One to One Relationship Nested Form
```bash
rails g model address city:string state:string user:references
rails db:migrate
```

```ruby
class Address < ApplicationRecord
  belongs_to :user
end

class User < ApplicationRecord
  has_one :address
end
```

This form will have a one-to-one relationship. A user has one address and an address has one user. If we want rails to update the User model and the Address model at the same time, we need to add `accepts_nested_attributes_for` on the user.

```ruby
class User < ApplicationRecord
  has_one :address
  accepts_nested_attributes_for :address
end
```

The form is not going to be much different. We simply use a `fields_for` tag to pass in the `address` key with city and state values.
```haml
= form_for @user do |form|
  = form.text_field :name
  = form.text_field :age
  = form.fields_for :address do |f|
    = f.text_field :city
    = f.text_field :state
  = form.submit
```

What is the magic behind `accepts_nested_attributes_for`? By adding that method to User, Ruby writes a setter method on User. Here's what happens in the background

```ruby
class User < ApplicationRecord
  def address_attributes=(attributes)
  end
end
```

## One to Many Relationship Nested Form

Let's say a person has multiple addresses. There's not much of a change here.

```ruby
class User < ApplicationRecord
  has_many :addresses # Note it's plural
  accepts_nested_attributes_for :addresses # Note it's plural
end
```

Since `accepts_nested_attributes_for` takes a plural `addresses`, that means the underlying setter method Rails will use `addresses_attributes` is also plural. Because Rails is forgiving, they will also allow you to keep the singular way `address_attributes`.

```ruby
  def user_params
    params.require(:user).permit(:name, :age, addresses_attributes: {}) # make addresses_attributes plural
  end
```

The form stays the same! Rails will automatically iterate through the `fields_for :addreses` if there are multiple addresses in the database and you'll see multiple input fields in your form.

```haml
= form_for @user do |form|
  = form.text_field :name
  = form.text_field :age
  = form.fields_for :addresses do |f| # Will automatically iterate.
    = f.text_field :city
    = f.text_field :state
  = form.submit
```

Let's create another address in console.
```ruby
rails console
user = User.first
user.addresses.new(city: "san diego", state: "california")
```

Refresh the form and you'll see there are two iterations of the address fields. Make a change and submit the form. Add `binding.pry` in the update controller action and take a look at the params.

```bash
"user"=>{"name"=>"Stacy", 
         "age"=>"25", 
         "addresses_attributes"=>{
            "0"=>{"city"=>"San", "state"=>"CA", "id"=>"2"}, 
            "1"=>{"city"=>"san diego", "state"=>"california", "id"=>"3"}
          }
         }
```

The `addresses_attributes` key is has address keys of 0 and 1 passed with the different addresses. Notice how 0 and 1 also pass in an address id. If you pass in a new address into `addresses_attributes` hash without an id, Rails will know that this is a new address and it should save it. If an existing id is passed, Rails knows to try to find an address with that id and update it.

Adding an address into the `addresses_attributes` field without an id is useful when you want to edit a form and dynamically add another address using javascript. We'll look at that another time.

# Deeply Nested Forms

We can take form nesting even further. Let's say a user has_many addresses. Addresses have many phone numbers. Let's say we want to edit all of this in one form. I'm not saying this is an ideal idea. I think a form like this becomes too deeply nested. But it's possible to do.

Let's create a Phone resource that will create a Phone model and Phone controller.

```bash
rails g resource phone number:string
rails db:migrate
```

```ruby
class Address < ApplicationRecord
  belongs_to :user 
  has_many :phones
  accepts_nested_attributes_for :phones
end
```

Modify the form to add another `fields_for` tag for phones that is nested within the address `fields_for` tag.

```haml
= form_for @user do |form|
  = form.text_field :name
  = form.text_field :age
    
  = form.fields_for :addresses do |address_form|
    = address_form.text_field :city
    = address_form.text_field :state
    
    = address_form.fields_for :phones do |phone_form|
      = phone_form.text_field :number
    
  = form.submit
```

Submit the form and look at the params again. Notice that the phone attributes are NESTED within the address attributes hash. 

```bash
{"user"=> 
    {"name"=>"Stacy", 
    "age"=>"25", 
    "id" => "2"
    "addresses_attributes"=>
        {"0"=> {
        "city"=>"san diego", 
        "state"=>"california", 
        "id"=>"3", 
        "phones_attributes"=>
            {"0"=>{
                   "number"=>"2025551000", 
                   "id"=>"1"}
            }
        }
    }
}
```

Did you notice that we didn't have to update the user_params to include `phone_attributes`? Why does the form work without us needing to add `address_attributes`. 

```ruby
# The address_attributes: {} hash below is empty. It will accept ANYTHING that's added into it.
# Since phone_attributes is inside addresses_attributes, we don't need to manually add it.
def user_params
    params.require(:user).permit(:name, :age, addresses_attributes: {})
end
```

The more you play around with forms on your own time, the better you'll get applying them to real problems.