task :default do
  puts "Available commands:"
  system "rake -T"
end

desc "Build the CSS"
file "assets/style.min.css" => ['assets/src/bootstrap.css', 'assets/src/bwp.css'] do
  puts "Minifying CSS"
  system "recess assets/src/bootstrap.css assets/src/bwp.css --compress > assets/style.min.css"
end

desc "Precompile all assets"
task :assets => ["assets/style.min.css"]

desc "Start a jekyll server with development configuration"
task :serve => [:assets] do
  exec "jekyll serve --config _config.yml,_config.dev.yml --watch"
end

desc "Build the website with production configuration"
task :build => [:assets] do
  system "jekyll build"
end

desc "Publish the website to the S3 server"
task :publish => [:build] do
  puts "Publishing to S3 ..."
  system "s3cmd sync --delete-removed --no-mime-magic --no-preserve --rr _site/ s3://bwp.io"
end
