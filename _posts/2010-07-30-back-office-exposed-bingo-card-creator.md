---
title: 'Back Office Exposed: Bingo Card Creator'
author: Paul Singh
layout: post
permalink: /blog/back-office-exposed-bingo-card-creator/
categories:
  - Back Office Exposed
  - Metrics
  - Operations
---
If you spend just a few minutes on Hacker News, you&#8217;ll come across Patrick McKenzie in one way or another (I&#8217;m convinced that he must comment on every single HN post). He lives in Japan and recently left his cushy full-time job to focus on Bingo Card Creator &#8212; something he created as a side gig four years ago. Patrick&#8217;s always sharing tactical tips on HN but I wanted to know more about *how* BCC actually worked. If you&#8217;ve built something on the side and you&#8217;re trying to extract more money out of it, keep reading &#8212; this one&#8217;s for you.<!--more-->

### What is BCC?

Elementary schoolteachers like playing bingo as a review activity, because it scales to any number of students, is fun while remaining educational, and proceeds at a predictable pace.  However, every student needs a unique bingo card to play.  Making cards by hand takes a while, buying them costs a lot of money.  Bingo Card Creator makes bingo cards quickly and cheaply for schoolteachers, and other folks who are interested in playing custom bingo games.

There are two versions of the software.  One is the original downloadable Java application.  The other version is a web application, written in Rails.  They&#8217;re sold as a set, for $30 (plus $5 if you want a CD).  This is a one-off purchase.

### How did you get started?

While working at my ex-ex-day job, at a prefectural technology incubator, an English teacher connected to us asked whether I knew of a good way to make bingo cards.  I told her to Google it.  She said that she did and couldn&#8217;t find anything useful.  One thing lead to another and, well, here we are.  (Here&#8217;s the <a href="http://www.kalzumeus.com/start-here-if-youre-new/" target="_blank">full story</a>.)

### Why did you design BCC as a downloadable app instead of using a SaaS model?

When I created BCC, I was 24 years old and had graduated from a &#8220;Java school&#8221; and then spent a few years with 90%+ of my development experience being fat client Java applications.  You know the line about how if all you have is a hammer, everything looks like a nail?  Bingo cards, yep, totally a nail.  In retrospect, web applications are much, much, much, much better from the developer&#8217;s perspective (if you&#8217;re interested, [my thoughts on desktop vs web apps][1]).  However, at the time I could not make web applications.

Some time after releasing BCC, I switched jobs to a company which make Big Enterprise Java Web Applications, and concurrently taught myself how to use Rails.  (Incidentally, teach yourself to use Rails if you work on \*any\* MVC architecture: it will greatly clarify your thinking about MVC in general.  I became a much better Java programmer through my exposure to Rails.)  I started expanding the website for my product, first creating content at scale highlighting the usage of the product, then creating a custom CMS to make it easier for freelancers to create content, and eventually integrated web-enabled features on the downloadable application and launched a web application.

As for why BCC is a one-time purchase: back in 2006 I had the traditional developer&#8217;s skepticism of many effective ways to make money.  One of these is recurring charges.  I also thought my customers were used to recurring charges in their industry and hated them, so a one-off purchase would be a point of differentiation.  Certainly, some customers do genuinely hate recurring charges, but I will certainly have them as a core feature of any software I produce in the future.  The business benefits are just incredible.

I have approximately 3,000 paying customers for my software.  You know what my revenue was for today?  \*Nothing\*, because we&#8217;re in the dog days of summer, and sales slow to a crawl until school gets back in session.  If there were any recurring component to the revenue from BCC, that would essentially smooth out performance over the very seasonal calendar, and also continue to reward me for previous hard work.

### What tools do you use on a daily basis?

