require 'rake'
require 'rake/testtask'
require 'rbconfig'

namespace :gem do
  desc "Remove any .gem files in the project"
  task :clean do
    Dir['*.gem'].each{ |f| File.delete(f) }
  end

  desc "Create the win32-security gem"
  task :create => [:clean] do
    spec = eval(IO.read('win32-security.gemspec'))
    Gem::Builder.new(spec).build
  end

  desc "Install the win32-security gem"
  task :install => [:create] do
    ruby 'win32-security.gemspec'
    file = Dir["*.gem"].first
    sh "gem install #{file}"
  end
end

namespace :test do
  Rake::TestTask.new(:security) do |t|
    t.verbose = true
    t.warning = true
    t.test_files = Dir['test/test_security.rb']
  end

  Rake::TestTask.new(:acl) do |t|
    t.verbose = true
    t.warning = true
    t.test_files = Dir['test/test_acl.rb']
  end

  Rake::TestTask.new(:sid) do |t|
    t.verbose = true
    t.warning = true
    t.test_files = Dir['test/test_sid.rb']
  end

  # ACL class isn't ready yet
  Rake::TestTask.new(:all) do |t|
    t.verbose = true
    t.warning = true
    t.test_files = Dir['test/test_sid.rb', 'test/test_security.rb']
  end
end

task :default => 'test:all'
