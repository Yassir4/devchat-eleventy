---
layout: layouts/post.njk
title: >
  014 AiA Using ES6 with Angular with Scott Allen
date: 2014-10-30 13:00:00
episode_number: 014
duration:
audio_url: https://media.devchat.tv/adventures-in-angular/AiA014ES6.mp3
podcast: adv-in-angular
tags:
  - adv_in_angular
  - podcast
---

The panelists talk to Scott Allen about using ES6 with AngularJS.

### Transcript

**_&nbsp;[Do you wanna have conversations with the Adventures in Angular crew and their guests? Do you wanna support the show? Now you can. Go to adventuresinangular.com/forum&nbsp; and sign up today!]_\*\***CHUCK: **Hey, everybody and welcome to Episode 14 of the Adventures in Angular Podcast. This week on our panel, we have Aaron frost.** AARON: **Hello.** CHUCK: **Joe Eames.** JOE: **Hey there!** CHUCK: **John Papa.** JOHN **: Hey everybody.** CHUCK: **I'm Charles Max Wood from devchat.tv. And this week, we have a special guest -- Scott Allen.** SCOTT: **Greetings.** CHUCK: **Do you wanna introduce yourself really quickly?** SCOTT: **Sure. I run my own company OdeToCode LLC, and do some consulting in the mid-Atlantic area of the United States. And do some PluralSight videos once in a while.** CHUCK: **Awesome. Before we get going, I also want to let people know that we're putting together a round table discussion about the mobile JavaScript frameworks like Cordova, Ionic and Famous. And so if you wanna know more about it, you can text “MobileJS” to the short code 38470 and you'll get more information about that. We're going to be doing it on the 5<sup>th</sup> of November, so if you're getting this afterward, we're sorry but we'll do other events. Today’s episode is about ES6 in AngularJS.** SCOTT: **That’s right.** CHUCK: **Do you wanna give us a starting point there?** SCOTT: **Sure.** CHUCK: **Maybe explain what it is that we're really talking about or give us a little more depth there?** SCOTT: **I can do that. Earlier this year I started looking what was going on with ECMAScript 6 and I started to get a little bit excited about the language, because JavaScript has been around for a while now but it hasn’t evolve very much. In fact, the JavaScript Jabber guys had Brendan Eich on this year, and that was just a fantastic interview. He went through a lot of the history of JavaScript and we knew that there was this time where the standards organization was trying to put something together for ECMAScript 4 and it just sort of all fell apart. And we lost a significant chunk of time where the JavaScript language could have improved or added features. But that’s all on the past and it's finally moving forward now. And I started actually working on an ECMAScript 6 course with Joe on PluralSight and getting genuinely excited about this feature. It's like I wish I was writing this today. And at the same time, I was working on an application that is sold to hospitals in the United States, so it's a commercial application and it's been around now about 11 years. And when you dig in for some of the code for this application on the server side code, doesn’t have a lot of JavaScript to it yet. Some of that code is 11 years old. It's build with the Microsoft stack and the code is C# version 1. That was a dramatically different language than what we have today with the latest version of C#. But I was looking at this application and we’re planning on adding pockets of Angular into this application, I started thinking, “It sure would be a shame if we wrote everything with today’s JavaScript. And just like this code we have now, if someone comes to this application five years for now and they look at it and they think, ‘Geez, I wish these people would had written it with ECMAScript 6.’” I started thinking after doing this course and seeing all the tools and working with other stuff that maybe we really should look at trying to start writing with ECMAScript 6 today, so that three years, four years from now when it's a lot more common place, this code will be a lot easier to work it. Is that a good background for you?** CHUCK: **That makes sense. So ECMAScript is the next version of JavaScript?** AARON: **No.** JOE: **ECMAScript 6.** CHUCK: **Isn’t that what I said?** AARON: **No.** JOE: **You just said “ECMAScript.”** CHUCK: **Oh. ECMAScript 6, yeah. ECMAScript is the standard that JavaScript is based on. Version 6 is the next version. And so, you wanna write in tomorrow’s JavaScript because it's nicer and because that’s what the people are going to be writing in in the future. Did I sum that up nicely?** SCOTT: **That’s exactly right. There's so many features in ECMAScript 6 that are very exciting. It's nothing that we couldn’t do today, it's just that the syntax is better. It's easier to read, it's easier to write, the intention is very revealing. Some things are small, some things are large. So a small thing would be like, default parameters, much easier to write with ECMAScript 6, much more obvious when you look at a function definition -- and that’s a small thing. But then big things would be like generators, iterators, classes. So now that you can write a class in JavaScript, some people find that distasteful, but I think it's genuinely useful.** JOHN: **So, Scott, let me just jump in there. That’s kind of what I'm seeing too with ECMAScript 6 is just a lot of things is pretty wicked cool, but there's others that honestly, I don’t really feel like I missed at all with previous versions of JavaScript, such as class. Not even just class itself, but the inheritance model for example. I mean, people only feel like, “I like classes or I don’t in JavaScript.” But getting into inheritance, one thing I've found coming from the .NET world or the JavaScript in the last couple of years, is at first I thought I’d miss regular inheritance. And now, I find that I really don’t ever miss inheritance. So I'm curious what your thoughts are there.** SCOTT:**I would definitely agree with that. I've long been a fan of composition over inheritance, so bringing together small pieces instead of trying to use inheritance to reuse code. I think unfortunately inheritance has been a selling point for object-oriented programming, but it's just been over emphasized for decades. And I think it's just over the last 8 or 10 years that people would come around and say, “You know, maybe inheritance isn’t that great.” So that being said, when I first saw the class feature in ES6 I thought, “Do I wanna use this? Do I not wanna use this?” And I have to say that for building an abstraction, I think classes can be pretty useful because the code sort of jumps out at you and it says, “Here’s an abstraction to represent something. An abstraction to represent local storage or an abstraction to represent a ?? that we're going to eventually data bind onto the screen.” And I don’t need inheritance for any of that. And in fact in some places, this whole in ES6&nbsp; works out pretty well. For instance, specifically when we're talking about Angular, when you register a controller with an Angular and you say, “angular.module.controller” what you're really registering is a constructor function. And when you create a class, the symbol for that class (whatever the class name is) is a constructor function. And if you can imagine the typical code that you have inside of a JavaScript file when you’re creating a controller, (and John, I know you try to address in some of the coding standards that you’ve come up with Angular and you’ve done a really good job with that), there's the sort of area in the controller where you want to initialize model stuff, and then there's typically some method calls that you need to kick something off to call into the service to get a… it needs to be call started or something like that. The class syntax I've found is actually really nice for that, because yes, the class name is your construction function, but you also have this dedicated key word constructor, where you add a function to this class that is invoked when someone uses the new keyword against your constructor function. And it's a really nice place to put your initialization logic and maybe list all of the things that are going to be data bound against those.**JOHN:**I love that. I mean, the initialization stuff in the constructors. I think that not having to do some of the patterns we do in JavaScript, I think these features really shine a light on the goodness of classes. But the part I worry about a lot honestly is when you give somebody a tool that does 20 things, (which just making up a number here) like a class, people can tend to abuse it and do things I don’t think they should. And I tend to see a lot of ES6 code right now that I'm running across where people are doing a lot of inheritance and super and they are going right back into that world. And that’s where I kind of get a little worried, iffy, if you may (pun intended) on [chuckles] having too much in my class. I love the idea of a class being a controller and getting rid of this crazy, modularity thing. But I think there’s got to be ways we can kind of control it a little bit, so that people can build things that don’t become too complex and we end up with a “seven layers of class inheritance hell.”**JOE: **I can’t wait for the first time I maintain code like that.** AARON: **So I'm over here biting my tongue because I've got some opinions on classes as well. But I'm excited to hear how we're going to use this stuff in Angular. So I'm going to avoid the whole ES6 discussion, and hopefully we can talk about how it works into Angular.** CHUCK: **I think that’s actually a good point. How does ES6 power up Angular?** SCOTT: **I don’t think there’s anything specific to ES6 that lets say would make an Angular experience better or worse. I don’t know how to explain this, but ECMAScript 6 is the language and I think the language is more beautiful. Therefore, the code that you're going to write to power Angular will be more beautiful, expressive and elegant and so forth. So that being said, there’s some things that I think ?? pretty well. For instance, using a class for a controller, I think that that’s an approach that you want to do. I think that actually works pretty well. Using a class for a service, and registering it with the .Service API that also works really well. And then there's just all the other little things that fall into place like spreads and default parameters and arrow functions that you can use in any type of JavaScript code, and will work pretty well with the Angular stuff too.** JOHN: **Can I say, “Oh, thank gee for having arrow functions.” So, so happy to have those.** CHUCK:**[Chuckles] Is that just the arrow syntax, or is there more to it than that?**AARON: **There's more to it.** SCOTT:**Yeah, there's a little more. I mean, essentially, it's a lambda… what in some language, you would call a lambda expression or some language call it a fat arrow and things like that. But one thing the arrow function does give you special in JavaScript is that it lexically binds to the outer scopes of this reference. (I'm still debating this one, actually.) You can use this reference inside of a call back if it's an arrow function and not have to worry about this reference point something else.**AARON: **Yeah. So basically, in other words, everywhere in your code where you said “var me = this” so that you can later on say “me.something” without referring to the wrong this, you don’t have to do that anymore with arrow functions. It keeps its scope on the right this.** SCOTT:**Yeah. Which is wonderful but every time I open up a JavaScript file and I see this.something, this.something, there's still something in the back of my mind that’s screaming out, “Oh, my gosh, someone is using this. It could be wrong!” [Laughter]**CHUCK: **Right. So one other thing that I'm curious about is just the barrier to writing Angular in ES6. And there were couple of things that come to my mind. One of them is my browser runs ES5, I believe. So do I have to add some extra libraries or something to kind of fill in for the ES6 functionality?** SCOTT: **You are going to have to have some sort of build process currently, today because you're going to have to take the JavaScript files that you write in ES6, and somehow transform them into ES5 so you can developer them to browsers that are running today. And I think the most popular tool to do that is Traceur. And I know you guys have had a show on that already.** CHUCK: **Yeah, we did on JavaScript Jabber.** SCOTT: **Yeah. And that’s really easy to put into your workflow. I mean, chances are you already have some sort of build system or task running that’s linting files and concatenating files, so that this will just be another step of first transpiling things from ES6 to ES5.** JOHN: **Scott, have you used 6to5?** SCOTT: **I haven’t, no.** JOHN: **It's a library. I think Dan Wahlin, I believe. I may be incorrect, but I think Dan Wahlin was telling me he was using 6to5 and I checked it out. It looks really interesting. It does a similar thing turning ES6 code into ES5 code. Because I've had my own issues. I love Traceur, but I hate it at the same time.** SCOTT:**[Chuckles]**JOHN: **But this seems to be an alternative which I hadn’t heard much about. I'm curious, have any of you folks used 6to5 yet?** AARON **: Yup.** CHUCK: **No.** JOE: **No.** JOHN:**I'll have to ask Dan about it -- if he’s even the one who told me. [Chuckles]**AARON: **He's got a lot of features in there though -- 6to5.** JOE: **Also, it's worth noting that if you're absolutely unable to do any kind of a build process at all. There is some shim libraries like ES6 shim and others where you couldn’t get a few of the ES6 without actually going through your build process. But it's pretty limiting. Like you have map and set, but you won’t get any of the new syntax that makes like class and fat arrow and things like that.** JOHN: **And there’s develop time experience, and there’s run time too, right? So develop time, use whatever you want to get there like these shims but runtime, I think we would generally not recommend putting another library in the browser to make people do that.** SCOTT: **Yeah. For example, Traceur can actually do that transpilation on the fly. You could send ECMAScript 6 code to the browser and have the full Traceur compiler down there. But that’s like a megabyte of JavaScript.** JOE: **You talked about not putting in shim libraries. It's important to note that Traceur does have an actual shim library that does have to run. It does not compile 100% of your ES6 written code to ES5 compatible code. For example, things like map and set, those are objects that just don’t exist at all in ES5. And there's no analogy to them, so you do need some shimming. So there is some shimming involved even when you’re using a compiler like Traceur.** JOHN: **Right. And Traceur mostly work on the server with your build process, but you get a couple of those things shimmed. It's not the full shim.** JOE: **Right. Sorry, let’s move on to another question.** JOHN: **Good point, man. So Scott, where does ES6 leave things like CoffeeScript and TypeScript and whatever else might be out there in the world?** SCOTT: **Personally, I think moving forward, people that are happy with TypeScript are still going to be using TypeScript because ECMAScript 6 does give you classes and lambda expressions, arrow functions, things like that. But it doesn’t give you a compilation process that checks the types and does any sort of strong typing that you can get with TypeScript. And CoffeeScript, a slightly different flavor of language, and I can still see people still using that moving forward too. Does that answer your question?** JOHN: **Yeah, I kind of was wondering where that that’s going to evolve, because I keep hearing TypeScript really is on top of ES5 and kind of looks towards being an ES6 compliant, and then has a few additional features. I wonder if that’s going to evolve now as well, I mean more like ES7, is it going to keep jumping? And then there's a ?? side which really isn’t a superset of JavaScript. It's really just shortcuts for JavaScripts. I may not be describing that really well, but it's a different way of doing transpilation. And I think people generally created that to find a better way to deal with the issues most developers have in creating JavaScript. Do you think those concerns will still be there? I guess that’s my question.** SCOTT: **I think so. Maybe when thinking about CoffeeScript not so much, but definitely Typescript is with types, that's just not something you have sets and there's a lot of people that want that, so I don’t think they would drop&nbsp; Typescript in favor of ES6 even though it has a nicer syntax for a lot of things.** JOHN: **Gotcha.** AARON: **So on that topic, I think that some people are going to prefer the route of kind of what&nbsp; we've been talking about so far which is polyfill all your stuff and make sure that you’ve got all the right polyfills and all the right build steps and kind of take care of it on your own. And then there's other people that are going to rather use something like a CoffeeScript or a TypeScript where it's going to take care of that stuff for you and you just write in whatever it is. And it will worry if you're in ES6 land or ES5 land and work the way that it needs to or not. So I think that people using CoffeeScript or TypeScript -- and I don’t -- but I think those people will possibly have an easier time upgrading their stuff to work with ES6 than the rest of us will. Again, not advocating for either those -- just saying that that’s I think how it will work.** JOHN: **Scott, who should be able to looking at moving to ES6 and when they should be looking? What's the profile of that team that should be considering it or not considering it?** SCOTT: **I’d probably wouldn’t do it if I didn’t expect the code to stick around for a bit, because although it's relatively easy, there's not too many hurdles. You have to have a build process and do this transpiling. It doesn’t really mess up too much of your workflow. If you're just trying to slam something out, the minimum, viable product or something like that, I don’t know if it's something I would consider for that sort of project. I think right now it's still forward looking, right? The spec is basically finished, but it's still in the “debugging phase” if you will, until the end of next year. Browsers are still slowly putting this stuff together. So we still have some time.** JOHN: **Yeah, as I heard on I think JavaScript Jabber, they were talking about ES7 and kind of where that’s all heading to. And one thing I worry about with a lot of this ES6 and ES7 talk is how does Angular fit into this picture? I don’t mean Angular 2.0, but I mean Angular 1.3. You mentioned how we can use some of this stuff today, but is this something that will…. I'm wondering how it's going to change the world of an Angular developer – if at all.** SCOTT: **That’s a good question. That’s something I'm still really trying to figure out. Again, a lot of those is just syntax. Things that were possible before, but it's just easier and more intention revealing. So having all these new syntax features doesn’t necessarily make programming in Angular faster or anything like that but I think it makes the code more readable. And then it’s just sort of you up to you to figure out, “Do I wanna use Class? Do I also wanna use ES6 modules and somehow work them into this thing?” It's looking at all these features and figuring out how you wanna map them. I guess the biggest thing is to me actually is classes. Do I wanna embrace classes or not? Because if you want to embrace classes as a way of building an abstraction, then you'll start thinking of controllers as being&nbsp;&nbsp; &nbsp;a class instance and services as being a class instance.** AARON: **I think classes is probably the biggest question of how does it fit in. I think what Scott is saying is true. I think everything else just kind of fits in. Like the rest of its syntax, the only real major change…&nbsp; some of those syntax though will change how we'll write Angular. For example, when you have a class or a controller function, we can do like default value stuff in functions today, and then Angular knows how to inject based on the signature of the function. But if we start putting all sorts of weird, default values and rest arguments up in our controller functions, the Angular library is not going to know how to parse that stuff out. And we're going to start getting a lot of errors. And so we are going to have limits on what we can use and what we can’t use. So, I mean like you pretty much are going to have to stay away from anywhere Angular needs to dependency inject anything. If that makes any sense.** JOHN: **What do you mean by stay away from it?** AARON: **Like, if you have a filter or any part of Angular and you wanna use like rest arguments in it, that rest argument syntax will likely break the dependency injection engine. Or if you try and like do a default value on something that's getting injected, that syntax in the places where the dependency injectors trying to look to see what needs to be injected. Those syntax is like equal signs or like a triple dot or a function call for a default value. Those kinds of things will likely break Angular’s dependency injection system. And so, anywhere where a dependency injection function like a controller or service, you're going to have to stay away from using the new ES6 syntax sugar in those function parameters. So in your scope functions, like “scope.foo = some random function,” you could use it in there, but you couldn't use it on your&nbsp; controller function because those syntaxes will likely break the 1.3, 1.2 or 1.1 dependency injection. I mean, I was just trying to point out that you can use it. You're not likely going to be able to use most of it, like if it goes up in your parameters, you can’t use for… it will probably break the dependency injection. But you could use everything like modules, you could use generators, you could use let. It should be a problem. I don’t know if classes will work or not. We'd have to test to see how the native implementation of a class, if you could just swap it out for a controller function. Because I don’t know if those controller functions get newed up. Does it call new?** SCOTT: **Yeah. If&nbsp; you register a controller using the name of your class, it all just work.** JOHN: **Beautiful. Awesome.** AARON: **That’s good. Okay.** JOHN:**[Sings] _Everything is awesome._**CHUCK:**[Chuckles]**JOHN:**Yeah. Little things too, I think are really helpful. You hit on let, and I think people underestimate the value of that even because I, myself has seen lots of codes where you're trying to scope things, and a again, a lot of people are flooding the JavaScript from Java and .NET and other lands, where these issues don’t exists. So defining a variable inside of an if statement or other places where you think scope exists, but it doesn’t really in JavaScript, I think that's where let is really going to help us create… what did you say, Scott? “More beautiful Angular code?” [Chuckles]**SCOTT: **Yeah, more beautiful Angular code. Absolutely.** JOHN:**That sounds like the title of your next course. [Chuckles]**SCOTT:**[Chuckles] I just wanna revisit it, if it's okay, this idea of using a class as a controller, just because I've gone through like 12 different iterations of, “What is the best way to create a controller for Angular?” And a couple of those iterations involve classes. It's really interesting. When you define a class in ECMAScript 6, the name of that class, that symbol, let’s say you write a class called “podcast.” Podcast is a constructor function. And Angular always treated the function that you register for a controller as a constructor function. So it uses the new keyword, so it instantiate some instance from that function.**AARON: **I never realized that. That is true. I didn’t even realize I was doing that. But yeah, you are right.** SCOTT:**It also does that when you call all the module object. If you call module.service to register a service, when it instantiates that service, it takes the function you give it and treats it as a constructor function because it uses the new keyword there. It doesn’t do that with factory or value or constant, but it does with the .Service API. So one way to write Angular code in ES6, if you want to embrace classes, is to write controllers as classes, and services as classes. And the controller one is interesting to me because I've always felt… I've never been happy with the controllers that I write in Angular. There's always something that I look at them and I wished that something was different. I have never been able to quite put my finger on it, but controllers are these interesting mix of, “Let’s initialize binding properties. Let’s kick off some calls to services. Let’s add some methods in, so that we can hook up ng-click events.” It's just those mixture of all these things. I’ve tried several different approaches to try to disentangle these things. And with classes, one of the nice things I noticed is that when you define a class, again the name of the class is your constructor function. And behind the scenes, there's a constructor function and that constructor function still has prototype property, and any methods that you add to that class, gets attached to the prototype. So it's very similar to what we've been doing in the past and like Aaron said, it's syntactic sugar for what we've always been doing. [Chuckles] But the interesting thing about a class is that there's a dedicated keyword for a constructor, and that is the code that actually gets executed when someone says, “New podcast”, “New class instance”. And one of the things I've found interesting about writing my Angular code is all of a sudden, “Oh, now I have a place to put my initialization code. I don’t have to worry about where that’s going inside of some big iffy or inside of my function.” It's very easy for me to look at a constructor function and see, “Oh, here's this property, this property, this property, this property.” And then there's a whole bunch of methods defining the class that are reachable from the view through expressions. There's a couple of good things about this and a couple of bad things about this -- and I'll try to wrap this up really quick because I know we're short on time. But one of the things that changes when you use a class and you are writing that constructor method, is that that is now your injectable function. So the parameters that you advertise on that constructor method are the things that Angular has to figure out, “How do I pass these to you using its injector?” And now, those things are scoped to that constructor. So what are you going to do with them? Well, I guess I'll save them as “\_members” inside of my object now. Whereas before, when you write Angular controller using ES5, you just have a function and things are injected, then you have ?? inside of there that close around that stuff. I've found some benefits to classes in the sense that, “Oh, I have this nice initialization logic here. And here's a list of all the methods that are going to be available.” But there's some down sides too, just in the sense that it's a little harder to form closures around things that you need. You need to think a little more about where you are going to save things like services, that you've injected. Hopefully, that all makes sense.**AARON: **John, in the style guide that you have that everyone loves, you have a syntax for injecting variables that I normally hate, and I tell people, “John got everything right besides this.” But I think using your injector syntax would probably for me, I think it would fix the problems that Scott’s explaining. And it would also fix my main problem with Angular controllers, which is like people writing code, code, code and then declaring another function and then more code, and then more functions, and more code. So it's just all kind of combobulated nightmare. And ECMAScript 6 classes and really all classes that I've worked with in languages, don’t let you write that root level code. Any code that’s going to run, has to be in a method that gets called. And Angular controllers are just horrible, ugly nightmares the way most people write them or its function expression, code expression, a watch more function expression. I think classes will clean up the way that people write controllers. And yeah, I've actually never been more excited in them now listening to kind of Scott explain some of the ways it will work. That’s cool. I'm excited.** SCOTT: **Yeah. I know John in the style guide talks about, “In the controller, put all your bindable properties upfront.” And that’s kind of what you can get with the constructor of a class.** AARON: **Yeah.** JOHN: **And that’s kind of where a lot of this stuff got models from because when we create classes, it's not that it forces you to go there, but that’s really what I was looking at was, “Why was it so easy in .NET for me to these stuff?” Well, the class structure forced you to put certain things in certain places and make easier to read even. So that’s kind of where some of this came from. It's not always just, JavaScript is getting drunk on a beach one night and, “Hey, let’s do that, man.”** CHUCK: **I was wondering.** JOHN:**[Chuckles]**AARON: **And honestly, because of the inheritance, you could probably include like some default classes like an Angular controller class, dependency injection class, or an injectable class where you could extend that for your controller. And when that gets supered up, maybe it takes care of the dependency injection problems for you. You know what I'm saying?** JOHN: **Yeah. I think it's&nbsp; where inheritance really makes sense in this new world with Angular in ES6. Not where you’ve got, you know, I&nbsp; hate the canonical, “Hey, you’ve got mammal. And it's got an animal and it's got a dog and it's got a…” “Oh come on, man get me out of that world, please.”** CHUCK:**[Chuckles]**SCOTT: **Yeah. At least on the server side, when I write server side code with languages that have classes, base controller classes have always been helpful.** JOHN: **Yeah, I always question myself. Whenever I see… I love base controllers or base classes in general, but I question myself every time I create more than one level of inheritance -- in any language. And it's not that it's a bad thing, it's I really wanna ask the question, “Why did I do this? Is it really giving me a value for doing this?” And if it's not, then I usually back off it.** SCOTT: **Yeah, there's dragons in that direction.** CHUCK: **So I wanna ask, are we ever going to get to a point where we don’t have to do the ES6 compiling song and dance? And it's not just a question of, “Okay, eventually browsers are going to support ES6, but we're still going to have to deal with older browsers.” So when do we start cutting those off and saying, “I'm sorry, but you need to upgrade your browser if you’re going to make this work.” Or are we just going to have polyfills for the difference?** SCOTT: **I sure hope so. There's this push behind evergreen browsers now and everyone seems to be trying to keep things updated. So I hope that when my grandkids are programming, they are not looking for transpilers. No matter how long it will be.** AARON: **So, Chuck, we're kind of in a similar situation today already with ES5. We all use things like Lo-Dash or jQuery that kind of take the normalcy out of programming and it's all kind of included for you. Instead of using array.map, we'll use a lo-dash map instead because we don’t wanna have to detect if the browser has the map function on the array. So we're already kind of in this transition phase with ES5. Granted, ES5 was a much, much smaller release. Way less ambitious than ES6, right? And so ES6 is going to be harder, but I think it will just work its way out, and I think the tools will make it easier to do the tools in the new language.** CHUCK:**Cool. The other question I have (and this is something that I think can be answered quickly with Yes or No and some links), are there any examples out there of people writing Angular right now with ES6?**SCOTT: **I don’t know of any. I've looked around a little bit, but I don’t see much of it as yet.** CHUCK: **Okay.** JOHN: **Yeah. I've seen very little other than just examples and demos and things. I personally have not written any apps with ES6 for Angular.** AARON: **Yeah. Can I give one last thing before we cut off, Chuck?** CHUCK: **Yeah, go.** AARON: **We've talked so much about ES6 in here. Can we just give everyone some references? I think you should go look at Joe and Scott’s PluralSight course. And I did a Frontend Masters course last month. It will be out in December. So if you're sitting here listening to this going, “What is ES6? What in the world are they talking about?” There's some really great video content online that you can go and learn about all the new features and consider how you're going to implement it in your Angular apps.** JOHN: **And I'll mention, I don’t know if you did this in your Frontend Masters course, Aaron, but in our course, we have a whole section at the end that’s just about using ES6 today. How to use transpilers, and shims and all that sort of stuff. So that’s kind of the relevant point here is how to use it today, right?** AARON: **Yeah.** CHUCK: **All right. Let’s go ahead and do some picks. John, do you wanna start us off with picks?** JOHN: **Yeah. I could do that. And I think Aaron hit the ?? there. The ES6 course is that both Aaron and Scott and Joe all have respectfully on PluralSight in front of the masters are excellent resources in general. Something else that I've been playing a little bit with lately is NightmareJS. Pretty neat stuff. So I've been doing a lot with Phantom lately, doing end-to-end testing. And it's kind of monotonous at times and I find NightmareJS is kind of cool to basically trim down the syntax to play with that. Second thing I'll put out as a pick is I've been doing a lot of research lately on Restify, Cola, Hapi, Connect, and Express, just going down the road of all these different things that serve up APIs in the server. And one thing I didn’t really think I do coming out of this was think that, “You know what, all these are pretty darn cool.” So my pick in that case is, it's an amazing Node ecosystem that we have to be able to say we can choose Restify, Hapi, Cola, any of these guys and actually build a robust web API out of them. So I'm picking Node, man.** CHUCK: **Do you have a tip?** JOHN: **My tip in this case is actually&nbsp; use tools like JSCS, JSHint, JSLint, ESLint, because even though you might write good code and solve code, those tools can really help you find issues in your process, especially, on large teams. So my tip is all those linting type tools.** CHUCK: **All right. Aaron, what are your picks?** AARON: **I'm going to pick a project called Angular Custom Elements, which it's kind of a directive system for Angular 1.2, 1.3 that allows you to kind of start using some of the web components stuff. And I hate the web component API. I think it's really hard to learn. I don’t think most people will love it, but putting it behind this Angular custom elements will allow you just write your regular Angular code and take advantage of custom elements in the browser. So that’s my pick. And my tip is make your Angular apps performant. I did a talk at AngularJS Boston last week, and it was epic on performance. So go check it out.** CHUCK: **Awesome. Joe, what are your picks?** JOE: **My pick is going to be the movie Fury with Brad Pitt. I just went and saw it last night. Really enjoyed it. It's a lot like Saving Private Ryan in its presentation. So it's kind of like brutal show, but it was a good one. I didn’t like it quite as much as I liked Saving Private Ryan, but I'm a big fan of World War Two military movies and I really enjoyed it. So that will be my pick. And for my Angular tip, my tip will be to learn to use resolve when doing routing. The resolve feature is really neat. It's very powerful. It can help you when you're doing authentication, authorization or when doing loading screens. And it's just a really cool feature. So that’s my tip is learn to use resolve in routing.** CHUCK: **Awesome. My pick, I'm just going to remind everybody about the MobileJS roundtable that we're doing. So go ahead and check that out again. And you can just find out about it by texting “MobileJS” to 38470. And my tip is you can use the angular.module not only to define modules, but also to look them up. And that way you can avoid polluting your creating global variables to keep track of your app. Scott, what are your picks?** SCOTT:**Sure. The last book I’ve read, I enjoyed it was Lock In by John Scalzi. I was a Robert Heinlein and his book always remind me of some of the Heinlein works because he has the ability to explore social and political issues involving technology, but he does it with a compelling story. Another pick would be PhysicsJS. Just something I played around with a few weeks ago or a couple of months ago. It can make things move around in the canvas, and it's pretty easy to use. I even had a blog post back then about how to wrap PhysicsJS with some custom directives and services with Angular to make it really easy to use, make it very declarative. And another pick would be for those people that travel a bit, or even if you don’t, travel.stackexchange.com. It's one of those sites that falls under the Stack Exchange and Stack Overflow umbrella. But it's fascinating if you just want to see different questions and answers about airline luggage rules and people that get into trouble with the Visas. And sometimes it's just plain funny. I mean&nbsp; you see people in there asking questions like, “I just bought a live tarantula. Can I take this on an airplane?” [Chuckles] It's bizarre. And as a tip, something I've found this week is the browser.pause() API. If your writing protractor tests that aren’t working and are driving you crazy, if you call browser.pause(), it will break into the debugger and you can actually play with developer tools in the browser and play with variables in the debugger.**CHUCK: **Very cool. All right, thanks for coming, Scott.** SCOTT: **Thank you for having me on the show. This was fun. I enjoy the podcast – all of them.** CHUCK:**[Chuckles] That’s because we have awesome hosts. All right, I just wanna thank everyone again for listening and we look forward to talking to you again next week!**_[This episode is sponsored by Mad Glory. You’ve been building software for a long time and sometimes it gets a little overwhelming; work piles up, hiring sucks, and it's hard to get projects out the door. Check out Mad Glory. They are a small shop with experience shipping big products. They're smart, dedicated, will augment your team, and work as hard as you do. Find them online at madglory.com or on Twitter at @madglory.]_\***\*_&nbsp;[Hosting and bandwidth provided by The Blue Box Group. Check them out at bluebox.net]_\*\***_[Bandwidth for this segment is provided by Cache Fly, the world’s fastest CDN. Deliver your content fast with Cache Fly. Visit cachefly.com to learn more.]_\*\*