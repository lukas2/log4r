require 'rubygems'
require 'rake/gempackagetask'
require 'rubygems/specification'
require 'date'
require 'fileutils'

GEM = "log4r"
GEM_VERSION = "2.0.0"
AUTHOR = "Revolution Health"
EMAIL = "rails-trunk@revolutionhealth.com"
HOMEPAGE = %q{http://github.com/revolutionhealth/log4r/tree/master}
SUMMARY = "Updated version of Log4r"

spec = Gem::Specification.new do |s|
  s.name = GEM
  s.version = GEM_VERSION
  s.platform = Gem::Platform::RUBY
  s.has_rdoc = false
  s.extra_rdoc_files = ["README", "LICENSE", 'TODO']
  s.summary = SUMMARY
  s.description = s.summary
  s.author = AUTHOR
  s.email = EMAIL
  s.homepage = HOMEPAGE
  
  # Uncomment this to add a dependency
  # s.add_dependency "foo"
  
  s.require_path = 'lib'
  s.autorequire = GEM
  s.files = %w(LICENSE README Rakefile TODO log4r_original_LICENSE) + Dir.glob("{lib,specs,test,config}/**/*")
end

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.gem_spec = spec
end

desc "install the gem locally"
task :install => [:package] do
  sh %{sudo gem install pkg/#{GEM}-#{GEM_VERSION}}
end

desc "create a gemspec file"
task :make_spec do
  File.open("#{GEM}.gemspec", "w") do |file|
    file.puts spec.to_ruby
  end
end

require 'test/unit'
 
task :test do
 FileUtils.mkdir(File.join(File.dirname(__FILE__), %w[log])) if !File.exists?(File.join(File.dirname(__FILE__), %w[log]))
 FileUtils.rm(Dir.glob(File.join(File.dirname(__FILE__), %w[log *])))
 runner = Test::Unit::AutoRunner.new(true)
 runner.to_run << 'test'
 runner.pattern = [/_test.rb$/]
 exit if !runner.run
end
 
task :default => [:test, :package] do
end
