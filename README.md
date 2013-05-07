# selenium-webdriver for chromedriver2

This gem provides nescessary changes to selenium-webdriver to allow selenium to work with chromedriver2

Changes needed inside your code, if you want to use chromedriver2 instead of the chromedriver:

1. Use the modified chromedriver-helper:

https://github.com/sztupy/chromedriver-helper

The modified chromedriver-helper will download the latest chromedriver2 instead of the legacy chromedriver

2. Set `:detach => :unspecified` inside the webdriver's constructor. Without this, the current chromedriver2 instance
won't start up

3. Instead of profiles, you have to set prefs.

So for example when using Capybara you have to change this

    profile = Selenium::WebDriver::Chrome::Profile.new
    profile["download.default_directory"] = '/tmp'
    Capybara::Selenium::Driver.new(app, :browser => :chrome, :profile => profile)

to this

    prefs = {"download" => {"default_directory" => '/tmp'}}
    Capybara::Selenium::Driver.new(app, :browser => :chrome, :prefs => prefs, :detach => :unspecified)

and it will load up chromedriver2 instead of the legacy one

Old README follows:

# selenium-webdriver

This gem provides Ruby bindings for WebDriver and has been tested to work on MRI (1.8.7 through 2.0), JRuby and Rubinius.

## Install

    gem install selenium-webdriver

## Links

* http://rubygems.org/gems/selenium-webdriver
* http://selenium.googlecode.com/git/docs/api/rb/index.html
* http://code.google.com/p/selenium/wiki/RubyBindings
* http://code.google.com/p/selenium/issues/list

## License

Copyright 2009-2013 Software Freedom Conservancy

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

