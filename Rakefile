require "benchmark"
require "rubygems"
require "rake"
require "rake/testtask"
require "rake/rdoctask"


spec = Gem::Specification.load(File.join(File.dirname(__FILE__), 'scrapi.gemspec'))

desc "Generate documentation"
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = "rdoc"
  rdoc.title    = "Scraper"
  rdoc.options << "--line-numbers"
  rdoc.options << "--inline-source"
  rdoc.rdoc_files.include("README.rdoc")
  rdoc.rdoc_files.include("lib/**/*.rb")
end


desc "Run all tests"
Rake::TestTask.new(:test) do |test|
  test.libs << "lib"
  test.pattern = "test/**/*_test.rb"
  test.verbose = true
end
task :default=>:test


spec = Gem::Specification.load(Dir["*.gemspec"].first)

desc "Build the Gem"
task :build do
  sh "gem build #{spec.name}.gemspec"
end

desc "Install #{spec.name} locally"
task :install=>:build do
  sudo = "sudo" unless File.writable?( Gem::ConfigMap[:bindir])
  sh "#{sudo} gem install #{spec.name}-#{spec.version}.gem"
end

desc "Push new release to gemcutter and git tag"
task :push=>["test", "build"] do
  sh "git push"
  puts "Tagging version #{spec.version} .."
  sh "git tag v#{spec.version}"
  sh "git push --tag"
  puts "Building and pushing gem .."
  sh "gem push #{spec.name}-#{spec.version}.gem"
end
