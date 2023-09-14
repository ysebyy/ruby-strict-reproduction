## Env details

* .ruby-version - 3.1.2
* Bundler version - 2.3.7
* Renovate version used - 36.92.0

## Steps to recreate

* Gemfile currently has ddtrace version  ~> 0.9.0
* Update Gemfile ddtrace to version ~> 0.14.0 (as it was suggested by Renovate)
* Execute the same command as suggested by renovate: ` bundler lock --minor --strict --update ddtrace`
* We should see an error due to not being able to update libdatadog.  
* To update the library, we use the following command: ` bundler lock --minor --conservative --update ddtrace` 
* `git diff Gemfile.lock` shows libdatadog and ddtrace updated just fine. 

## The issue

* Renovate runs --strict flag while updating minor version for library which requires update on certain dependencies
* --strict: This flag ensures that only the gem you specify is updated to its latest version, without updating any of its dependencies.
* Adding renovate option ` "postUpdateOptions": ["bundlerConservative"] ` adds the --conservative flag as the logs suggest by Renovate: ` {"cmd":"/bin/sh -c bundler lock --minor --strict --conservative --update ddtrace" `, however, due to appending --strict flag, the error persists


