require 'rake/testtask'
require 'rake/clean'

# rule to build the extension
file 'ext/hola_ext.so' => %w(ext/extconf.rb ext/hola_ext.c) do
  Dir.chdir('ext') do
    ruby "extconf.rb"
    sh "make"
  end
end

# build the extension automatically (if needed) when running tests
task :test => 'ext/hola_ext.so'

# 'rake clean' and 'rake clobber' get rid of generated files
CLEAN.include('ext/*{.o,.log}')
CLEAN.include('ext/Makefile')
CLOBBER.include('ext/*.so')

# tell TestTask to look in 'ext' for 'hola_ext'
Rake::TestTask.new do |t|
  t.libs.push 'test', 'ext'
end

desc "Run tests"
task :default => :test
