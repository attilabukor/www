---
layout: post
title: Performing backups the right way
date:   2014-08-06 20:33:45
categories: journal
tags: [backups, unix]
---

For years I've had a single task on my TO-DO list: backup photos. I had an awful solution years ago, and only recently did a permanent, proper solution.

Doing backups the right way means taking several items into consideration, and should not be done lightly. Trusting poor backup solutions will result in a false sense of security where you might loose everything suddenly, and not even realize it until it's too late!

These are items you should keep in mind when designing your backup solution:

 * **Automation**  
 Backups that require manual internention are backups that you'll forget to perform. Period. Backups need to be automated as much as possible so as to be sure to always have a very recent one.  

 * **Transparent**  
 Backups shouldn't be a hastle to my everyday life. A popup every day at any time is a PITA, and needless. and will most likely end up in me disabling the process permanently. I don't really need a "everything is working fine" popup anyway, which leads me to:

 * **Fail-safe**  
 If anything goes wrong, I need to be aware of it ASAP. Ideally, I need an email notification of what went wrong and as much information as possible. 

 * **Efficient**  
 Particularly, in space. I've 17GiB worth of photos (including family photos, etc). I want a snapshot of each day's files easily accesible, but don't want to use up 170GiB in just 10 days by brute-copying everything.  
 I also want the bandwidth usage to be efficient, since I usually pay for it and/or it interferes with my actual bandwidth availability.
 
 * **Maintainable**  
 Or, to put it another way: *simplicity*.  Huge scripts mixing dozen of applications may work, but in a weeks time, I'll forget how it works, and will be unable maintain it, reuse it, and, worst of all, fix it if it breaks.

 * **Secure**  
 Everything needs to be transfered securely. Dead simple.

What I did
----------

**Automation**, **transparency** and **fail-safe** are all covered by using ```cron```. My backups run on a daily basis, in case of error cron emails the output, and it does not in any way interfere with my work at all.  
```cron``` sends an email to the current user with the output of what it runs. My backup script is silent in case of success, but will leak all errors to ```stdout```, which ```cron``` will then email to me. By simple creating an MX record for my machine's hostname, and an alias on my mail server, I get an email in my inbox if anything goes wrong.  
If you don't have your own domain (or don't control the host's domain), you can set up a local [smtpd server](https://opensmtpd.org/), and forward the emails to yourself.

**Efficiency** is covered by ```rsync```. ```rsync``` is really efficient when it comes to bandwidth usage by only transfering chages over the network and not the entire 17GiB.  
As for disk-usage, by using the the ```--link-dest``` flag, ```rsync``` creates the directory tree for each day, but hardlinks files which have not been altered since the previous day. The result is a 3.4MiB usage increase per day, but the entire file tree for each day available. I can also randomly delete any day, and all other backups are unaffected.

**Security** is also covered by ```rsync```, by simply making it use ```ssh``` for transfers (which is actually the default). If you use ssh of course, you'll have to create a special ssh key pair, and make the private key available to cron, unencrypted. You'll probably want full-disk encryption to protect it.

As for **Maintainability**, I had to deal with that myself. Instead of over-complicated solutions, I wrote a 26-line shell script, of which 6 lines are actually whitespace, and 13 are comments. Pretty easy to maintain.

How I did it
------------

First of all, here's the above mentioned script:

{% highlight bash linenos %}
#!/bin/sh
#
# Backs up photos into the fileserver.
#
# Pre-existing files are hardlinked to yesterday's copy, so the size
# increase equals the size of new files, while keeping daily snapshots.
 
set -e

# Since other scripts sync cron tasks across machines, I want to make sure
# this one only runs on hyperion
if [ $(hostname -s) != hyperion ]; then exit 1; fi;

SSH="ssh -i $HOME/.ssh/backup@hades"
REMOTE=backup@hades.barrera.io
TODAY=$(date -I)

# Using -H is too expensive, and I don't use hardlinks in this directory.
# Use -x to avoid copying .enc.mount directories (fuse-mounted encrypted
# data).

# Sync the files:
rsync -aqx -e "$SSH" /home/hugo/photos/ $REMOTE:data/photos/$TODAY/ \
  --link-dest=../latest/

# Link today's as latest:
$SSH $REMOTE "rm data/photos/latest && ln -sf $TODAY data/photos/latest"
{% endhighlight %}

Stupidly simple, right?

 * Lines 8 make sure the script bails upon error instead of continuing (ie: whenever something exists non-zero).
 * Line 14 forces ssh to use a specific ssh key which has been added on the host with very limited permissions, and only for the user "backup", who owns backups and nothing else. Nobody else has access to ```backup```'s files either.
 * Line 23 does the actual copying. The files are copied to data/photos/2014-08-06, with hardlinks to ../latest (on the server side). As you'll see in a moment, latest is a symlink to the latest *successfull* backup (the very first day, it was an empty directory, of course).
 * Line 27 updated the symlink latest to point to today's backup (the script would have bailed if there had been an error). Tomorrow, the files will be compared to today's files to determine what's changed.

And, of course, the single line in ```crontab```:
{% highlight bash %}
35   5    *    *    *    /bin/sh /home/hugo/.config/cron/scripts/backup-photos.sh
{% endhighlight %}


A final item was securing the backup. I own the destination server, and the ```$HOME``` for user ```backup``` is mounted onto an encrypted drive. Should that server reboot, I'd get an email, and would need to log in and re-mount that drive manually. This may result in a single backup failing, but I would get **2** emails if it came to that. And a server having been offline is an indicator of a more serious problem.