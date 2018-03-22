# frozen_string_literal: true
require "bundler/gem_tasks"
require "rake/testtask"

sources = Dir["lib/licensed/source/*.rb"].map { |f| File.basename(f, ".*") }

namespace :test do
  Rake::TestTask.new(:core) do |t|
    t.description = "Run source-agnostic tests"
    t.libs << "test"
    t.libs << "lib"
    t.test_files = FileList["test/**/*_test.rb"].exclude("test/source/*_test.rb")
  end

  sources.each do |source|
    Rake::TestTask.new(source.to_sym) do |t|
      t.description = "Run #{source} tests"
      t.libs << "test"
      t.libs << "lib"
      t.test_files = FileList["test/source/#{source}_test.rb"]
    end
  end
end

Rake::TestTask.new(:test) do |t|
  t.libs << "test"
  t.libs << "lib"
  t.test_files = FileList["test/**/*_test.rb"]
end

task default: :test
