require 'rubygems'
require 'rake/clean'
require 'rake/gempackagetask'
require 'rake/rdoctask'
require 'rake/testtask'
require 'rdoc/rdoc'

#include FileUtils::DryRun

PROJECT_NAME = "rubyjedi-testunitxml"
PACKAGE_VERSION = "0.1.5"
PACKAGE_FILES = FileList["README", "CHANGES", "MIT-LICENSE", "{docs,lib,test}/**/*"].exclude("rdoc").to_a

SRC = FileList["README", "CHANGES", "MIT-LICENSE", "lib/**/*.rb"]
CLOBBER << FileList["docs/html"]

desc "Generate documentation"
task :rdoc => [:clobber, :test]do
  begin
    r = RDoc::RDoc.new
    args = %W[-o docs/html -m #{SRC[0]} -T html] + SRC
    r.document(args)
  rescue RDoc::RDocError => e
    $stderr.puts e.message
  end
end

# Create a task named 'test'
Rake::TestTask.new do |t|
  t.libs << "test"
  t.test_files = FileList['test/tc_*.rb']
  t.verbose = true
end

#Rake::PackageTask.new(PROJECT_NAME, PACKAGE_VERSION) do |p|
#  p.need_tar = true
#  p.need_zip = true
#  #p.package_files.include("lib/**/*.rb")
#  p.package_files.include(PACKAGE_FILES)
#end


# Add a task for creating GEM packages
spec = Gem::Specification.new do |s|
  s.name         = PROJECT_NAME
  s.version      = PACKAGE_VERSION
  s.author       = "Henrik Martensson, Laurence A. Lee"
  s.email        = "self@henrikmartensson.org, lalee@pobox.com"
  s.homepage     = "http://wiki.github.com/rubyjedi/testunitxml/"
  s.platform     = Gem::Platform::RUBY
  s.summary      = "Unit test suite for XML documents"
  s.description  = "Test::Unit::XML extends the Test::Unit framework with an assertion for testing well-formed XML documents"
  s.files        = PACKAGE_FILES
  s.require_path = "lib"
  s.test_file    = "test/ts_testunitxml.rb"
  s.has_rdoc     = true
#  s.extra_rdoc_files = ["README"]
end

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.need_zip = true
  pkg.need_tar = true
end
