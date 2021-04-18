---
title: "Tracking your investments in a Google sheet"
---

There are many apps that can take your investment data and give you a fancy dashboard, plus some add-on services based on analysis of your data. If you don't want all those bells and whistles, you can just track your investments in a Google sheet. You can even fetch the price of stocks/mutual fund units using the `GOOGLEFINANCE` function and add charts for a quick overview.

> I have created [an example sheet](https://docs.google.com/spreadsheets/d/1Kkr4hqphldFYqyikw2Zu0l29a0EdVYLhh17z-MgaHLE/edit?usp=sharing) you can use to get the idea (or use it as a template). You can get the ticker name for `GOOGLEFINANCE` as described in [this](https://stackoverflow.com/a/59435693) StackOverflow answer. One gotcha is, the price data returned by `GOOGLEFINANCE` can be a day old sometimes.

![Example sheet screenshot](/assets/images/posts/investments-tracking.png)

For me, there are two main reasons to get a consolidated view like this:
1. To know where my portfolio stands with respect to the goals.
2. If there is any deviation from the intended asset allocation. 

Google sheet works just fine for both of these.

I have been using this approach for a few months now, and so far it is working well. I update the sheet once a month to record the SIP/STP transactions. If I make a lumpsum investment, I add it once I get the statement in email. 

What do you think of this approach? Thoughts, suggestions - do let me know in the comments.
