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
  sh 'jekyll serve --host 0.0.0.0 --port 4000 --watch --force_polling'
end
