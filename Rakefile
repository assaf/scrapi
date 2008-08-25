require "benchmark"
require "rubygems"
Gem::manage_gems
require "rake"
require "rake/testtask"
require "rake/rdoctask"
require "rake/gempackagetask"


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

gem = Rake::GemPackageTask.new(spec) do |pkg|
  pkg.need_tar = true
  pkg.need_zip = true
end
