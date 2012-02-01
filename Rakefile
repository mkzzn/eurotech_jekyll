desc "Parse haml layouts"
task :parse_haml do
  print "Parsing Haml layouts..."
  system(%{
    cd _layouts/haml && 
    for f in *.haml; do [ -e $f ] && haml $f ../${f%.haml}.html; done
  })
  puts "done."
end

desc "Launch preview environment"
task :preview do
  Rake::Task["parse_haml"].invoke
  system "jekyll --auto --server"
end

desc "Build site"
task :build do |task, args|
  Rake::Task["parse_haml"].invoke
  system "jekyll"
end

desc "Package app for production"
task :package do
  ENV['JEKYLL_ENV'] = 'production'
  
  Rake::Task["build"].invoke

  print "Compressing assets..."
  system "jammit -o assets -c _assets.yml"
  puts "done."
end

desc "Deploy latest code in _site to production"
task :deploy do
  system(%{
    rsync -avz --delete _site/ mz@doblock2:/var/www/eurotech/
  })
end
