--- 
layout: post
title: Generate Local Ruby Core RDocs
---
I like being able to go to "ruby-doc.org/core":http://ruby-doc.org/core if i want to look up some Ruby 1.8 docs, but what if you don't have the internet?  I always compile Ruby myself so I can have the latest security fixes and after I compile I always issue a:

<pre><code>
 $ rdoc --template=jamis --op <some output dir>

</code></pre>

That gives me a local copy of the RDocs so  can serve it up via a webserver and look up whatever I desire without the internet, pretty neat.  Oh that *--template=jamis* bit comes from Jamis' awesome RDoc template that he made in 2005 for use with the Rails RDocs.  For its use, take a look at the "original article":http://weblog.jamisbuck.org/2005/4/8/rdoc-template from the man himself.
