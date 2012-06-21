$LOAD_PATH.unshift(File.dirname(__FILE__))

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new do |t|
end

task :install do
  rm_rf "*.gem"
  puts `gem build typhoeus.gemspec`
  puts `gem install typhoeus-*.gem`
end

task :release => :build do
  system "git tag -a v#{Typhoeus::VERSION} -m 'Tagging #{Typhoeus::VERSION}'"
  system "git push --tags"
  system "gem push typhoeus-#{Typhoeus::VERSION}.gem"
end

desc "Start up the test servers"
task :start do
  require 'spec/support/boot'
  begin
    Boot.start_servers(:rake)
  rescue Exception
  end
end

desc "Build Typhoeus and run all the tests."
task :default => [:spec]
