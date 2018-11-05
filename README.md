# some twitter blocks

Here are 12191 accounts that I block on Twitter.  Mostly promoted, meme-posting, or "parody" accounts.

To block these accounts:

1. right click and "Save As..." [this csv](https://raw.githubusercontent.com/elliottbinder/some_twitter_blocks/master/blocklist.csv) file to download.
2. go to your settings on Twitter
2. click **Blocked accounts** on the left-hand sidebar
3. from the **Advanced options** drop down, select "Import a list" and select the csv that you downloaded.

If you think it's a mistake you made it onto this list, make an issue and I'll see if I can remove you.

If you wanna contribute, make a pull request, append your blocks, and push!


### To automate blocks for promoted accounts

Throw this script in Greasemonkey.  Open up a few twitter windows and watch your blocklist grow!  If you have any suggestions for how to block the accounts on loading of more tweets instead of using the scroll action, I'm all ears!

```
// ==UserScript==
// @name     Block promoted tweets
// @version  1
// @include  https://TWITTER.COM/*
// @require http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js
// ==/UserScript==

// select and block accounts that have promoted tweets.
$(document).on("scroll", function() {
	$(".Icon--promoted").parent().parent().parent().children("div.stream-item-header").children("div.ProfileTweet-action").children("div.dropdown").children("div.dropdown-menu").children("ul").children("li.block-link").each(
    	function (e) {
        this.click();
        $("button.block-button")[0].click();
      })
});

// scroll to bottom of page to load in some more tweets (some promoted maybe)
window.setInterval(function() {window.scrollByPages(100)}, 2000);

// refresh the page every 20 seconds so 
window.setInterval(function() {location.reload();}, 20000);
```
