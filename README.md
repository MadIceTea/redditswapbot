# TPFS (Thinkpads For Sale) Bot

## Description

These PRAW 5 scripts will be used on /r/thinkpadsforsale by (/u/tpfsbot). They are modified from scripts created by the mods of /r/hardwareswap and modified for use by /u/chankster, /u/NotMelNoGuitars, and /u/thelectronicnub. There are three other known running instances of the bot, /u/hwsbot, /u/mechkbot, /u/funkoswapbot.

## Files

* **flair.py**
  * Watches the current confirmed trade post (specified in config.cfg) and updates user flair.
  * Normally fired via cronjob.
  * Accepts -m (curr,prev) to allow for processing of the previous month.
  * Checks flairs against a database and will warn if the flair deviates more than the value in the config.  Helps to catch users that accidently hide flair and end up getting reset
  * Easier manual flair processing.  Simply send the bot a message with the URL of the root comment in the body (click permalink first).  The bot will flair the users, delete the warning message, approve the reported comment, reply with 'added', and send a confirming PM to the mod.

Flair is important to our moderators. It is probably the 2nd most time consuming activity we undertake. We may need to give some thought, however, to how we can preserve custom flairs set on a few of our users.

* **heatware.py**
  * Watches the current heatware thread (specified in config.cfg) and updates user flair.
  * Normally fired via cronjob.

Heatware may or may not be deployed in our subreddit, this will probably be left up to a vote of moderators with input requested from our most active users.

* **post_check.py**
  * Monitors all new posts to ensure it matches specified regexs.
  * Attempts to set post flair based on title.
  * Adds comment to each post with specific details for the OP.
  * Removes posts created < 24 hours after the previous post.
  * Checks all selling and trading posts for a timestamp.
  
  This feature will be super handy, but we'll be trying to keep the auto-messages short, to prevent user-fatigue.
  
* **monthly_trade_post.py**
  * Creates a new trade post, stickies it in the top position, updates the sidebar based on regex, and updates config file.
  * Normally fired via cronjob.
  
  Should prevent /u/madicetea from forgetting to make a new trade post for an entire six months. Hopefully.
  We have previously received modmail indicating that this may be the most looked-forward to application of a future bot.
  
* **monthly_price_post.py**
  * Creates a new price post, stickies it in the bottom position, updates the sidebar based on regex, updates config file.
  * Normally fired via cronjob.
  
  Likely will not be used in our subreddit. It will be put to a quick vote by any active moderator, but I wouldn't be holding my breath. If deleted, this part of the README will also be deleted to reduce confusion.
  
  The following scripts are utilities for the backend so PRAW will work properly with our subreddit:
  
* **util/flair_sql_import.py** 
  * Used to seed the sqlite database with initial flair values.
  * Extract the current subreddit flair values to json using [modutils](https://github.com/praw-dev/prawtools).
  * **Must be done before running heatware.py and flair.py. Failure to do this causes all flair > flairdev in config to be reported as a deviation.**

* **util/flair_sub_import.py**
  * Set subreddit flair via csv or json files

## TODO

(a) Just about everything, including making an actual TODO list of programming issues involved.
(b) Collaborate with anyone still interested in helping. There's a week left before Hacktobefrest is over and I think people will want their T-shirts. List them all in a CONTRIBUTORS.md file.
(c) Find hosting for the bot. Thinking Heroku, but also hearing options such as micro instances on Google Cloud, small box on Vultr, or Glitch.
(d) If we use a more expensive hosting option, we may need to fundraise. Might make a donations entry on the README, github wiki, or subreddit -- probably using Stripe as the funds disbursement provider.
(e) Register the bot and get API key for our PRAW initialisation file.
(f) Once the code is looking alright here, running the internal GitHub Security Scanner tool to check for tokens, necessary updates to dependencies, or other CVE problems. On that note, writing up a quick security and responsible reporting policy -- probably by writing SECPOL.md in this repository.
(g) Holding an announcemnet for a testing period and making a subreddit post to inform of these changes. If all goes well, this will smoothly become the beginning of operations date for the bot.
