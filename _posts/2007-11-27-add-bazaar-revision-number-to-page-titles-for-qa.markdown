--- 
layout: post
title: Add bzr revision number to page titles for QA
---
I came across a "little article":http://www.brynary.com/2007/8/30/add-svn-revision-number-to-page-titles by Brian Helmkamp on his blog.  I thought this was a good idea for SVN, so why not update it for my use with Bazaar?  Also, his fallback is to resort to the Capisrano revisions.log file, which is no longer in use with the release of 2.0, so I use the REVISION file.

<br>
Here is the snippet of Brian's original code:

<pre><code>
  def revision
    @revision ||= if svn_info_from_working_copy 
      svn_info_from_working_copy["Revision"].value
    else
      last_revision_in_log
    end
  rescue
    @revision = "UNKNOWN"
  end
  
  def svn_info_from_working_copy
    @svn_info ||= YAML.parse(`svn info #{RAILS_ROOT}`)
  end
  
  def last_revision_in_log
    File.readlines(RAILS_ROOT + "/../../revisions.log").last.split[3]
  end
  
</code></pre>

And here is my modified:

<pre><code>
  def revision
    @revision ||= if bzr_revno_from_working_copy 
      bzr_revno_from_working_copy
    else
      last_revision
    end
  rescue
    @revision = "UNKNOWN"
  end
  
  def bzr_revno_from_working_copy
    @bzr_revno ||= `bzr revno #{RAILS_ROOT}`
  end
  
  def last_revision
    File.read(RAILS_ROOT + "/REVISION").strip
  end
  
</code></pre>

Of course let's not forget his suggestion of using this in the title of the page:

<pre><code>
  <title>r<%= @revision  %> | ...Normal page title...</title>
  
</code></pre>

Thanks Brian!
