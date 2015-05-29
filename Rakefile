require 'rubygems'
require 'rake'
require 'fileutils'

desc "Draft a new post"
task :new do
  puts "What should we call this post for now?"
  name = STDIN.gets.chomp
  FileUtils.touch("drafts/#{name}.md")

  open("drafts/#{name}.md", 'a') do |f|
    
    f.puts "---"
    f.puts "layout: post"
    f.puts "title: \"DRAFT: #{name}\""
    f.puts "category: ???"
    f.puts "tags: blog"
    f.puts "year: #{Time.now.year}"
    f.puts "month: #{Time.now.month}"
    f.puts "day: #{Time.now.day}"
    f.puts "published: false"
    f.puts "summary: ???"
    f.puts "---"
  end
end


desc "Startup Jekyll"
task :start do
  sh "bundle exec jekyll server --watch"
end

task :default => :start

