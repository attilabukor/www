---
layout: default
permalink: /portfolio/
---

Portfolio
=========

You can check my <a href="https://github.com/hobarrera"><i class="icon-github"></i>github page</a> for publicly available source code.

Websites & Webapps
------------------

I'd a good eye for details, and ample experience working side-by-side with designers to achieve highly polished websites for various clients.

The following is a brief list of those which have granted permission to be added to a portfolio.

<div class="section group portfolio">
  <div class="col span_1_of_2">
    <a href="https://virtstart.com" class="img" title="virtstart.com">
      <img src="/images/portfolio/virtstart.png" alt="virtstart.com">
    </a>
    Implemented virtstart's website, along with virtstart's webapp (both backend and frontend), which is currently in open beta.
  </div>
  <div class="col span_1_of_2">
    <a href="http://moodsy.me" class="img" title="moodsy.me">
      <img src="/images/portfolio/moodsy.png" alt="moodsy.me">
    </a>
    Implemented moodsy.me.
  </div>
</div>

<div class="section group portfolio">
  <div class="col span_1_of_2">
    <a href="http://minimalistech.com" class="img" title="minimalistech.com">
      <img src="/images/portfolio/minimalistech.png" alt="minimalistech.com">
    </a>
    Initial implementation of minimalistech.com, which has since received some minor tweaks.
  </div>
  <div class="col span_1_of_2">
    <a href="https://hugo.barrera.io" class="img" title="hugo.barrera.io">
      <img src="/images/portfolio/hugobarrera.png" alt="hugo.barrera.io">
    </a>
    Implemented this website. It's source is available over at <a href="https://github.com/hobarrera/www"><i class="icon-github"></i>github</a>.
  </div>
</div>

Native Applications & Scripts
-----------------------------

### ubersquare
<a href="https://github.com/hobarrera/ubersquare">ubersquare</a> was a foursquare client for the N900/Maemo. It was my first proper desktop (well, mobile) application, as well as my first Qt application and on of my first large python projects. As such, the code was pretty awful (though it did get the job done). Regrettably, my N900 broke before I finished the complete rewrite, and poorly designed code is the latest that's available of this now defunct proyect.

### usrc.d
<a href="https://github.com/hobarrera/usrc.d">usrc.d</a> is a set of scripts to manage user sessions' services, WMs, etc similar how to rc.d manages system daemons. Based on OpenBSD's rc.d, it's use to control background services like window managers, offlineimap, sxhkd (or xbindkeys), etc.

### screenswitch
<a href="https://github.com/hobarrera/screenswitch">screenswitch</a> is a very simple python script to switch between connected displays. Bind to one of those useless media keys modern keyboards have, it's saved me countless times when I disconnect a display without enabling another one.

### volctl2
There were good intentions when implementing <a href="https://github.com/hobarrera/volctl2">volctl2</a>, the design was pretty poor, and so was it's implementation. volctl2 binds to extra keys on my mouse and volume keys on my keyboard and adjusts the volume onpress. Unlink a oneline script, holding down the button will make the volume increase/decrease exponentially, allowing fine-grained volume changes, but allowing one to large changes fast.

### scrotpush
<a href="https://github.com/hobarrera/scrotpush">scrotpush</a> is a very simple python script that takes a screenshot, uploads it to imgur, and copies the URL into the X clipboard. Simple, yet useful.

### kbdlight
Although an extremely simple program, <a href="https://github.com/hobarrera/kbdlight">kbdlight</a> has become irreplaceble for me over time. It's a very simple C program that allows 

Libraries
---------

### tornado_rest
<a href="https://github.com/hobarrera/tornado_rest">tornado_rest</a> is a python module which includes a set of utilitary classes I commonly use for tornado-based proyects which expose REST APIs.

### pyenvsettings
<a href="https://github.com/hobarrera/pyenvsettings">pyenvsettings</a> is a python module to easily read settings from environment variables, used to follow the advice given by the [twelve-factor methodology](http://12factor.net/config).


### PyAFIP
<a href="https://github.com/hobarrera/PyAFIP">PyAFIP</a> is a python library for authorizing and validating invoices with <a href="http://www.afip.gob.ar/">AFIP</a>'s web services.

### rprint
<a href="https://github.com/hobarrera/rprint">rprint</a> is a rather simple python module pretty-prints objects or lists recursively. Useful in development/debug when you can't be bothered to write ```__str__``` for each of your classes (or simple, can't).

Experiments
-----------

### Greydown
<a href="https://github.com/hobarrera/greydown">greydown</a> was a proof-of-concept implementation for new ways to notify users of low battery: gradually turning the screen to greyscale as battery was under 10%: notifying the user non-intrusively, but in a way that cannot go unnoticed. A <a href="/journal">journal</a> article related to this experiment is still pending.

Misc
----

### AUR Packages
I maintain <a href="https://aur.archlinux.org/packages/?SeB=m&K=hobarrera">several packages</a> on the <a href="https://aur.archlinux.org/">Archlinux User Repositories</a>. Their source is all kept in a single <a href="https://github.com/hobarrera/aur-packages"><i class="icon-github"></i>git repo</a>.
