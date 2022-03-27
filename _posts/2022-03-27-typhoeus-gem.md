---
title: Using Typhoeus for API calls in Ruby
date: 2022-03-27
layout: post
permalink: /typhoeus-gem
tags:
- ruby
---

I like using Typhoeus for making API calls in Ruby on Rails because the interface is simple. Here's how I use it.

Add it to your `GEMFILE` from [Typhoeus github page](https://github.com/typhoeus/typhoeus).

It's not what I'd prefer, but you could make GET requests like this:
```ruby
request = Typhoeus.get("www.google.com", followlocation: true)
```

I prefer to have one consistent way of doing things even if the syntax is a bit longer. Here's how I structure my API calls.

```ruby
request = Typhoeus::Request.new(url, options)
```

Let's make an API call to [icanhazdadjoke API](https://icanhazdadjoke.com/api):

```ruby
request = Typhoeus::Request.new(
  'https://icanhazdadjoke.com',
  method: :get,
  headers: { 'Accept': 'application/json', 'User-Agent': 'Bob Smith' },
  followlocation: true
)

response = request.run      # Makes the API call

# A few methods to analyze the response
response.body               # "{\"id\":\"KBsWnO711Dd\..." Returns JSON as string
response.code
response.headers

data = JSON.parse(response.body)   # Converts string to Ruby Object
data['joke']                       # The joke
```

Let's do another API call to [EventBrite API](https://www.eventbrite.com/platform/docs/events). You'll need your own private API key if you want to replicate this yourself. I'm going to create a wrapper class in the `app/lib` Rails folder.

```ruby
# app/lib/event_brite_api.rb

class EventBriteApi
  APIKEY = ENV['EVENTBRITE_API_KEY']
  BASE_URL = 'https://www.eventbriteapi.com/v3/events/'

  def initialize
  end

  def fetch_event(id)
    request = Typhoeus::Request.new(
      "#{BASE_URL + id.to_s}",
      followlocation: true,   # Without this, it won't redirect automatically
      method: :get,
      params: { expand: 'ticket_classes' },
      headers: { 'Authorization': "Bearer #{APIKEY}" }
    )

    JSON.parse(request.run.body)
  end
end
```

Let's go to Rails console `rails console` in the terminal and try it out.

```ruby
event_id = 86569213849
EventBriteApi.new.fetch_event(event_id)   # Returns JSON data
```

Note that I passed in params as an option in Typhoeus.

```ruby
request = Typhoeus::Request.new(
      "https://www.eventbriteapi.com/v3/events/",
      method: :get,
      params: { expand: 'ticket_classes' }
    )

# It would access params like this:
# https://www.eventbriteapi.com/v3/events/?expand=ticket_classes
```