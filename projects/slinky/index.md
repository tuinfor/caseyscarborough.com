---
layout: project
title: Projects &middot; Slinky Web Application
---

# Slinky Web Application

<i class="icon-cloud-download"></i> <a href="https://github.com/caseyscarborough/slinky/zipball/master">Download .zip</a> &nbsp; 
<i class="icon-cloud-download"></i> <a href="https://github.com/caseyscarborough/slinky/tarball/master">Download .tar.gz</a> &nbsp; 
<i class="icon-github"></i> <a href="https://github.com/caseyscarborough/slinky">View on GitHub</a>

Slinky is a URL Shortener web application written using Ruby 2.0 and Rails 3.2.13.

The application can be used and seen at [http://slnky.me/](http://slnky.me). The following is a screen capture of the application's homepage in it's current state.

![alt text][screenshot]

# Dependencies

This application uses the following system dependencies:

* Ruby 2.0.0 (possibly 1.9.3, but not tested)
* Rails 3.2.13
* PostgreSQL for production (not needed for development or testing)
* Other gems listed in [Gemfile](https://github.com/caseyscarborough/slinky/blob/master/Gemfile)


## Using the Application

If you'd like to run the application locally or contribute to the application, begin by cloning the application and installing necessary dependencies:

<pre class="no-highlight"><code><span class="dollar">$</span> git clone http://github.com/caseyscarborough/slinky.git
<span class="dollar">$</span> cd slinky
<span class="dollar">$</span> bundle install</code></pre>

Afterwards, create and migrate the database and fire up the rails development server.

<pre class="no-highlight"><code><span class="dollar">$</span> rake db:migrate
<span class="dollar">$</span> rails server
</code></pre>

Afterwards, navigate to [http://localhost:3000](http://localhost:3000) in your web browser to see the application in action.

## Configuring the Application

If you'd like to generate sample data for a user, you can do so by editing the [lib/tasks/sample_data.rake](https://github.com/caseyscarborough/slinky/blob/master/lib/tasks/sample_data.rake) file.

```ruby
# Generate first user, typically the one you'll use.
User.create(
  first_name: 'Casey', 
  last_name: 'Scarborough',
  email: 'casey@caseyscarborough.com',
  password: 'password',
  password_confirmation: 'password'
)

# Create links for each user in the system.
puts 'Generating links...'
User.all.each do |user|     
  15.times do |n|
    user.links.create!(
      short_url: Link.generate_short_link, 
      long_url: "http://" + Faker::Internet.domain_name, 
      total_clicks: rand(0..15),
      last_visited: rand(0..365).days.ago
    )
  end
end
```

Afterwards, you can add the sample data to the database by running the following command:

<pre class="highlight"><code class="bash"><span class="dollar">$</span> rake db:populate</code></pre>

## Running the Test Suite
The tests are built using the [RSpec](http://rspec.info/) testing framework and can be run by issuing the following commands from the project root:

<pre class="highlight"><code class="bash"># Prepare the database for testing
<span class="dollar">$</span> rake db:test:prepare

# Run the tests
<span class="dollar">$</span> rspec spec/
</code></pre>

## To-Do

* Upgrade project to Rails 4.0.
* Add link editing.
* Create logo.
* Add more features.


## Contributing

Please feel free to contribute to the application by following the steps below:

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request


[screenshot]: https://github.com/caseyscarborough/slinky/raw/master/app/assets/images/homepage.png "The application's main layout."