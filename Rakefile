require "rubygems"
require 'rake'

# template file used to generate test html
TPL = "_site/test-template/index.html"
# test file generated by :test task
TST = "tests.html"

# test building helper
module Py
    class Test

        def self.get_template
            puts "Copy #{TPL} content"
            File.read(TPL)
        end

        def self.build_jekyll
            puts "Building Jekyll"
            system "jekyll build --config _config.yml,_config_dev.yml"
        end

    end
end

task :default => :test

# Usage: rake test
desc "Generates test page"
task :test do

    # build jekyll site for first time
    Py::Test.build_jekyll

    # copy TPL content
    template = Py::Test.get_template

    # delete target file (TST) if exist
    if File.exist?(TST)
        puts "#{TST} exists deleting it"
        rm TST
    end

    # create new target file (TST)
    puts "Creating #{TST} file"

    open(TST, 'w') do |post|
        post.puts "---"
        post.puts "layout: default"
        post.puts "menu: main"
        post.puts "title: Tests"
        post.puts "weight: 30"
        post.puts "---"
        post.puts template
    end

    # build jekyll again
    Py::Test.build_jekyll

    puts "task :test END ------------"
end # task :post


