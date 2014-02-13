task :default do
  puts "Available commands:"
  system "rake -T"
end

### Assets

# Filenames of unfingerprinted assets
$assets = { :css => "assets/style.min.css" }

# Names that glob to fingerprinted assets
$wildcards = $assets.each_with_object({}) do |(k,v), h|
  (pre, post) = v.split '.', 2
  h[k] = "#{pre}-*.#{post}"
end

# CSS
desc "Build the CSS"
file $assets[:css] => ['assets/src/bootstrap.css', 'assets/src/bwp.css', 'assets/src/wombat.css'] do
  puts "Minifying CSS"
  system "recess assets/src/bootstrap.css assets/src/wombat.css assets/src/bwp.css --compress > #{$assets[:css]}"
  fingerprint_asset :css
end

# Global task for all assets
desc "Precompile all assets"
task :assets => $assets.values
task :assets => "_assets.yml"

### Fingerprinted assets

file "_assets.yml" do
  $assets.keys.each do |type|
    fingerprint_asset type
  end
end

# Dummy tasks (real tasks will be inserted below if needed)
task 'fingerprint:css'
# Set the prereq so that the fingerprint runs if necessary.
task :assets => ['fingerprint:css']

# Determine if fingerprinting needs run
namespace :fingerprint do
  # check that the fingerprinted assets exist, and if not, insert a task for that
  $assets.each do |type, filename|
    if Dir.glob($wildcards[type]).empty?
      task type do
        fingerprint_asset type
      end
    end
  end
end

def fingerprint_asset(type)
  require 'digest'
  require 'yaml/store'

  # determine the new fingerprinted filename
  filename = $assets[type]
  hash = Digest::MD5.file(filename).hexdigest
  (pre, post) = filename.split '.', 2
  fingerprinted_name = "#{pre}-#{hash}.#{post}"

  # copy the file
  system "rm -f #{$wildcards[type]}"
  system "cp #{$assets[type]} #{fingerprinted_name}"
  puts "Fingerprinting #{type} ==> #{fingerprinted_name}"

  # save the fingerprinted filename to yml file so that jekyll knows where to find it
  require 'yaml/store'
  YAML::Store.new("_assets.yml").transaction do |t|
    t[type.to_s] = fingerprinted_name
  end
end

### Development server

desc "Start a jekyll server with development configuration"
task :serve => [:assets] do
  exec "jekyll serve --config _config.yml,_assets.yml,_config.dev.yml --watch"
end

### Deployment

desc "Build the website with production configuration"
task :build => [:assets] do
  system "jekyll build --config _config.yml,_assets.yml"
end

require 'dotenv/tasks'
desc "Publish the website to the S3 server"
task :publish => [:build, :dotenv] do
  puts "Publishing to S3 ..."
  system "s3_website push"
end