[<img class="alignright size-medium wp-image-934" title="business-in-a-box" src="http://www.resultsjunkies.com/wp-content/uploads/2010/07/business-in-a-box-300x225.jpg" alt="Business in a Box" width="300" height="225" />][2]I&#8217;m currently using a Dell Studio notebook, which I bought two months ago to celebrate going full-time.  Most importantly for my business, it has a SSD drive (128 GB of lifechanging speed &#8212; buy one today if you don&#8217;t have one) and a copy of VMWare Workstation, which lets me switch seemlessly between Windows and Ubuntu running in a VM.  I prefer Windows as a client OS, and love Windows Seven.  (And I just lost any chance of speaking at a Rails conference in the forseeable future.)  These days, most of my development is done in Ubuntu, because I use too many server-side things which are hard to fake on Windows.

I use NetBeans for Rails development and Eclipse for Java development.  My preferred browser is Chrome, and I keep Firefox around for superior add-on (Firebug, YSlow, ShowHTTPHeaders, etc) support and IE around for testing, though I prefer IE to Firefox.  (Darn, I am burning the bridges today.)

I use an 812SH Sharp phone, which is a Japanese featurephone.  My main use of my phone is to send text messages to friends and receive phone calls, although it also has a (crippled) browser which is sufficient to operate my site&#8217;s admin interface.  I take my Kindle everywhere I go, and use its built-in browser for light browsing, such as checking email or reading Hacker News.

You can see my whole workspace in the attached photo.  The $1 notebook is from Muji, probably the best designed of a series of $1 notebooks I have owned.  I use it for project management, technical documentation, and todo lists.  I also use <a href="http://www.kalzumeus.com" target="_blank">my blog</a> as a public repository of &#8220;What was I thinking when I did that?!&#8221;, and it has saved my bacon more than once.

I use Gmail personally and Google Apps for my business-related email.  My email workflow is very simple, owing to many years of running this business on a part-time basis: I check it when I wake up and bfeore I go to sleep, and immediately answer any emails from customers, and address emails from non-customers (for example, startups asking for advice) as time allows.  The time difference between Japan and the US means that most customers get emails within 5 ~ 9 hours of their email.  I tell my customers that I generally aim at answering all questions within one business day, and I meet that goal in excess of 99% of the time.

I use a variety of web services to handle various aspects of my business.  Many of them will be discussed below.

### Can you tell us a little about your backoffice infrastructure?

At any given time I have approximately three or four VPSes at Slicehost.  All use Ubuntu.  The largest one, currently 1.5 GB, is for Bingo Card Creator.  I run all of my PHP-using sites, such as my blog and mini-sites, on a separate 512 MB VPS.  These are physically separate because I trust WordPress about as far as I can throw it, and also because Apache has a habit of taking down memory-constrained VPSes when hit by large amounts of traffic, and if that took down my site as collateral damage many people would be annoyed with me.  I also have another VPS for <a href="http://www.appointmentreminder.org" target="_blank">Appointment Reminder</a>, currently at 512 MB while in development.

Bingo Card Creator is a Rails application, running behind Nginx (the best webserver ever) proxying to four Mongrels.  This is largely because that was the best practice back in 2007 when I created it, and I&#8217;ve had no impetus to change.  In addition, there are two DelayedJob workers running constantly &#8212; these primarily do PDF (bingo cards) and image creation (live previews of bingo cards for display via AJAX), and secondarily handle talking to external APIs such as Mixpanel.

Most of my customer data is in MySQL.  I also use Redis, primarily for non-permanent persistent data such as A/B test participation, and Memcached as a generic scratchpad and cache.

BCC has a fairly sophisticated monitoring setup, because <a href="http://www.kalzumeus.com/2010/02/21/i-had-downtime-today-heres-what-im-doing-about-it/" target="_blank">I hate downtime with a burning passion</a>.  The processes are monitored by god and Scout.  Should anything untoward happen, Scout sends me an email, and Google sends emails matching certain subjects (implying critical issues, such as the site being totally unavailable or the DelayedJob queue going out of control) directly to my cell phone.  My cell phone has a custom ringtone for receipt of those emails: <a href="http://www.youtube.com/watch?v=Gz3Cc7wlfkI" target="_blank">Ride of the Valkyries</a>.  I chose it because it is intensely disturbing to me, would certainly wake me up, and yet would not unduly embarass me if it were to ring in public.

