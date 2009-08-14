require File.join(File.dirname(__FILE__), 'config', 'boot')

import File.join(SPREE_ROOT, 'Rakefile')


desc "do local upgrade and hide risky files"
task :upgrade => ["unhide_files", "spree:upgrade", "version", "hide_files"] do
  puts "Look for files with a '~' suffix."
  puts "These are the previous versions and might need to be reviewed/merged."
  puts "Then you might need to copy some other config files after merging etc:"
  puts "  * initializers/spree.rb-hide"
  puts "  * routes.rb-hide"
  puts "  * boot.rb"
  puts "  * and the environment(s) files"
end

desc "add some kind of time stamp"
task :version do
  edge_file = "#{SPREE_ROOT}/.git/refs/heads/master"
  if File.exist? edge_file
    version = `cat #{edge_file}`
  else
    version = `#{SPREE_ROOT}/bin/spree -v`
  end
  version = version.chomp + ' -- ' + Time.now.to_s
  File.open("version","w") {|f| f.write version}
end

desc "hide conflicting files"
task :hide_files do
  ["config/routes.rb", "config/initializers/spree.rb", "config/initializers/session_store.rb"].each do |f|
    File.rename(f, f + '-hide')
    backup = f + '~'
    File.rename(backup, f + '-hide~') if File.exist?(backup)
  end
end

desc "unhide conflicting files"
task :unhide_files do
  ["config/routes.rb", "config/initializers/spree.rb", "config/initializers/session_store.rb"].each do |f|
    File.rename(f + '-hide', f) if File.exist?(f + '-hide')
  end
end


