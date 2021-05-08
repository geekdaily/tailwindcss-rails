# Tailwind CSS Rails

The `tailwindcss` gem helps you to easily install the Tailwind CSS framework by using WebPack and the `webpacker` gem.

Note: this is a fork of [the original](https://github.com/IcaliaLabs/tailwindcss-rails) which seems unmaintained at the moment. It does three things differently:

1. Updates to Tailwind CSS 2.1.2
2. Syncs the gem version with the version of Tailwind CSS
3. Changes the gem dependency to `railties ~> 6` to force working with modern Rails

If you're not already locked into this gem, you should consider a [the better maintained official Rails tailwindcss-rails gem](https://github.com/rails/tailwindcss-rails) ... which I didn't discover until I'd cleaned this up already, so I'll share and immediately abandon them. I'm not even cleaning up the rest of this README.

## Table of contents

- [Installing the gem](#installing-the-gem)
- [Contributing](#contributing)
- [License](#license)
- [Code of conduct](code-of-conduct)



## Installing the gem

In order to run the install generator from `tailwindcss` you need to add the [webpacker](https://github.com/rails/webpacker) gem, and run the installation setup for it.



#### Installing webpacker + tailwindcss

tailwindcss-rails ~> 1.0.0 supports Rails ~>5.2.0 and tailwindcss ~> 1.0

You first need to add the following gems to your `Gemfile`:

```
# Gemfile
gem 'webpacker', '~> 4.0.0'
gem 'tailwindcss', '~> 1.0.0'
```

Run the following:

```shell
bundle

bundle exec rails webpacker:install

bundle exec rails g tailwindcss:install
```

This will prepare the application to use tailwind by:

1. Adding tailwind by using `yarn`
2. Create a `javascript/css` directory
3. Init tailwind from the `node_modules`
4. Setup tailwind
5. Configure `postcss.config.js` file

If you want to know how this is achieved, you can go [here](https://github.com/IcaliaLabs/tailwindcss-rails/blob/master/lib/generators/tailwindcss/install_generator.rb).

These two lines will compile the assets from the `app/javascript/css` folder.

You must add the following to your `config/initializers/content_security_policy.rb`:
```ruby
  Rails.application.config.content_security_policy do |policy|
    policy.connect_src :self, :https, 'http://localhost:3035', 'ws://localhost:3035' if Rails.env.development?
  end
```

Inside of `config/webpacker.yml`, you must set `extract_css: true` default is `false`.

You have to add these two lines to your `application` layout in order to compile it.

```ruby
<%= stylesheet_pack_tag    'application' %>
<%= javascript_pack_tag 'application' %>
```

Webpacker will automatically compile your assets while a `bundle exec rails s` is active.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/IcaliaLabs/tailwindcss-rails. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Tailwindcss project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/tailwindcss/blob/master/CODE_OF_CONDUCT.md).
