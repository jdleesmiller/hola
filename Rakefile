require 'rake/testtask'
require 'rake/clean'

NAME = 'hola'

# rule to build the extension: this says that the extension should be
# rebuilt after any change to the source files in ext
file "lib/#{NAME}/#{NAME}.so" => Dir.glob("ext/#{NAME}/*{.rb,.c}") do
  # this does essentially the same thing as rubygems does
  Dir.chdir("ext/#{NAME}") do
    ruby "extconf.rb"
    sh "make"
  end
  cp "ext/#{NAME}/#{NAME}.so", "lib/#{NAME}"
end

# make the :test task depend on the shared object, so it will be built
# automatically before running the tests
task :test => "lib/#{NAME}/#{NAME}.so"

# use 'rake clean' and 'rake clobber' to easily delete generated files
CLEAN.include('ext/**/*{.o,.log,.so}')
CLEAN.include('ext/**/Makefile')
CLOBBER.include('lib/**/*.so')

# the same as before
Rake::TestTask.new do |t|
  t.libs << 'test'
end

desc "Run tests"
task :default => :test
