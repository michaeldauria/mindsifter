--- 
layout: post
title: Add hg revision number to page titles for QA
---
<p>Recently after my article about Bazaar I switched to Mercurial.  Bazaar is just WAY too slow for remote repositories, which is what I use so my partner can pull changes, whereas Mercural is very fast.  Now let me show you how to go from the SVN code to Mercurial this time.</p>
<br>
<p>Here is the snippet of Brian's original code:</p>

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

<p>And here is my modified:</p>

<pre><code>
  def revision
    @revision ||= if hg_log_from_working_copy 
      hg_log_from_working_copy['changeset'].value.split(':').first
    else
      last_revision
    end
  rescue
    @revision = "UNKNOWN"
  end
  
  def bzr_revno_from_working_copy
    @hg_log ||= YAML.parse(`hg log #{RAILS_ROOT}`)
  end
  
  def last_revision
    File.read(RAILS_ROOT + "/REVISION").strip
  end
  
</code></pre>

<p>Bazaar made this easier, but the remote repository performance is just too subpar for my use.  So there you have it, enjoy.</p>
