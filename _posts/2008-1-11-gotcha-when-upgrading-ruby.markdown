--- 
layout: post
title: Gotcha When Upgrading Ruby
---
I decided to upgrade my ruby version from 1.8.5 p114 to 1.8.6 p111 today and came across an error when I tried to run "merb":http://merbivore.com.  Whenever I would try and run the *merb* command witihin my project it would get as far as "Compiling routes...", then just stop output.  I decided to install *rdebug* to inspect:

<pre><code>
 $ sudo gem install rdebug
</code></pre>

Then I could check out where it was failing:

<pre><code>
 merb_project_dir:$ rdebug -d -x ./script/merb
</code></pre>

I use *./script/merb* here because I had frozen merb to the project so I poke around a bit.  After a solid minute of output, there was something that stood out:

<pre><code>
 bad version, 1.8.6 != 1.8.5
</code></pre>

This might not trigger anything to you at first glance, but some of the "rubygems":http://rubygems.org you depend on are actually compiled to the version of ruby that you have.  Offhand I can think of *mysql, datamapper, sqlite3, do_mysql, do_sqlite3*, and of course the reason merb was failing, *RubyInline and ParseTree*.  Once I reinstalled these two i was golden:

<pre><code>
 $ sudo gem install RubyInline ParseTree
</code></pre>

Shoot me a comment if you ran into this as well because I couldn't find anythnig on Google.
