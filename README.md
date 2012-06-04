Twitter-SNA
===========

README

2. Create Graphs, v 2.0
filename: creatgraph_v2.py

This script creates a dynamic 1-mode digraph from Twitter.com messages.

HOW TO USE:
This program accepts three arguments: the input filename, the output filename,
and a time argument (integer representing the number of hours)

Example: python readtweetsml_v2.py inputfilenamehere.csv outputfilenamehere.txt 3

INPUT:
a csv file with three columns Date, Tweet content, username
Example: 
"Fri, 08 Jan 2012, 13:22:45 +0000","RT@cnn @johndoe Protest in Egypt #jan25","username@twitter.com (Authorname)"

The "date" field is formatted as: DoW, dd MMM YYYY HH:MM:SS +0000
+0000 refers to the timezone
The message field can contain any characters allowed by Twitter, as well as Retweets and
Tweet-ats and Hash-tags. RT@ (or "RT @") represents a Retweet; @ a tweet-at; and # a hashtag.

The R script CollectTweets.r (see, also: http://www.russellshepherd.com/d/?q=blog/replacing-twapperkeeper-r)
will collect Twitter data in this format automatically, for any given hashtag.


OUTPUT:
The script creates a 1-mode digraph of Twitter users where an edge exists if:
  1. The author includes tweet-at to another user. A directed tie is create from the
     author to the mentioned user.
  
  OR,

  2. The author includes a retweet from the original author of a message. In this case, a
     directed tie is create from user mentioned in the re-tweet to the author.

For example, the tweet "RT@cnn @johndoe Protest in Egypt #jan25" by user1 would create
two ties:
1. From user1 to johndoe
2. From cnn to user1

The graph is output in two files:
1. A static (no time data) edgelist ending in .txt
2. A dynamic (nodes and edges have lifespans, see "Time" below) gexf format file. See http://gexf.net for more info.

TIME:
Call the script with the third argument (an integer) to use time values:
Any integer greater than "0" (zero) X, defines the edge to exist from the start time
provide by Twitter (t1) to t1 + X.
For example, consider a tweet from user A to user B at 01:33:33 +0000:
If you call the script with "3" as the value for the optional third argument,
that tie will exist from A to B from 01:33:33 +0000 to 03:33:33 +0000.

CHANGE LOG:

Version 1.2 to 2.0:
1. Dynamic graph output in gexf format.
2. Automatically duplicate tweets (by indentifying identical entries, and only using one).


Verion 1.0 to 1.2: 
1. Update to work with tweets which spanned multiple lines (e.g., contained newline characters).
2. Accepts timestamps as generated by the Twitter Search API


Released under Creative Commons (BY, NC, SA) by Russell Shepherd -
russell.l.shepherd@gmail.com