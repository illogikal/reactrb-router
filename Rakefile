require "bundler/gem_tasks"

require 'bundler'
Bundler.require
Bundler::GemHelper.install_tasks


require 'rspec/core/rake_task'
require 'opal/rspec/rake_task'

RSpec::Core::RakeTask.new('ruby:rspec') do |s|
  s.rspec_opts = "--tag ruby"
end
Opal::RSpec::RakeTask.new('opal:rspec') do |s|
  s.append_path 'spec/vendor'
  s.index_path = 'spec/index.html.erb'
end

task :test do
  Rake::Task['ruby:rspec'].invoke
  Rake::Task['opal:rspec'].invoke
end

require 'generators/reactive_ruby/test_app/test_app_generator'
desc "Generates a dummy app for testing"
task :test_app do
  ReactiveRuby::TestAppGenerator.start
  puts "Setting up test app database..."
  system("bundle exec rake db:drop db:create db:migrate > #{File::NULL}")
end

task default: [ :test ]
