=============================
LogDog, the Timelog Guardian
=============================


Disclaimer
===========

This software is provided "as is", without any guarantee.
If you loose your entire paycheck, please do not blame me.


Purpose
========

This piece of software tries to serve as a portable, plug'n play 
Drucker Analysis Tool. For more information about the Drucker Analysis
and it uses in the everday life of the modern knowledge worker, please
refer to [1].

Installation
=============

Copy the files in the "bin" folder to a location in your disk, then
add a line in your crontab to call the `crondog` script.

Optionally, you can add this (or equivalent) lines to your .vimrc to 
access the two most common operations

map <F2> <Esc>:wq<cr>
map! <F2> <Esc>:wq<cr>
map <F4> <Esc>:r! date +\%Y\%m\%d\%H\%M\%S<cr>
map! <F4> <Esc>:r! date +\%Y\%m\%d\%H\%M\%S<cr>

How it works
=============

This software is composed of a set of scripts, each one with a defined
function:

- crondog: Call this script from your crontab to provide the reminder
  function and automate the log entering

- editdog: Call this script manually in order to enter a new log for
  the current date/time. If there is an open editor for a given day,
  this script will not open another instance. 

- transformdog (pending): Convert the LogDog log files to several formats

- POSTdog (pending): Post the logs to some time-logging services

Log files
==========

The logdog files are simple plain-text files.
The files are partitioned by timestamps, with the format:


<weekday> <mon> <day> <hh>:<mm>:<ss> <TZ> <year>

Between a timestamp and the next (or EOF) there is the description
of the work done between the first timestamp and the previous one.

Given a file with:

mar ene  1 00:02:17 ART 2013 [a]
I do bla

mar ene  1 10:02:17 ART 2013 [b]
I also do blabla

mar ene  1 13:02:17 ART 2013 [c]
Last thing I did this day
EOF


The text between [a] and [b] tells the story of the work done
between the start of the day and the moment [a]

The text between [b] and [c] tells the story of the work done
between the time [a] and the time [b]

The text between [c] and EOF tells the story of the work done
between the time [c] and the end of the day. 

Script guide
=============

Description of each script 

crondog
--------

This script is called from the user's crontab every a user-defined
number of minutes. By default calls `editdog` with default params.

Call `crondog` with the DISPLAY variable setted to something like :0
or you will not be able to view the editor screen.

Example:
\*/15 * * * * DISPLAY=:0 ~/proyectos/logdog/bin/crondog 2>~/logdog.log


editdog
--------
It will open the log file for today in your favourite
text editor, after appending it with the current timestamp.

