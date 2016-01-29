# RIVR
RIVR is the world's first open source torrents search engine. It scrapes torrent websites (Kickass, ThePirateBay, isoHunt, Limetorrents, 1337x), and give fast results with a ranking based on torrent hash, seeds and peers. For each torrent it provides a magnet link and when available a torrent file displaying its contents. RIVR is a personal project I decided to make open source with the hope of finding people to build a distributed torrents search engine with high quality results.

# Installation
* Create a MySQL database and import schema.sql, sources.sql and trackers.sql from install folder.
* Import any torrent data you want to rtindex table (I will upload a dump with 13M torrents soon).
* Edit includes/config.php with your MySQL host, username, password and database name.
* Edit install/sphinx.conf.in (mysql_all source) with your MySQL host, username, password and database name.
* Use install/sphinx.conf.in to create the Sphinx indexes:

  > sudo -u sphinx indexer --config sphinx.conf.in --all
  
* Access Sphinx indexes with MySQL client:

  > mysql -h 0 -P 9306
 
* Execute the following commands to attach regular indexes to real-time indexes:

  > ATTACH INDEX orig TO RTINDEX rtindex;
 
  > ATTACH INDEX mysql0 TO RTINDEX rtindex0;
 
  > ATTACH INDEX mysql1 TO RTINDEX rtindex1;
 
  > ATTACH INDEX mysql2 TO RTINDEX rtindex2;
 
  > ATTACH INDEX mysql3 TO RTINDEX rtindex3;
 
* Start the Sphinx search daemon.
 
* Create a cron job to call admin/indexer.php for example every 12 or 24 hours.

* admin/tupdater.php updates the seeds/leech of all torrents in groups of 73. The final numbers are the maximum among those found in all the trackers. If we have 10M torrents this makes ~960,000 requests in total to the 7 torrent trackers, so it is not recommended to run it at the moment until we define some criteria to limit the number of torrents we need to get stats every time (for example we don't want recently (re)indexed links).

# To Do
* Limit the torrents we need to update the seeds and peers in admin/tupdater.php
* Improve the ranking formula
* Make speed optimizations
* Add user features (sign up, sign in, comments, votes)
* Make the interface responsive


# Donate
The search engine is at an early stage and many optimizations and expensive hardware are needed to put it live. The main problem is the refreshing of the torrents seeders and leechers that needs to be done for millions of torrents every 12 or 24 hours. That's why we need a few donations.

bitcoin:3EtjNVUcEc3fSab2U9JH9uHmr7aCoKcP5K