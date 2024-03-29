# -*- coding: utf-8 -*-
source :rubygems

gem "rails", "2.3.14"

gem "coderay", "~> 1.0.0"
gem "i18n", "~> 0.8.0"
gem "rubytree", "~> 0.5.2", :require => 'tree'
gem "rdoc", ">= 2.4.2"
gem "liquid", "~> 2.3.0"
gem "acts-as-taggable-on", "= 2.1.0"
gem 'gravatarify', '~> 3.0.0'
# Needed only on RUBY_VERSION = 1.8, ruby 1.9+ compatible interpreters should bring their csv
gem "fastercsv", "~> 1.5.0", :platforms => [:ruby_18, :jruby, :mingw_18]
gem "tzinfo", "~> 0.3.31" # Fixes #903. Not required for Rails >= 3.2

group :test do
  gem 'shoulda', '~> 2.10.3'
  # Shoulda doesn't work nice on 1.9.3 and seems to need test-unit explicitely…
  gem 'test-unit', :platforms => [:mri_19]
  gem 'edavis10-object_daddy', :require => 'object_daddy'
  gem 'mocha'
  gem 'capybara'
end

group :ldap do
  gem "net-ldap", '~> 0.3.1'
end

group :openid do
  gem "ruby-openid", '~> 2.1.4', :require => 'openid'
end

# Use the commented pure ruby gems, if you have not the needed prerequisites on
# board to compile the native ones.  Note, that their use is discouraged, since
# their integration is propbably not that well tested and their are slower in
# orders of magnitude compared to their native counterparts. You have been
# warned.

platforms :mri, :mingw, :rbx do
  group :mysql2 do
    gem "mysql2", "~> 0.2.7"
  end

  group :postgres do
    gem "pg"
    #   gem "postgres-pr"
  end
end

platforms :mri_18, :mingw_18 do
  group :mysql do
    gem "mysql"
    #   gem "ruby-mysql"
  end

  group :sqlite do
    gem "sqlite3-ruby", "< 1.3", :require => "sqlite3"
  end
end

platforms :mri_19, :mingw_19, :rbx do
  group :sqlite do
    gem "sqlite3"
  end
end

# Load a "local" Gemfile
gemfile_local = File.join(File.dirname(__FILE__), "Gemfile.local")
if File.readable?(gemfile_local)
  puts "Loading #{gemfile_local} ..." if $DEBUG
  instance_eval(File.read(gemfile_local))
end

# Load plugins' Gemfiles
["plugins", "chiliproject_plugins"].each do |plugin_path|
  Dir.glob File.expand_path("../vendor/#{plugin_path}/*/Gemfile", __FILE__) do |file|
    puts "Loading #{file} ..." if $DEBUG # `ruby -d` or `bundle -v`
    instance_eval File.read(file)
  end
end
