require 'html-proofer'

task :default => :test

task :test do
  sh 'jekyll build'
  HTMLProofer.check_directory('./_site', {
    :check_favicon => true,
    :check_html => true,
    :disable_external => true
  }).run
end

task :server do
  sh 'jekyll serve -H 0.0.0.0 -w'
end
