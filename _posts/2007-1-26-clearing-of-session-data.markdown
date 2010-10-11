--- 
layout: post
title: Clearing of Session Data
---
You can do it this way:
<pre><code>
  class SessionCleaner
    def self.remove_stale_sessions
      CGI::Session::ActiveRecordStore::Session.
        destroy_all( ['updated_on < ?', 20.minutes.ago] ) 
    end
  end

</code></pre>

Then just call via cron:
<pre><code>
  */10 * * * * ruby /full/path/to/script/runner 
     -e production "SessionCleaner.remove_stale_sessions"

</code></pre>

Above was found via: http://www.realityforge.org/articles/2006/03/01/removing-stale-rails-sessions

Or you can do it all one 1 line:

<pre><code>
  */5 * * * *  ruby /full/path/to/script/runner -e 
    production 'CGI::Session::ActiveRecordStore::Session.destroy_all
    ( ["updated_at < ?",20.minutes.ago ] )' 2>&1

</pre></code>

Both will clear out sessions that are 20 minutes old every 10 minutes.  Both will  work, but they have to load up Rails every time it runs.  I came up with the following solution to avoid loading up Rails thus alleviating some server load:
<pre><code>
  require 'rubygems'
  require 'mysql'
  
  db = Mysql.new("localhost", "db_user", "db_user_pw", "db")
  query = db.prepare("DELETE FROM `sessions` WHERE 
    updated_at < NOW() - INTERVAL 20 MINUTE")
  query.execute
  puts "Removed #{query.affected_rows} Sessions\n"
  db.close
  
</code></pre>

<p>Please note that I assume that you have a MySQL database ,have the mysql gem installed and that you are storing your sessions in a table named 'sessions'.</p>
<br />
<p>Enjoy!</p>
<br />
<p>
Stay tuned for a more flexible version that will read in your config/database.yml for your db settings so you don't have to put them in the script itself.</p>
