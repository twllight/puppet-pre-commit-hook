A Puppet pre-commit hook
========================

This is inspired/editted from the pre-commit hook found on the following blog: http://techblog.roethof.net/puppet/a-puppet-git-pre-commit-hook-is-always-easy-to-have/

All credits should really go to Ronny Roethof, I merely editted it and added some ERB template checking.

What does this do?
-----------------

For every commit you make into your repository, this script will check the syntax of your code (both Puppet (.pp) and Ruby Templates (.erb)) to make sure they are valid. This does not check the actual workings of your Puppet code, you should look into rspec or cucumber testing for that.

If any invalid syntax is found, it will abort the commit and you won't be able to commit your faulty code that will break production. Yay!

Installation
------------

Go to your git repository, create the file .git/hooks/pre-commit and place the content of this repo in it. Make it execute (chmod +x $file).

What does it look like ?
------------------------

Every commit will check the changed files and will report on them as such.

<pre> $ git commit modules/name/ -m "Your commit message"
### Checking puppet syntax, for science! ###
modules/name/manifests/init.pp looks good
modules/name/tests/init.pp looks good

### Checking if puppet manifests are valid ###
OK: modules/name/manifests/init.pp looks valid
OK: modules/name/tests/init.pp looks valid

### Checking if ruby template syntax is valid ###
Syntax OK
OK: modules/name/templates/template-file.erb looks like a valid ruby template

Everything looks good.
[develop adb6889] Your commit message
 3 files changed, 120 insertions(+)
  create mode 100644 modules/name/manifests/init.pp
  create mode 100644 modules/name/templates/template-file.erb
  create mode 100644 modules/name/tests/init.pp
</pre>
