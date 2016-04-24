task default: %w[test]

task :test do
  sh 'jekyll build'
  sh 'htmlproofer ./_site'
end

task :server do
  sh 'jekyll serve -H 0.0.0.0 -w'
end
