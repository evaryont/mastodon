begin
  require 'jeweler'
rescue LoadError
  puts "Jeweler not available, but is required. Install it with: sudo gem install jeweler"
  exit 1
end

@jtasks = Jeweler::Tasks.new do |gemspec|
  gemspec.name = "mastodon"
  gemspec.summary = "A ruby parser for todo.txt files"
  gemspec.description = "Mastodon: A ruby parser for todo.txt files.\n\nAnd the mastodon, like plain text, isn't extinct! (Yet.)"
  gemspec.email = "colin@evaryont.me"
  gemspec.homepage = "http://github.com/evaryont/mastodon/"
  gemspec.authors = ["Colin Shea"]
end
@jeweler = @jtasks.jeweler

namespace :version do
    desc "DON'T CALL. Write the version to lib/#{@jeweler.gemspec_helper.spec.name}/version.rb"
    task :ruby do
        # TODO: This is hard coded but it should be dynamic, given
        # the gem spec
        file = File.open("lib/#{@jeweler.gemspec_helper.spec.name}/version.rb", "w")
        # TODO: and so should this class template
        file.write <<-CLASS
# Automatically generated by `rake version:ruby' - use version:bump to change
# this, do not edit this directly, as it will be overwritten!
class #{@jeweler.gemspec_helper.spec.name.capitalize}
    VERSION = [#{@jeweler.major_version}, #{@jeweler.minor_version}, #{@jeweler.patch_version}]
end
CLASS
        system("git commit --file='.git/COMMIT_EDITMSG' --amend -q -o 'lib/#{@jeweler.gemspec_helper.spec.name}/version.rb'")
    end

    # Take advantage of Rake not overwriting tasks.
    #
    # After the 'real' task has been called, write version.rb as well.
    namespace :bump do
        task :major do
            Rake::Task["version:ruby"].execute
        end
        task :minor do
            Rake::Task["version:ruby"].execute
        end
        task :patch do
            Rake::Task["version:ruby"].execute
        end
    end
end

require 'rake/testtask'
Rake::TestTask.new do |t|
  t.libs = ["lib"]
  t.libs << "test"
  t.pattern = 'test/test_*.rb'
  t.verbose = true
end
