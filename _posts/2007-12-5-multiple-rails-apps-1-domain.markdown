--- 
layout: post
title: Multiple Rails Apps, 1 Domain
---
For development I have been using a VM these days with a web server hosting multiple apps under the same VHost via different directories.  What i need to use what this under my 'config/development.rb' files:

<pre>
<code>
ActionController::AbstractRequest.relative_root_url = '/app'
</code>
</pre>

Hope this saves some people time...
