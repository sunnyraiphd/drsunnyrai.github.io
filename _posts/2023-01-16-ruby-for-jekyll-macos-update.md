---
title: ruby for jekyll macos update
layout: post
categories:
- ruby
- jekyll
---

Here, I'm posting my solution for ruby / jekyll issue after MacOS update. I use jekyll for my website and few days back when I tried to update my website blog and executed `bundle exec jekyll serve`, I faced this issue.  I don't have the exact error messages. So **please decide for yourself**.

The error message suggested to execute `bundle install`.  However, this spiralled to other errors related to `unf_ext`, `commonmarker` and other packages suggesting `gem pristine` installs. On trying the suggested solutions, I eventually got a message about not having the right permissions. These are the links which I went through during my search:
* [Ruby on Mac](https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/)
* [Install Jekyll on Mac](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_install_jekyll_on_mac.html)

Finally, this is what I did:
* Check  `which ruby` and `which gem`
	* If it's system's ruby (/usr/bin/...), then you can simply install a local ruby with your choice of version. 
* Run `brew doctor`
	* It should return `Your system is ready to brew`. If any warnings are shown, first try to resolve them. In my case, I uninstalled `homebrew` completey using this [LINK](https://mac.install.guide/homebrew/5.html) and reinstalled using this [LINK](https://mac.install.guide/homebrew/index.html). 
	* Please follow the steps as described (1. [prepare your mac](https://mac.install.guide/homebrew/1.html), 2.  [Install Homebrew](https://mac.install.guide/homebrew/3.html)) Read the tutorials thoroughly as it requires update in `.zshrc` and `.zshprofile` files. 
	* Once this is done, check again `brew doctor` and verify that it returns `Your system is ready to brew`.
* Now, run `brew install ruby@3.0` or the version you prefer. If you run `brew install ruby`, then it installs `ruby@3.2` and eventually this will cause `tainted object` compatibility errors with jekyll theme. 
	* Pay attention to the messages displayed during installation. You will have to set paths as indicated in the messages. For instance, `echo 'export PATH="/opt/homebrew/opt/ruby@3.0/bin:$PATH"' >> ~/.zshrc`, `export LDFLAGS="-L/opt/homebrew/opt/ruby@3.0/lib" ` and `export CPPFLAGS="-I/opt/homebrew/opt/ruby@3.0/include"`
* Check `which ruby` and `which gem`
	* Now, you should see (/usr/local/....). If you still get paths such as /usr/bin/..., in that case, you have not set the paths in the above step.
	* At the end, you may also see a warning about `sassc` . Pay attention to this warning and accordingly add `gem 'sassc-rails'` in the gemfile in local repo 
* `gem install jekyll`
* `gem install bundler`
*  Move to your local repo path, and run `bundle update` and `bundle`
*  Finally, `bundle exec jekyll serve`

Hope it was helpful.
