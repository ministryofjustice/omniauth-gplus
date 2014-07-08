#!/usr/bin/env ruby
require 'bundler/gem_tasks'
require 'rake/clean'
require 'rake/testtask'
require 'yard'

begin
  Bundler.setup :default, :development
rescue Bundler::BundlerError => error
  $stderr.puts error.message
  $stderr.puts 'Run `bundle install` to install missing gems.'
  exit error.status_code
end

Bundler::GemHelper.install_tasks

desc 'Run all of the tests'
Rake::TestTask.new do |config|
  config.libs << 'test'
  config.pattern = 'test/**/*_test*'
end

desc 'Generate all of the docs'
YARD::Rake::YardocTask.new do |config|
  config.files = Dir['lib/**/*.rb']
end

begin
  require 'rubocop/rake_task'
  RuboCop::RakeTask.new
rescue LoadError
  task :rubocop do
    $stderr.puts 'Rubocop is disabled'
  end
end

desc 'Default: run tests, and generate docs'
task :default => [:test, :yard, :rubocop]
