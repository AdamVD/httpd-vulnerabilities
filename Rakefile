require 'rspec/core/rake_task'
require 'yaml'
require_relative 'spec/cve_spec.rb'

desc 'Run the specs by default'
task default: :spec

RSpec::Core::RakeTask.new(:spec)

namespace :cve do

  desc 'Use cve_spec and cve_helper to check incoming cve*** yaml files'
  task :check_new_cves do
    puts "Reading the ymls..."
    ruby 'cve_spec'
  end
end

namespace :git do

  desc 'Clone the HTTPD repo into ./tmp/src'
  task :clone do
    puts "Cloning httpd git repo..."
    Dir.chdir('./tmp') do
      puts `git clone https://github.com/apache/httpd.git src`
    end
  end

end

namespace :list do

  desc 'Use Git to list all of the files that were fixed from a vulnerability'
  task :vulnerable_files do
    puts "Getting fixes from ymls..."
    fixes = ListCVEData.new.get_fixes
    puts "Getting files from git"
    puts GitLogUtils.new('./tmp/src').get_files_from_shas(fixes).to_a
  end

end
