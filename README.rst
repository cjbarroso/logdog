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

How it works
=============

This software is composed of a set of scripts, each one with a defined
function:

- crondog: Call this script from your crontab to provide the reminder
  function and automate the log entering

- editdog: Call this script manually in order to enter a new log for
  the current date/time 

- transformdog: Convert the LogDog log files to several formats

- POSTdog: Post the logs to some time-logging services

- correctdog: Check the structure of a log file, report inconsistencies


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

editdog
--------
It will open the log file for today in your favourite
text editor, after appending it with the current timestamp.


POSTdog
--------