I take payments via Paypal and Google Checkout.  Both are wrapped for me by e-junkie, a payment processor who offers a custom cart (which I no longer use, but which is a great first option for folks who can&#8217;t program their own) and which handles Registration Key delivery, accounting, and wraps callbacks in a consistent API.  I originally used them when this was all beyond my capabilities, since I couldn&#8217;t do web programming.  As time has progressed, I&#8217;ve gradually brought many of their functions (such as accounting / customer records / search) in-house.

One other thing e-junkie handles is API calls to SwiftCD for customers who order CDs.  It happens totally transparently for me: if the customer requests a CD, I don&#8217;t have to do anything.  SwiftCD burns an image I&#8217;ve uploaded, mails it directly to the customer, and invoices me at the end of the month.

I handle all customer support by myself, using email.  (I have made two phone calls related to Bingo Card Creator in four years.  Customers frequently request that I call them.  I have no desire to do so, because $30 a sale is not enough for me to walk technically disinclined customers through a Java installation at 4:30 AM in the morning.  Most are quite happy when I resolve their issue over email and tell them that, as I&#8217;m in Japan, it would be inconvenient for them to have to call me.  Since the vast majority of my customers have never made an international phone call, that explanation works for them much better than &#8220;Basically, it makes little economic sense for me to speak to you about this.&#8221;)

I am a metrics junkie.  At present, I use <a href="http://mixpanel.com/" target="_blank">Mixpanel</a> for funnel tracking, Google Analytics for basic web statistics, <a href="http://getclicky.com/" target="_blank">Clicky</a> as a backup to Google Analytics, and <a href="http://www.crazyegg.com/" target="_blank">CrazyEgg</a>.  CrazyEgg lets you know where people are clicking on your website.  It has repeatedly made me thousands of dollars by showing obvious visible evidence of suboptimal page design.  I highly recommend everyone use it.

I use <a href="http://www.bingocardcreator.com/abingo" target="_blank">A/Bingo</a>, OSS Rails software which I wrote, to do A/B testing.

I am a heavy user of Google AdWords, mostly on the content network.  You know all those pages Mahalo / About.com / Demand Media / etc have which satisfy every query a Kansas schoolmarm could possibly ask?  If one is about bingo, you&#8217;ll probably find my ads on it.    AdWords is my #2 source of customers after organic search.  It is responsible for approximately half of my sales and 1/5 of my profits.  (I do a bit of work these days to measure this in a more systemic manner than AdWords will by default.  For example, if you Google [math bingo cards] and arrive at my math page via the organic listings, then sign up to my trial, and later Google [bingocardcreator.com] and click the AdWords link, Google will score that as a conversion for AdWords.  I only score conversions for AdWords if the customer found me through AdWords prior to signing up for their trial, regardless of how they use Google as navigation after that.)

### Can you share the key metrics you watch on a daily basis? Why are they important to you?

<a href="http://www.bingocardcreator.com/stats" target="_blank">I have published a variety of stats</a> but I don&#8217;t watch metrics on a daily basis because I don&#8217;t make metrics-based decisions on a daily basis, and absent making decisions watching metrics is only as productive as playing WoW.  When I have to make decisions about upcoming development priorities or marketing decisions (such as what keywords to look at), I look at my keyword data (Analytics), previous popularity for word lists on my site (homegrown), and A/B tests.  A/B tests are sort of the holy grail of metrics, because they are \*designed\* to result in data that tells you something which you can use as the basis for a decision.

Pop quiz: Analytics said your conversion rate went down.  What do you do?  Answer: nothing, because you have no clue why.  Maybe you spend a few hours digging into stats and trying to retrofit an explanation onto the data, which is probably just deceiving yourself.  Pretend that instead you A/B tested blue buttons versus green buttons.  Blue buttons won.  What do you do?  Exactly, you use the blue buttons.  A/B tests are actionable by design.  That is why I&#8217;m so enamored with them, and why I \*had\* to create a better way for Rails developers to use them.

A/B tests also have a very nice property for time-constrained businessmen: you code them and then let them run while you do other things, then check them.  Coding and checking is fast, and letting them run doesn&#8217;t block progress (or participation with your family, the day job, or what have you).

One metric I do watch is sales, particularly YOY change in sales (this tells me whether the business is growing when adjusted for seasonal distortions) and &#8220;predicted sales this year&#8221;, which is partially a vanity metric (that is my score at the game of business, and I love playing games) and partially lets me make consequential decisions such as &#8220;How much do I get paid?&#8221; and &#8220;Can I afford to leave my day job?&#8221;

[<img class="alignright size-medium wp-image-935" title="BCC Dashboard" src="http://www.resultsjunkies.com/wp-content/uploads/2010/07/dashboard-for-paul-291x300.png" alt="BCC Dashboard" width="291" height="300" />][3]The image on the right is what you see if you log into my website as me.  At the top left you&#8217;ll see quick links to common tasks, from using my bingo card CMS to linking to my version of various stats.  (They&#8217;re typically similar to the publicly available versions, with more detail.  For example, I can show data more granularly because I don&#8217;t have to worry about private customer data leaking.)

On the left side you&#8217;ll see a few stats I use as a quick business health check, like login counts for this week.  Invitation Stats shows the status of a project I tried, where I created Dropbox-inspired double-sided incentives for inviting your friends to join the service.  As you can see, it has not been a resounding success.

Sources of sales shows a quick overview of who is sending me customers that convert lately.  (&#8220;nil&#8221; is #1 largely because I wasn&#8217;t tracking this until recently.)

Vanity Stats is on the dashboard purely because it brings a smile to my face.  I used to be a teacher, and even in my best year I rather doubt that I contributed to 600,000 lessons.

The main pane of the dashboard is search results, which I use for customer support.  By default it shows the last ten customers, because people are overwhelmingly likely to ask for support their first day with the product.  It is optimized to my most common problems: &#8220;What is my Registration Key?&#8221;, &#8220;What is my password?&#8221;, and &#8220;I&#8217;m seeing something funky.  What is up?&#8221;  (Clicking on &#8220;Ghost me&#8221; logs me in as them, which often lets me diagnose the issue instantly.  I love web applications.)

You&#8217;ll also note the quick&dirty sales projections.  These are intentionally not that sophisticated: if I sold $100 on the first day and there are 30 days this month, then it will project $3k in sales for the month.  Currently it is showing $4k in projections for a June, which I would be flabbergasted if that came to pass, but after a week or so it typically converges on a fairly accurate number for most months without a major holiday.

<a href="http://www.bingocardcreator.com/articles/dashboard-on-a-shoestring.htm" target="_blank">I also have a physical dashboard in my room</a> which displays some other metrics, mostly for personal motivation.

### When a new sale comes in, can you walk us through the process?

I&#8217;m going to back up a step, because the vast majority of my sales start in the free trial, either the web app or the downloadable version.

In the downloadable version, the customer probably just hit a trial limitation.  They&#8217;ll be shown a message much like this one:

[<img class="aligncenter size-medium wp-image-937" title="trial-limit-reached" src="http://www.resultsjunkies.com/wp-content/uploads/2010/07/trial-limit-reached-300x158.png" alt="" width="300" height="158" />][4]

If they click Yes, the program will generate a random ID within the Java application, and open their default browser to a particular page using that ID as a query parameter.  Rails will stuff that ID in the session, then show them the purchasing page.  The shopping cart on the purchasing page contains a link to e-junkie, including a parameter e-junkie will pass back if they receive a transaction notification from Google or Paypal corresponding to that link.

Let&#8217;s pretend that the customer clicks purchase.  They&#8217;re transparently redirected through e-junkie to the payment process they selected in my shopping cart (Paypal or Google Checkout).  They fill out their payment details, and I get money deposited in my account.

Paypal or Google Checkout then pings e-junkie with a very large, complicated API containing all the details of the transaction.  e-junkie turns around and pings my server with the details of the transaction, twice.  Once in requesting the Registration Key for the customer, and once to register the fact of the sale.

As soon as my server receives word of the sale, I look at the session ID e-junkie gave me, and determine what session it belongs to.  Then, I check to see if they had that random ID passed by the Java application.  If yes, I write a key in memcached recording the correspondence between their random ID and their Registration Key.

While this was going on, their copy of Bingo Card Creator has been relentlessly polling the server: &#8220;Has she bought it yet?  Has she bought it yet?  Has she bought it yet?&#8221;  It does this by passing the same random ID to a web service running on the server.  If the transaction has been consumated, BCC will learn the Registration Key, and then automatically upgrade itself to the registered version.  This removes a \*major\* source of customer support complaints, since Registration Key management is a hard concept for many shareware customers to grasp.  From the customer&#8217;s perspective, she just got done putting her details into Paypal, and by the time she closes the browser (after ignoring the instructions) and goes back to Bingo Card Creator, it already says &#8220;Thanks for your purchase!&#8221;  That little psychic saves me hours every month in support email.

The process is quite similar for the online application. (You&#8217;ll notice that this test account has participated in the Refer a Friend program a few times and has a quote of 20 cards, rather than the 15 cards that most folks start out with.  That referral program has not been a success.)

[<img class="aligncenter size-medium wp-image-938" title="online-trial-limitation" src="http://www.resultsjunkies.com/wp-content/uploads/2010/07/online-trial-limitation-300x129.png" alt="" width="300" height="129" />][5]

If you purchase while signed into the online application, the link to e-junkie contains an identifier for your account.  I look it up when I receive the purchase confirmation, and transparently upgrade the account to the registered version.  There is a manual way for customers to upgrade accounts, too, for those who use it at home but purchase at school from a machine I&#8217;ve never seen before, and for similar cases.  The vast majority of customers get instant, automatic gratification though.

In addition to handling the registration, my site also creates bookkeeping entries (in my home-grown bookkeeping software &#8212; there was a remarkable dearth of stuff which would produce publicly visible sales reports) and entries in my customer records so that I can conveniently look them up for support purposes.  Prior to developing these systems, I used the ones at e-junkie.  They were perfectly adequate, but that is one more login to have to do to accomplish any customer support task.

### What were some of the biggest mistakes you made in growing your business?

The time IE 6/7 users couldn&#8217;t sign up, lasting for the busiest month of the year, has got to be up there.

There are many, many things that I&#8217;ve done which were suboptimal in retrospect, but I don&#8217;t necessarily consider them mistakes.  Doing a desktop application was suboptimal, but I couldn&#8217;t have delivered a web application at the time.  I am currently on my third &#8220;second&#8221; product, having done a bit of work on numbers one and two and then discovered that they were unlikely to be successful.  I have a list of failed A/B tests too long to fit into this already overlong interview.

I have consistently underestimated how far this program would eventually go.  For example, prior to leaving my ex-ex-job (which was a cushy 40 hours per week endeavor with little professional growth) to become a salaryman (which taught me a lot of things at the expense of 2.5 years of my life), I was offered the opportunity to recontract for two years.  I declined, feeling that I was going to better things as a salaryman.  At the time, I considered it beyond fantasy to go full-time just on BCC.  Knowing what I know now, could I have used much longer nights and weekends to grow the business, develop another product, and go full time a bit earlier with less work-related stress?  Probably.  But I don&#8217;t really regret being a salaryman &#8212; it makes for a great story to complain about.

### If someone wanted to start a business similar to yours, what advice would you give to them?

DO IT.  LAUNCH IT.  GET IT OUT THE DOOR.  I don&#8217;t care if you think you can&#8217;t code.  You can learn.  I don&#8217;t care if you think you can&#8217;t market.  You can learn.  I don&#8217;t care if you think there is no market for your product.  You can grow, expand, and pivot.  (And besides, what are you working on which is more niche than bingo cards for elementary schoolteachers, anyhow?)

Running a business is the best possible training for running a business.  So stop making excuses &#8212; believe me, I was a champion at it &#8212; and start running a business.  By all means, read blogs, talk to people, scheme and dream&#8230; but then go get your hands dirty.

In the entire history of the world, there has never been a better time to start a business than right now.  You can run a multinational software business with thousands of customers.  It isn&#8217;t rocket science.  A confluence of things &#8212; OSS, scalable distribution like organic SEO, AdWords, Facebook and friends, powerful APIs like Paypal or Twilio that let you hook into massive enterprise power without leaving your kitchen &#8212; is making it even easier with each passing day.  So start learning now.  Every day you&#8217;re working, you&#8217;ll be building the knowledge, tools, connections, SEO juice, capital, and audience to make an even better go of things tomorrow.

### What else should we know about you?

Prior to running a business I ran a WoW guild.  It was rather substantially more work and more drama than running a business, for dramatically worse loot.

If you haven&#8217;t started a business yet, you&#8217;re saying that everything in your life right now is more important to you than having a business.  Ask your heart of hearts: is that really true?  If you&#8217;re booked solid with your children, then yes, absolutely put your children first.  But if you \*say\* you&#8217;re booked solid with your children and yet you still find time to watch television and play online poker, then it is time to have a frank discussion about your true priorities in life.

<p style="text-align: center;">
  ***
</p>

<p style="text-align: left;">
  <em>Jeebus</em>, is there anything else I can add to this? Patrick&#8217;s kicking some serious ass and, this is the best part, is openly sharing the details of how he does it.
</p>

  * I *love* his approach to metrics &#8212; he loves them but avoids looking at them unless they&#8217;re critical to a decision. Even then, he lets the results of A/B testing tell him what to do next.
  * If you don&#8217;t have an admin dashboard for your app, do it now. Patrick&#8217;s dashboard let&#8217;s him handle customer service and business metrics in one place, yours should do the same. (Incidentally, this interview convinced me to build &#8220;user impersonation&#8221; into my own dashboards for <a title="On Demand Direct Mail" href="http://www.mailfinch.com" target="_blank">MailFinch</a> and <a title="Notary CRM Software" href="http://notarycrm.com" target="_blank">NotaryCRM</a>. Thanks Patrick!)

*You can find Patrick on <a href="http://www.kalzumeus.com" target="_blank">his blog</a> and on <a href="http://news.ycombinator.com/user?id=patio11" target="_blank">HN</a>, check out <a href="http://www.bingocardcreator.com/" target="_blank">Bingo Card Creator</a>, read other <a href="../category/back-office-exposed/" target="_blank">Back Office Exposed</a> features and <a href="https://spreadsheets.google.com/viewform?formkey=dDJRdWdkYWlycEVDc3ZQSWUtUVlfeFE6MQ" target="_blank">submit yourself for a Back Office Exposed</a> feature.*

 [1]: http://www.kalzumeus.com/2009/09/05/desktop-aps-versus-web-apps/
 [2]: http://www.resultsjunkies.com/wp-content/uploads/2010/07/business-in-a-box.jpg
 [3]: http://www.resultsjunkies.com/wp-content/uploads/2010/07/dashboard-for-paul.png
 [4]: http://www.resultsjunkies.com/wp-content/uploads/2010/07/trial-limit-reached.png
 [5]: http://www.resultsjunkies.com/wp-content/uploads/2010/07/online-trial-limitation.png