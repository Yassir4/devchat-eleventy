---
layout: layouts/post.njk
title: >
  281 RR Take My Money with Noel Rappin
date: 2016-10-12 06:00:21
episode_number: 281
duration: 41:38
audio_url: https://media.devchat.tv/ruby-rogues/RR281_Take_My_Money_with_Noel_Rappin.mp3
podcast: ruby-rogues
tags:
  - ruby_rogues
  - podcast
---

00:30 - Introducing Noel Rappin

- [_Take My Money: Accepting Payments on the Web_ by Noel Rappin](https://pragprog.com/book/nrwebpay/take-my-money) (Ebook only)
- [_Take My Money: Accepting Payments on the Web_ by Noel Rappin](https://www.amazon.com/Take-My-Money-Accepting-Payments/dp/1680501992/ref=asap_bc?ie=UTF8), (physical copy pre-order link)
- [Website](http://www.noelrappin.com/)
- [Twitter](https://twitter.com/noelrap)
  1:00 - Paid gateways for apps6:05 - Why write _Take My Money_?8:45 - Getting tripped up on simple arithmetic 11:55 - Troubleshooting gateway system failures
- [Runscope](https://www.runscope.com/)
  21:45 - Managing administrative roles
- [Paper Trail](https://papertrailapp.com/)
  25:55 - Reporting29:00 - Techniques for testing your system33:25 - Overarching themes in _Take My Money_

### Picks:

[_The Fifth Season_](https://www.amazon.com/Fifth-Season-Broken-Earth/dp/0316229296) and [_The Obelisk Gate_](https://www.amazon.com/Obelisk-Gate-Broken-Earth/dp/0316229261) by N.K. Jemisin (Noel)[Flash Forward podcast](http://www.flashforwardpod.com/) by Rose Eveleth (Noel)Police officers (Charles)[Webinar Jam](https://webinarjam.com/)(Charles)

### Transcript

Charles: Hey everybody and welcome to Episode 281 of the Ruby Rogues Podcast. This week, I am the panel I guess, I'm Charles Max Wood. If you're wondering where everybody else is, stay tuned either next week or I’ll put a link in the show notes to the discussion that as we record this I’m planning to have on Thursday about that. We also have a special guest this week and that’s Noel Rappin.Noel: Hi everybody. Charles: Noel, do you want to give us a brief introduction? I know you’ve been on the show before, you’ve got some new stuff going on.Noel: My name is Noel Rappin, I am the Director of Development at Table XI which is a consulting, mostly Rails and also Javascript and a couple of other things in mobile and design. We do a lot of stuff in Chicago. I also write technical books, I have a technical book which is out currently in beta from Pragmatic Press which is called Take My Money: Accepting Payments on the Web. Charles: Awesome. That’s what we brought you on today to talk about is money. It was interesting you gave a talk at Ruby Remote Conf about this and then I read a few chapters and skimmed the rest of the book, I just didn’t have time to completely finish it. It was funny because when I first thought about money and code, it’s just like well it’s just numbers. It’s so simple, it’s just math. Clearly, it’s not just math.Noel: Yeah. It is math, it’s also math. I actually had to do this in my proposal too. When I pitched the book to Pragmatic, one of the pushback was, and they pushed back largely to see if you can explain it. One of the pushback was like well, Stripe already has great documentation, what else is there? I think that there’s a couple of things with that. Money is math but it’s also a really weird kind of math that has these real world consequences that are very, very important to people. The API calls need to be embedded in this business logic that can get very complicated. Just because you can make the API call to Stripe doesn’t mean that you are correctly storing the information that you need in order to be able to refund it or to be able to write reports or to be able to take care of legal or accounting obligations or administration. When we architect code, we sort of hand wave about business logic. This is the best way to handle business logic. But when you're talking about money, you’re literally talking about the business logic, just the logic that runs the business. It tends to be the most complicated part of the application. If somebody comes to you and says, “Oh, we just made this great sale, it’s a big customer but we had to give them a 15% discount, can we handle that?” No is not an acceptable answer.Charles: It’s interesting too because there are all these rules around how you deal with your payment gateway and there are all these rules. I’ve set up a few systems either for myself or for other people as a contractor. Yeah, it’s like we need to get a refund. It’s like oh crap.Noel: Yeah, refunds are funny because refunds in some ways are more straightforward than charges because in most gateways they don’t actually reauthenticate it. There’s a tremendous amount of administrative complexity behind that. Who can authorize it? Is it a full refund? Is it a partial refund? Can you undo a refund? How do you account for that in your daily reporting statistics or your inventory? It’s amazing. Also, unlike search algorithms or something like that, money has legal obligations that go along with it. When you're taking people’s money or when you're taking people’s information like that, you're running up against the log very fast. You need to take that into account as well.Charles: Yeah, I worked on a contract where we actually had to deal with PCI compliance. It was like holy cow.Noel: My recommendation is to avoid that if at all possible. The gateways make it easier and easier to avoid having to store that information locally because they have these mechanisms where a customer enters their credit card and the credit card is authenticated by a direct browser ajax called to Stripe server and Stripe gives you this one time token that you can use. You don’t need to even see the user’s credit card number on your server which is fantastic.Charles: Yeah, I really love that, that’s what I use as well. I’ve also gotten into Paypal and that’s a whole can of worms.Noel: It’s really interesting there because you can kind of see the evolution of how people have thought about these problems. When Paypal started, they were a solution to a specific problem, specifically people were nervous about giving their credit card numbers to every online retailer. Paypal’s original proposition, if I'm remembering it right, was you can just give your credit card to Paypal and then all the web retailers will just deal with us. That’s still true, people are still a little bit nervous about it I guess, but the ways in which people deal with it, the ways in which Stripe’s API deals with that issue with the browser checking and things like that, are so different than the way Paypal’s flow evolved that dealing with Paypal payments just becomes a completely different thing in its own right because the workflow is so different.Charles: This isn’t really a problem I hear many people talking about, people just tend to solve it either by going with Stripe or they suffer through whatever they have to suffer through to get Paypal or something else set up. I'm wondering why write a book about something that people don’t even really talk about as a problem that they have?Noel: This is a weird thing. I get really interesting responses when I talk about it in public. I think that to some extent, the book is going to need to find its audience in a particular way. When I started on, I did my first really complicated payment gateway application, not the first one I’ve ever done but the first one that was really complicated about three years ago. I was really looking for people who had written down ideas of good practice in terms of dealing with the API and things like that. I really didn’t find any. In particular, dealing with things like how do you manage the case where you need to go to the credit gateway and then you need to touch your database afterwards but you need to be really careful that nothing in that database call doesn’t fail because it’s really bad if your database transaction fails after you charge the credit card. I really couldn’t find anything about how other people had attacked this problem. I actually really started to wonder whether I was seeing a problem that nobody else saw or whether I was just missing something obvious. I eventually came to believe that people do tend to really muddle through this whether they realize the specific problems or not, people do have a strong tendency to muddle through this on their own. In the end, I wound up writing a book that I would’ve really loved to have gotten my hands on three years ago because it would’ve saved me a ton of time. What happened is I just gave the Ruby Remote Conf talk, I gave a very similar one just last week at Rails and a number of people came up to me and said various things like, “Yeah, I had to do all that, boy that was hard.” As far as I can tell, the world seems to divide into people who don’t realize they need to read this book yet and people who think they’ve already solved the problem themselves. I think both of those people are going to be helped by this, I think there’s stuff that hopefully will save you a lot of time and frustration when dealing with failures, when dealing with the needs of administration or when dealing with some of the other things that can trip you up, or even just dealing with the simple arithmetic of dealing with money which can trip you up.Charles: How do you get tripped up on simple arithmetic?Noel: If you never worked with money before, the natural tendency is to represent money as a floating point number because it’s got a decimal point and everything. Typically, at least in the US. The problem with that turns out that floating point numbers are actually approximations. You can simulate this in Ruby really easily by going into RIB and typing 3.01x5 and you will get rather than 15.05, you’ll get 15.049 repeating because floating point numbers just don’t accurately reflect most decimal numbers, even in these really simple cases. That’s for all kinds of arcane reasons of encoding and trying to match an infinite set of numbers into a finite set of digits. There’s two problems with that. One of which is that either math can be off fairly quickly even though the errors are small. If you're at a significant volume, you can easily start to lose fractions of pennies here and there and that can actually add up. Also, it makes quality testing hard. If your code is dependent on checking for quality and you're doing floating point arithmetic, there’s a good chance it won’t work.Ruby has a number of options for this. The one that I like to recommend is the money gem which uses Ruby’s bigdecimal class internally to represent money as essentially an integer number. It’s a little bit more complicated than that. It also handles rounding errors the way that financial institutions handle rounding errors or handle rounding which is potentially different than the way you learned it in elementary school. The money gem gives you an option as to how you want to round, how you want to break ties when you round numbers, and how many digits of precision and things like that. And then it gives you an exact representation of the money which saves you from floating point errors which can be hard to predict and can cause a lot of havoc.Charles: Gotcha. I think it’s interesting that even the simplest part of this that you would think okay, it’s just math, even that can get goofed up. Noel: Yeah. Table XI uses a coding problem. I think I can say this because we’re probably going to change it soon anyway but the coding problem does use a little bit of monetary arithmetic and it’s not much but it’s enough so that if people use floating points instead of integers, they actually hit the wrong answer. That’s not even doing complicated math, it’s just adding up a bunch of prices. If you use floating point, you get a rounding error at some point whereas if you use integers you don’t.Charles: I want to go into something that you mentioned a few minutes ago just because if there’s one thing that’s going to mess stuff up for me, there are two areas in this. One is basically strike call backs, I'm going to talk about them in a second. The first part is just when stuff fails, whether it’s on my system or the gateway gives me a failure error code or something like that, or things like that. What do you do or how do you handle those situations when they occur?Noel: There are a couple of things that I think help. There are a few that I’ve found, a couple that I’ve actually managed to implement in applications and a couple that I hope to the next time I do this that I’ve gotten from other people’s experiences. The problem with failure on a credit card issue is there’s sort of two problems, one of which is the credit card fails but you go on with the transaction anyway and you wind up pushing the sale through even though the credit card failed. I’ve never actually had an app that had a significant problem with that, that’s relatively easy to catch, you just need to know that it’s a possibility. It’s actually fairly easy to test for since most of the gateways give you sample credit card numbers or ways to enter sample data that will automatically trigger various fraud or credit card declined conditions so that if you're writing tests that use PCR or something, so you directly hit the gate when you test, you can relatively easily simulate a failure condition so that you can make sure that your code works correctly.The problem that struck me up more in my own work is the payment gateway transaction succeeds but then the database fails. I’ve had cases where sort of an innocuous seeming validation in one of the objects that we were saving, we thought we were validating against something that was always true of the response in the gateway and it turned out that sometimes the gateway hiccuped and sent us slightly different information. The validation would fail and the transaction wouldn’t save. That was disappointing.Charles: I’ve had that happen too. Noel: The thing I said in my talk was I went through every line of code that happened after the payment gateway with the idea that any mistake would be a customer yelling at me which was kind of motivating. One thing is you do as little as possible in that situation after the transaction and really think about whether validations and things like that are important enough to block a running transaction. Another thing that I think is helpful is to split the job up into a couple of different transactions and use them as different background jobs. For instance, the customer submits their form and instead of directly doing stuff, you trigger a background job that basically sets up the data that you need to set up to make the payment call. You have that trigger another background job that actually makes the payment gateway call and potentially that triggers another background job that does a mail un-success or something like that.There are a couple of advantages in that approach, one of which is that it sort of limits the consequences of failure. If the payment gateway fails, you still have a record of what you’ve done to date and you can potentially rerun that transaction if you make a fix. It also helps with error checking. If you know that the payment gateway background job is only going to get triggered if the setup succeeds, then there’s certain kinds of error checking that you don’t necessarily need to keep doing because you know there are errors conditions to where hopefully it’s just never gonna reach this job. That’s potentially a really valuable technique, you do it as a bunch of different, small transactions that get handled by background jobs. They can either spawn their own individual background job or they can register themselves and you have a periodic background job that picks up all the jobs and all the transactions in a particular state and tries to move them forward. That kind of incremental step through process is the way that I'm trying to push the new applications that I might write in this space.Charles: That makes sense. I like kind of the step by step flow because then you can see which step it actually failed on. Noel: Yeah.Charles: The other thing is that you have those side-long jobs and the nice thing about that is that you can also, in a lot of cases with most systems, you can actually re-run them.Noel: Right, it makes it much easier. A lot of times, the gateway fails for a transient reason, network failure or something like that. To have the ability to very easily have those jobs re-run on failure can be pretty powerful.Charles: The other thing is that it breaks up the process and makes it much more understandable.Noel: Another thing about that is to not throw out partial transactions. The natural tendency, I say this because I’ve done it and have production code that does it, is to start this whole thing in a database transaction so that the whole thing gets blown away if something goes wrong which is absolutely the right choice for many applications and even many payment applications. I would also think about doing something particular with logging or with continuing to store database transactions, coming back and storing a database transaction in a failed state or something like that so that you can go back and see what the failed transaction is. I'm currently trying to track down what seems to be a very intermittent possibly credit card failure case on a gateway that I'm using and I don’t see it often enough to know what it is. Whatever the gateway is sending back, it’s not matching our expectation of what the data is going to come back. I keep trying different things to try and get it to trigger an acceptance notification so that I can actually see a live failed response and then try and figure out what’s actually causing it. You want to make sure that you can try and see when those failure states happen so that you can mitigate them.Charles: I also found that as you said, a lot of times you get that case where you get information from the web hook that isn’t exactly what you expected. Then, it’s okay how do I figure out what’s going on here and how do I fix it? I wind up glomming on a whole bunch of if statements or special cases that may or may not actually help me out. Noel: I become a big fan of saving as much information from the payment gateway and the partial information that leads up to the price calculation and things like that. As much of that stuff as possible. It’s a little bit different. There’s kind of two contradictory save everything things which is save as little as your user’s personal information as you can and save as much information about the transaction, non-personal information, as you can. I think that also helps. You need to be in a situation where you can recreate the transaction as it was when it happened even if some of your business logic has changed.Charles: Yeah, I wound up using Runscope for a long time for that kind of thing. Effectively, what it does is you set up the place where Stripe is sending its requests for the web hooks. What it does is it records that and then passes it on to where you told it to and then you can re-run any of those end points getting triggered again.Noel: That sounds useful.Charles: It’s nice in the sense that then you can just see from that one perspective what got sent back from Stripe or whatever other gateway you're using. You can then retriever it and then set it off again and make sure that the process works as expected.Noel: That’s true. You also sometimes even have cases where you need to recalculate stuff even if you're not sending it. You might have reports or things like that where you need to recreate what the processing fee was versus the shipping fee versus the actual individual item fee for individual items if you're doing that kind of transaction. You also want to save those partial calculations so that you're not dependent on going back to the code which might’ve changed.Charles: Right. Your book goes into a mix of we talked a lot about the technical challenges here, but it also talks about some of the management and administrative stuff because that’s also part of this same system, right? Because you have the behavior, the people involved in the behavior of the data, so to speak.Noel: Yeah, you have this long term issue where you have all of this data and all this stuff and you have customers which means you probably have customer service. In the long term, how well your administrators are able to deal with customer service kinds of issues without having them cause programmer issues, that’s going to go a long way towards how your site runs. I think we all have a tendency as developers to underestimate the value of that part. We all kind of say the admins, we can just train them, they work for us, we don’t have to get them a great UI, we don’t have to give them great functionality. That can lead to some problems. My experience with domain admins, especially the customer support domain admins, the good ones, they really want to make the customer’s problems go away, they want to fix them. They will do whatever they need to do in the application in order to make that happen even if that is not exactly how you expect to see the admin tools get used and even if that means that your data winds up in a weird state or things happen that you don’t expect. You have this sort of tension between giving the admins the tools they need to do their job and yet the more power the admins have, the more abilities the admins have, the more likely they are to put something in a weird state or to change some value or something that affects the site in other ways. Administrators can, usually in this kind of system, break certain business roles. Typically, they can for instance authorize transactions at different prices or authorize discounts or authorize refunds. You need to have a way to manage that. It lets them do the things that need to be done but also allows you to sort of validate the integrity of the data and the system even when these kinds of changes happen.Charles: Do you have specific ideas around how to do that, how to communicate to people what they can or can’t, should or shouldn’t do?Noel: I think this gets really dependent on the individual parts of the system. A couple of general things, I think it’s probably a good idea to use paper trail or some sort of gem that audits changes to your database. Paper Trail is a Ruby gem and if you register an active record class with it, then any time that active record class is saved, it saves a snapshot of the previous data in the paper trail part of the database along with who made that change. That at least gives you the ability to go back and see what has happened to the data in the same way that you might get back to your Git Repo and see who changed a line of code, you can see who changed a piece of data. I think that treating administrators as users of the system in the same way you treat your users as users of the system and going through the same kind of design and user experience process that you do with actual users can really pay off here. A lot of times, that is a hard thing to get people who have limited resources to spend on a website. That’s sometimes a hard sell until the site has been running for a while and they start to see those issues happen in real time. Charles: I can tell you that one other thing related to administration, especially as you get higher up in companies, is reporting. You mentioned that before.Noel: Yeah, reporting is another thing especially on this one particular project that I’ve been referring to a fair amount. Reporting is a thing that I didn’t take super seriously at first. Reporting is how the business stakeholders in your application make decisions, it’s the information that gets presented to them. They can also be your interface with your accountants or your lawyers or whoever, but it’s also internally how they tell how is the site doing today, how much money came through today. It’s very data intensive. If you do it naively, you’ll wind up with situations where you are really stressing the site potentially when administrators want to run reports. You have some options, you can run reports as background jobs, you can partially calculate reports as time goes on, partially cache, you can cache report data like when the report is first calculated so that you don’t have to recalculate it. Every time a sale gets made on a five minute background job, you’ll recalculate the data received or something like that so that when somebody goes to look at their dashboard or the report that you give them, it happens quickly because nothing has to be recalculated. It’s also helpful if you can generate the data into some kind of intermediate format. If you can easily create your data as an array of arrays, then it’s very easy to output it as a CSV file or output it as an HTML table or put it in a PDF or create graphs out of it, getting that data in a sort of generic format can be really helpful. CSV I think is overlooked as the poor man’s reporting format. Everybody sits with this incredibly powerful analytical engine on their desktop known as Microsoft Excel. If you can get your application to spit out CSV reports, then your users can take them into Excel which is tremendously powerful at doing statistical analysis of data and go from there. It’s a good way to get that kind of thing up and running.Charles: That makes sense to me. One other thing that I’ve noticed about this, I'm not going to add anything to the discussion on reporting just because you basically covered the issues that I’ve seen with data being available immediately to the people who care about it and accuracy and things like that.Noel: If you're looking at your new relic or sky light trace and you can tell at a glance when the administrator is getting reports, that should be a warning sign.Charles: Yup, that’s a good point. One thing that I’ve seen though with money is that you kind of don’t want to screw it up, you want to test pretty thoroughly. What techniques do you recommend for this? It usually involves a third party way system, so you can’t just run it. Or you can run it against their testing system but then if you're offline or they’re offline or there’s some other issue. How do you get all of that tested and running?Noel: One of the secret things about this book which I think was also true of Rail’s test prescriptions is that they’re both secretly books about how to design Rails apps in the guys of either a book about how to test or a book about how to deal with money. I think we spend a fair amount of time in the book talking about testing and talking about data modeling and things like that. When you're looking at testing this kind of gateway, there are a couple of techniques that I really like. I really like the technique of wrapping the gateway gem or the gateway API in your own object. If you look at the source code for the book, most of the code in the book uses Stripe. Stripe has a very nice Ruby gem, we wrap everyone of it. I have our own Stripe charge class and our own Stripe account class and our own Stripe token class that do a couple of different things.One of which is they translate between the domain concepts of my application and the specific naming conventions of the Stripe API so I don’t need to have the Stripe API naming conventions go through my entire application. Secondly, they’re kind of a back stop. When testing, I can write stubs, test doubles, against those wrapper classes. I can write tests of the rest of my integrations that stop at the point of my wrapper class because it’s stubbed and then I test the wrapper class directly against the Stripe API using VCR or something like that. VCR is a Ruby gem that monitors remote HTTP calls that you make during your testing. The first time you make the call, the call goes through as normal. The VCR gem spits out this demo file with the details of the call. The second time you run the test, it takes that demo file and it takes the results from that file and treats them as though it really made the network call even though you didn’t. That allows you to run the test offline and it also allows you to run the test much faster. To some extent, it reduces the need to actually stub the wrapper class in tests because effectively you're stubbing the result of the third party call. Some combination of those things is kind of what I do. I try to have my own business logic interact with my own wrapper class. I have this wrapper class that interacts with the third party gateway. I have tests that stub the gateway using VCR. In the specific case of Stripe, there are a couple of gems that actually act specifically as fake Stripe APIs. There’s one that’s called Fake Stripe and one of them I don’t remember. I actually use the Fake Stripe gem in the book to trap the Stripe JavaScript call. I have a test that tests the browser interaction and it uses the Fake Stripe gem to return a Stripe Token so that the rest of the text can go on accurately.All of these techniques kind of work. I think that isolating individual pieces of your workflow so that they don’t interact with each other very much and that they only interact with the gateway through a single point of contact, all that stuff makes it easier to test. Like I said before, testing failure conditions with most of the gateways with known credit card numbers or known area codes that trigger various kinds of failures also needs to be a part of that.Charles: Overall, what’s kind of the point of this book? If there’s one overarching theme or idea that people should pull out of this book, what is it?Noel: I think the theme is that the API call is actually the easy part. As much as these payment gateway APIs are tremendously powerful and give you access to this ridiculously complicated credit card system so easily, within the logic of your application, that’s kind of the easy part. How your site manages over time is going to be dependent on how well you managed not making the API call but how well you managed the results of that API call and how you managed against failures and the kind of data you store and the way that you deal with authentication and security and potentially fraud analysis or all of those issues are things that are very unique to each individual site and really critical to the way that a site that takes in money is going to last overtime. I have a hard time explaining what kind of site this is about because calling it a financial site makes it sound like I'm talking about bank software. But to say it’s a site that takes in money is just weird. I haven’t come up with a graceful way to describe the kinds of sites that I'm talking about here.Charles: That makes sense. Sites usually are either information or takes some money or it could be both. There’s no special classification of website that, “Oh, this one takes money.”Noel: If your application takes in money and is using these payment gateways, then the important part is to really understand how your own business logic interacts with those gateways and how the inputs to those gateways and the outputs from those gateways are really necessary and critical to the way that your site’s going to operate.Charles: Sounds good. If people want to find out more about this topic or if they wanna get a copy of your book, what should they do for that?Noel: The book is available from Pragmatic Press. I pitched the book as Shut Up and Take My Money but they didn’t go for all that. I also want to call up the cover which is a shopping cart wire made of a mouse cord which is a fantastic image that they picked for it. It’s really great. That’s where you can get it. It’s available in beta ebook right now, the ebook will be draft complete probably in about two or three weeks and then it will go through the production process. The physical book should be out in late February or early March, I think we might’ve had a pushback of another week because we added another chapter right at the end. It’s available on Amazon for pre-order as a physical book, you can also find out information about it by following me on Twitter, I'm @NoelRap or[noelrappin.com](http://noelrappin.com) will have information about it too.Charles: Awesome. Let’s go ahead and get some picks.Noel: Sure, I do have a couple. I have two things that I want to talk about, an author and a podcast.The author is NK Jemisin. She recently just won the Hugo for Best Science Fiction Novel of the Year for a book called The Fifth Season which is outstanding. The sequel to it called The Obelisk Gate just came out. She’s written a number of really wonderful fantasy novels, The Fifth Season takes place in a world which has extinction level earthquakes on a regular basis and has a class of people who can control them or cause them and has some very interesting things to say about power and relationships with people and power and what it means to be powerful but have low status and anxiety at the same time. It’s also beautifully written, it’s wonderful. Her books are really great.The podcast is called Flash Forward. The creator’s name is Rose Eveleth and that podcast, every episode takes a potential future scenario, whether realistic or not, and starts off by presenting a couple of skits that are scenes from that future and then talks to various experts about whether it’s possible or what would happen in that case. A recent one talked about what will happen when politicians have to account for their entire social media history since they were teenagers. Another one talked about what will happen, whether it’s possible to go to a meatless future, whether vet-grown meat or something like that is possible. Another one said what would happen if every volcano in the planet went off simultaneously. There’s a wide range, it’s really good and I think a lot of people who listen to this will like it. Charles: I want to hear a zombie apocalypse episode.Noel: I don’t think she’s done a zombie apocalypse yet, I might have missed it.Charles: That sounds really interesting. I have a couple of picks this week. The first one is, this is more of a local Utah thing, but I was going to pick up my kids from school and I saw nine or ten police cars fly past. One of them slowed down long enough to indicate to me that I need to back out of the intersection because I had pulled into the intersection to turn left. It turned out that there was a bomb threat at one of the local elementary schools. They got in there, they took care of it, nobody was hurt. Anyway, I'm just going to pick police officers that do a great job all over the world. When this kind of stuff goes down, they’re running towards the danger and not away from it. I think that’s awesome.I'm also going to pick another tool that I’ve been using lately called Webinar Jam. It wraps over the top of Google Hangouts which I hear is going to be merged into YouTube as YouTube Live officially or unofficially or something. I keep hearing rumors about that but I don’t know exactly what’s going on there.Webinar Jam provides chat, polling, and a bunch of other stuff that sits in a plugin for the presenter and then it also provides those same features for participants so that they can chat with the presenter and things like that. That’s what I'm planning on using for the Ruby Rogues What Comes Next webcast that I'm doing in a couple of days. I also used it for Angular Remote Conf last week and I’ve used it for a webinar that I put on last week and another webinar that I'm going to be putting on tomorrow. Anyway, I think it’s a terrific tool, it works great, has all kinds of great analytics in it. You get the HD quality from Google Hangouts and I just can’t say enough good things about it. If that’s all we’ve got, I just encourage you to go follow Noel and check out what he’s working on because he’s always putting out good stuff.Noel: Yep, keep posted, keep looking at[noelrappin.com](http://noelrappin.com) for things about the book and follow me on Twitter for the book and whatever else I might be doing after that.Charles: Alright, we’ll go wrap this one up and we’ll catch you all next week.Noel: Great, thanks Chuck.Charles: Thank you.