
# Intro

This is a dummy extension for monitoring/including spree upgrades

The idea is that you run "rake upgrade" here from time to time - eg after a big spree upgrade, and 
get new versions of the asset/infrastructure files - which will then be copied into place or run 
in situ as appropriate. You don't have to run "rake spree:upgrade" in (each of) your projects 
any more, plus the changes you need to incorporate are more visible...

NOTE: you must run "rake upgrade", to avoid running spree's default task

# Usage 

I recommend this extension be loaded first (by mod. the config.extensions line in config/environment.rb): 
this allows any of your customizations to over-write the assets from this ext - which is what you'd want


(Pending a spree commit) The previous versions will be backed up with a ~ suffix (cf "cp -b") and you
will need to check whether any of the differences need to be patched into your customized files. 

# More detail

This started off as a blank spree project, and anything not needed to run "rake spree:upgrade" was 
removed. As a result of upgrade, some files are written back - most of which are kept.

* All assets in public/ are retained and will be copied in to place etc

* All "safe" initializer files are left here, and will be run when the extension is loaded

* spree.rb is needed to run the upgrade task, it seems - but can't be run from the extension, so 
  it is renamed to spree.rb-hide after the upgrade is done

* routes.rb is also needed, but also can't be run from the extension, so is also hidden

* session_store is also needed too (by environment.rb), and is hidden to avoid interference with your
  own file. Incidentally, the proper file is best moved to your site/config dir! 

* All of the other files directly in config/ (ie not initializers) are kept, eg environment.rb, 
  but you will need to process these by hand



