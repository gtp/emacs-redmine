emacs-redmine
=============
An emacs interface to work with redmine from emacs.

This package is a collection of tools based on a number of other
packages which enable creating, editing and deleting redmine issues.

It would suit a developer who wants to view, edit and close redmine
issues without using the web interface. It's significantly faster than
using redmine, and easy to tweak to your specific preferences, albeit
some lisp and/or python required for customisation.

Also I use the redmine-backlogs plugin, so where this document uses
the word 'sprint', it refers to the redmine-backlogs meaning of the word.

Acknowledgements
----------------
The emacs editing interface is based on the one written for http://ditz.rubyforge.org/ (a command line editing issue tracker)

The redmine api is from http://code.google.com/p/pyredminews with some changes.

Install
-------
git clone this repo and then add to .emacs file like this:

    (add-to-list 'load-path "path/to/emacs-redmine")
    (require 'redmine)

Then add one or more functions to .emacs for each project you want to access, for example:

    (defun redmine-my-project ()
      (interactive)
      (setq redmine-program "/path/to/emacs-redmine/redmine.py")
      (setq redmine-project-name "my-project")
      (setq redmine-login-key "myuniquekey##XX##XX")
      (setq redmine-url "http://www.somewhere.com/redmine")
      (redmine-show-sprints))

where:

      redmine-program : this is the redmine.py file inside this git repo
      redmine-project-name : the name of the redmine project to manage
      redmine-url : the url of the redmine login page
      redmine-login-key : your personal login key, which you get from redmine itself on the accounts tag. If you can't see it, then the redmine admin needs to enable API access for the project.

Configuration
-------------
The system needs to know the database ids of your different states and
trackers, edit the settings.py file to change them.

Usage
-----
run your command, eg

  M-x redmine-my-project

You will see a list of sprints (at the moment you need to create sprints on the redmine frontend), for example:

     Sprints for my-project:
     (press 'r' to show issues for the sprint, 'o' to show sprint in org mode )


       :23: (open) sprint1 
       :24: (open) sprint2 


Move the cursor over any sprint and press 'r'
You will now see the issues, for example:

    (list of keyboard shortcuts at the end of this buffer)


      :issue397: (New) do stuff
      :issue389: (New) do more stuff
      :issue386: (dev-done) do even more stuff

    ---------------------------
    Shortcut Keys:
      g : refresh
      s : show issue information
      A : add new issue
      e : edit issue
      j : add journal entry
      d : delete issue
      C-c n : set status to new
      C-c d : set status to devdone
      C-c r : set status to reopened
      C-c t : set status to tested


Then move the cursor over any issue and press one of the keyboard shortcuts to do something.

Org-mode
--------
There's an option to dump all the sprints and all issues into an org
file. This is really slow at the moment, but it's kind of nice
sometimes. It would be even nicer to be able to edit the org-file and
refresh redmine with it. The project
https://github.com/gongo/org-redmine seems to be working on that.

Todo
----
- ability to create/delete/edit sprints
- ability to move issues up and down in priority (specifically for use with redmine-backlogs)
- detection of available issue states instead of hard-coded
- better support for editing multi-line issue descriptions
- display and editing story points
- org-mode integration

Code style disclaimer
---------------------
redmine.el is awash with obsolete code, sorry about that. One day i'll
clean it up, mostly remnants of different versions of this same emacs
interface thingy that I've used over time.
