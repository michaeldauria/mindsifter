--- 
layout: post
title: Generate Local Rails RDocs
---
As a follow up to my quick article on creating RDocs for the Ruby Core, you can very easily do the same for Rails and even have generate with Jamis' template.  It's as easy as:

<pre><code>
 $ rake rails:freeze:gems
 $ template='jamis' rake doc:rails
 
</code></pre>

Run *rake doc:rerails* if you have already created the Rails RDocs before.  You already froze Rails to your app for easier deployment right?
