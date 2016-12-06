# Clojure X 2016

__01/12/2016__

## Angular Must Die - Here are some weapons

- Are all programming languages are basically the same ??
- Blub Paradox - All programmers have language they look down on but should also look up for aspirational languages
- Clojure reinvigorated interest. 

###Clojure

What Clojure taught me?


- Syntax doesn't matter.  Less is more
- Learn with community i.e. London Clojure Dojo
	- [BrainF*ck](https://en.wikipedia.org/wiki/Brainfuck)
- Programming languages are just programs. No ceremony should be involved.
- Design for human use i.e. write for humans not computers.
	- Design matters 	 
	- See Phiilip Wadler - Language design i.e. difference between a designed language and ad-hoc language.  	 
- Data modelling is the biggest idea in programming. i.e. representation is important
	- Data description should be the first design goal 
- Then transform data. Ship. 
	- TDD is oppposite.  Functional is model data first then behaviour rather than other way round.  
- Functional, compose behaviour to get result rather than imperatively define steps.  
	- See slugify example in Java and Clojure (using comp macro)

- [Japanese War Tuber](https://en.wikipedia.org/wiki/War_tuba)
- Effects
	- Interface with outside world
		- IO monad (io! ...)
			- Blows up in atom as atom may retry multiple times i.e. non-idempotent
		- Core Async  (<! ...)
	- Effects define the scope
	- Tracking effects 
	- Category theory - practical use to avoid incidental complexity (monoids, monads)
- DataModelling + Processing + Waste Management -> Good System
	- Design -> Data -> Process Building -> Effects  (Pyramid)
	- Most languages don't treat data as a primary concern unlike Clojure, Elm etc

- New new innovation in CS is a misnomer i.e. nothing new in last 30 years. Should be reading new papers as eventually they'll bear fruit in the future. 

Kris and Chris Howe-Jones - Data first vs OOP thinking of nouns first and then the behaviour

## Persistence and Clojure

- Not talking about persistence data structures but durable data i.e. disk, databases

- Data is simple, storage is the complication
- Mccarthy LISP machine - dump the whole image to disk
	- Restore the image as a whole = Transparent Persistence
- Clojure doesn't has transparent persistence so need other approaches
- Save the whole world
	- REPL
	- Ring middleware
		- Intercept request and responses so can intercept for/at persistence middleware.  i.e. Read and Print at REPL
	- See github hanshuebner/quizzbuzz.  	  
## Streaming with Kafka and Onyx - Jason Bell 

- Stream App = Data in + Process + Data Out
- See Jason Bell - Oynx/Kafka example


## Lightning Talks

### How we been sucking our eggs wrong (Picking the right abstraction) - Andy

- Hydra - Library for deeply nested data structures (maps, vectors, sets)
- Simple rules -> interesting consequences
- Tricky to manipulate/understand deeply nested structures
	- CircleDB paper. Hard to decipher
- Solutions
	- Zippers
	- Lenses
	- Specter
	- Ad-hoc solution
- Sidenote_ Wills 
	- Leave amount to charity -> benefits to recipients of Will
	- __Alan Perlis__ - Better to have 100 functions on one datastructure than otherway round. 
- Hydra uses the 'Egg of Columbus'
- Trees are maps of path onto values
	- to-path-map
	- from-path-map
	- upsert   
	- And more operators
- adwelly on github

### Quil

- CLJ/CLJS for graphics
- Gavile on github

### Klipse - Game of Life   (http://slides.klipse.tech)

- REPL in the browser. 
- Hilarious double act.  Morecambe and Wise would be proud :D. 
- [https://github.com/viebel/klipse](https://github.com/viebel/klipse)

## Clojure for Machine Learning

* Bandit Testing
	* Inference  
* Regresion models
* Neural Networks
* [kixi.stats](kixi.stats)
* See cortex on Github	
* [https://github.com/henrygarner/cljx-december-2016](https://github.com/henrygarner/cljx-december-2016)  

## Mathematical Modelling in Clojure - Sunny Townsend

- Q:  How many people will live in London in 2040?
- numerics : A Clojure numerical analysis library 
- [http://witan-alpha.mastodonc.com/](http://witan-alpha.mastodonc.com)

### Log All The Things - David James Humphreys


- Good logs will save you
- Is this really tech debt?
- Goals
	- Read them
	- Search/Filter
	- Respond to them i.e. monitoring
	- Calibrate them
	- Unify them 
- Buy versus Build    (Unicorn company???)
- Failure is always an option 
	- Bugs in apps
	- Network will fail
	- Services will fail
- Just use UTC. Don't deal with timezones. 
- Use structural logging i.e. JSONequse or key-value pairs.
	- Log message should be a data structure i.e. {:time 32392893, :host 192.168.388.323}
	- log4json
	- logstash-appender
- Use consistent keys
- Have a application context
- Have a request context.  Create a correlationId so you can correlate the request as it's processed through the system
- Stacktraces
	- Repurpose stack tracce into structured form
- Uncaught Exceptions
	- Catch unexpected ones and log at a set point. 
- Shutdown logging
	- Use shutdown hooks to know when app has been shutdown
- JVM logging
- Classloader logging
- Housekeeping 
	- Clean up your deps
	- Require you log lib early and exclude others
- Print to StdOut is an option.
	- Let OS level framework handle consuming and aggregating
- clojure.tools.logging - abstraction layer for Clojure
	- macros enabled
	- timbre - Simple to use and configure (just a map)
	- can filter sensitive information
- Log events not just raw data. Meaningful or contextual logs
- [https://juxt.pro/blog/posts/logging.html](https://juxt.pro/blog/posts/logging.html)    	    	



## Immutability - USwitch - Christian Ralph

- Benefits
	- No side effects
	- Thread safe
	- Deterministic
- Reframe - pattern for single page apps in CLJS using Reageant
	- Pure functions operating on immutable data
- Append only approach.  Value approach i.e. sequence of events
	- Rewind the clock to see state of system at any time  

- Legacy System 
	- Use a service that regularly polls and snapshots legacy system.  And also sends events.  	
	- AWS streams provides this out of the box
- Also use immutability for deployment
	- Docker images
		- Slower build times
		- Simpler in long run


Immutabilty is not just for code:

- Reframe and React		
- Append Only
- Streams of facts
- Derived static APIs
- Transform Legacy systems
- Docker		 


__02/12/2016__

## Writing a Framework in Clojure - luke@cognitect.com ##

- General purpose web framework for Clojure
- Several libraries
- General
	- Differences bewtween lib and framework
		 - You call a lib
		 - A framework calls you  i.e. IOC - you write small bits of code that framework will call. 
		 	 - If think of a tree, leaves are the parts to plug in  
	 		 - The tree is the framework    
	 - Library denotes you can use it but framework are more opioniated. You have to follow a paradigm. 
	 - Modularity benefits
	 	-  Application structure
	 	-  Aware of other modules
	 	-  Well defined extension points
	 		- Higher-level structures than just code APIs
	- Flexibility
		- Lots of options
		- Low cost to consume/switch modules
	- Security
		- Built in to framework by default as opposed to using a library where you're responsible
	- Domain
		- Language concepts vs application concepts
		- Frameworks define software entities
		- Higher "starting point"
	- Tradeoffs
		- Heavyweight
		- Requires conceptual buy-in 	  	  	  

- Arachnae
	- Be in Clojure
	- Rapid development
	- Shallow learning curve
	- Highly modular
	- Lower the ramp up time to be producative i.e relationship betwwen effort and scale.   i.e. hard to build a blog in Clojure but easy in Wordpress.

	- Configuration
		- Everything is data
		- Traditional config elements
		- Defines all the entities
		- Defines a schema 
			- Ontology of application
			- Concepts and relations
	- Where is the Design?
		- Reify concepts -> design change -> manipulate data in configuration
		- More flexibility
		- Code should not have to be refactored to any great extent. Should be isolated. 
		- Changes in the configuration has big changes
	- Modules
		- Provide code
		- Configuration schema
		- Configuration build time
	- Runtime
		- Find components from config
		- Uses Sierra components

		
	- Demo [https://github.com/arachne-framework/demo](https://github.com/arachne-framework/demo)

	- Status
		- Done
			- Module/Config systems
			- HTTP services
			- Abstract asset pipeline
			- Abstract data layer
		- TODO
			- Public Alpha Jan 2017
			- Kickstarter perks
			- Funding through March/April         	
	- [Architectural Decisions](https://github.com/arachne-framework/architecture)


## Asynchronous Ring - James Reeves @weavejester ##

Why do we need async?

- Fewer idle threads
- Performance 
- Future CLJS support

Async Ring

- Sync handlers
- Async handlers
- Non-blocking IO in future

- Immutable is simple but not performant, mutable is complex but performant.  Need a half way house.

- Going from simple to performant should be easy
- Shape of the code should remain similar 
- AR uses callbacks:
	- request
	- respond
	- raise - thrown after function ended
	- throw - thrown whilst function running

- Middleware
	
- Results
	- performant
	- backward compatible
	- midlleware works the same
	- no exotic syntax

-  Streaming responses
	- response body can be:
		- String
		- Seq
		- File
		- InputStream

	- For 1.6 these become a StreamableResponseBody
- Non-blocking IO??
	- Breaks backward compatibility.  request:body expects a blocking inputstream
	- Every Java web server handles NIO differently
	- Intended for 2.0  	   	

 
 
 ## CIDER: Inside the Brewery 	 	
 
 - [Spacemacs](https://github.com/syl20bnr/spacemacs)  or Emacs
 - CIDER most popular, Cursive catching up
 - 2016 - Has autotest mode like Infinitest, hover over symbol with mouse gives docstring
 	- Cider now has a [manual](https://cider.readthedocs.io/en/latest/)
 	- __New release 0.14 Berlin__ 
 		- Shows Clojure Spec in code buffers
 		- Bug fixes, improvements
	- clj-refactor
	- clojure-mode
	- inf-clojure

	
## CLJS on Electron

- Electron are apps built in [Atom](https://en.wikipedia.org/wiki/Electron_(software_framework)), similar to Eclipse framework for Java
- Project Spotlight: ClockWork
	- Time tracker
	- Can be used offline
	- Easy access to data
	- Integration with other apps
- Descjop - Lein template for electron 

Technologies used:

- Clojurescript easier to use than other languages. More productive
- Regeant supplies good abstraction layer but multiple ways to define a component
- Reframe - pattern for single page applications in CLJS/Reagent
	- Data Layer
	- Query Layer
	- View Layer
	- Control Layer

- [https://github.com/bru/clockwork-electron](https://github.com/bru/clockwork-electron) 


## Lightining Talks

### Skyscraper - Restructuring the Web - Daniel Janus @nathell

- Not as simple as recursive wget with Perl
	- Lose contextual information
- enlive scraping a little better solution but only suitable for single pages
- Run in technical issues i.e. HTTP errors, timeouts etc

- [Skyscraper](https://github.com/nathell/skyscraper)
	- Structrual scraping
	- Based on enlive
	- Scrapes data as tree structure
	- Based on the [List Monad](https://www.schoolofhaskell.com/school/starting-with-haskell/basics-of-haskell/13-the-list-monad)
	- Keeps context when scraping
		- Context
		- Processor
		- Results

### Terrorital Prisoner's Dilemma - Peter Westamcott - Strategic Blue

- [Critical Mass by Phillip Ball](https://www.amazon.co.uk/Critical-Mass-Thing-Leads-Another/dp/0099457865)
- Timothy Prately - Figwheel and Reagent
- Nash equilibirum
- [Prisoner's Dilemma](http://peterwestmacott.github.io/non-games/prisoners/index.html)
- Iterated Prisioner's Dilemma


### Stateful streaming with Kafka - Will Hamilton - Funding Circle

Porco Rosso Anime

- Evolution from offline to real-time analysis of data i.e. Hadoop to Storm -> Dataflow model (Google) -> Kafka streams (Confluent)
- Kafka Streams (Available in Kafka)
-	Library not a framework
	-	Windowing 
	- One at a time processing
- Stateful processing  - single event may not be important but a group of events maybe is:
	- Joins
	- Aggregations  	 
- Use a lot of Java interop though.  Use .. macro similar to threading macro
- Can filter streams using predicates and pipe to other Kafka streams etc

## Speculative Development - USwitch - Andrew McVeigh

- Why use Spec?
	- Data validation
	- Generative testing
	- Richer documentation
	- Example of parsing code
- What is it?
	- Predicate function
	- Arbitrary funtion
	- Ser of valus
- Can be named
- Conforms to a spec protocol i.e. valid or invalid
- Can return a generator for a spec if possible.  Probably for simple data types. But you can write your own generators
- See different types of spec. 
- Critiscm - Spec data is opaque. 
- USwitch use Spec with Swagger  
- Clojure Spec is a DSL 
- Other languages exist though
- Can be used to describe valid Ring routes etc. 
- Can be used at boundary of application to assert inputs/outputs are valid.  
	- Push generated data at boundaries
-  Spec delivers more value though?
	- AST
- [Speculate](https://git.hub.com/uswitch/speculate)  
- [https://github.com/uswitch](https://github.com/uswitch)

## Modern web apps with Rum - Nikita Prokopov

[Rum](https://github.com/tonsky/rum)

- HTML UI library for CLJ and CLJS
- Buidling UIs
	- Complex with mutable state, big

- Evolution: 
	- ReactJs 2013
	- Om 2013
		- Centralized state atom
		- Async rendering
		- Leveraged immutability
	- Reagent 2014
		- Reactive atoms
		- Hiccup syntax
	- Quiscent 2014
		- Minimal
		- No state model
		- Pure functional, no OOP  (Luke VanderHart)
	- Rum 2014
		
		
- Motivation
	- Borrow good stuff from other libraries
	- Mix Om, Reagent, Quiscent
	- Be compatible with any storage not just DataScript
	-  Be future proof

- Solution
	- Don't commit to particular approach i.e. non-opioniated 
	- Build for extension 	

- Rum is:
	- library not a framework
	- Non mandatory state model
	- Open architecture
	- Clear mappings from Rum to React
	- Minimal codebase ~900 LOC

- Core Concepts
	- Component
	- State
	- Mixins  

- Server side rendering	
	- Uses Sablono (server-side Hiccup)

- Rum is bad for
	- Doesn't teach you to write apps as open-ended. If learning then use a structured framework and when understand OM/Reagaent better than use Rum.  

##Serverlisp - Nigel Runnels-Moss

[https://github.com/sleepyfox](https://github.com/sleepyfox)

BDD = Beer Driven Development

- Google Cloud Functions (alpha)
- XKCD Lisp - Star wars references
- [Servless]()
	- AWS Lambda
	- Jay Kreps - I Heart Logs - Event Data, Stream Processing and Data Integration
	- 12 factor app
- [Staying Lean with Application Logs](http://www.slideshare.net/SamirTalwar/staying-lean-with-application-logs) - noodlesandwich.com
- Sibilant - Javascript with a LISP.  Lightweight compared to Clojure
- [Stathat](https://www.stathat.com) - Stats as a service
- Unit testing
	- Mocha
	- Jasmine
- Integration testing
	- Awkward as system it's deployed to is a blackbox. 
- Deploymemnt
	- Zip
	- FTP
	- AWS S3 bucket
- Forget about REPL.  Println debugging

##Living with Spec @sbelak - simon@goopti.com

- Parsing with Derivatives - Dianiel Spiewak
- parsing-with-derviates-regular.html
- Spec enables:
	- Validation
	- Error reporting etc    	
- ''Composition is about decomposing'' - E.Normand
	- [https://purelyfunctional.tv/issues/clojure-gazette-192-composition-is-about-decomposing/](https://purelyfunctional.tv/issues/clojure-gazette-192-composition-is-about-decomposing/)
- Now using Spec beforehand Prismatic Schema
- Validation
	 - API boundaries
	 - Structured errors
	 - Fail fast = more context	
	 - nil punning
	 - Multiple arities  
	 - Friendlier error messages
	 	- Pluggable explanations
	 	- Capture common mistakes
	 	- Provide hints
	 	- Limitations
	 		- One explainer funcation for all
	 		- Don't know whish spec, only what went wrong 
 		- Destructuring
 			- Pull apart and name
 			- Patterns
 				- case (dispatch on tag)
 				- core.match
			- Separate data decription and transformation 
- Data macros to transform data to a canonical form 
- Generative testing
	- Limitations
		- akward with time series i.e. sequences with internal structure
		- generic higher order functions
	- Uncovers numeric instabilities
	- s/exercise for mocking  
- Queryable data descriptions
	- Build a graph
	- No inline docs though

	
	
# Living Clojure - Juxt - Jon Pither

- Henry Marsh - All My Worst Mistakes
- Before was focused on:
	- 100% 
		- Test coverage
		- DDD
		- Pair Programming
		- CI
		- Kickoffs, showcases, retros every iterarion
- Learning technology should uplifts us
- Introduce Clojure piecemeal
	- Small service first
- Blog: Clojure at a Bank - Moving from Java
	- Someone else wrote - Clojure in a bank (Malcolm Sparks)
- Learning: Keep it small and tidy
- Learning: Continual improvement
	- State i.e. component
	- Schemas i.e. clojure.spec
- Learning: Peter Naur - Programming as Theory Building
	 - Need a plan when MVP becomes a legacy product
- Learning: Best lang != $$$ consulting :D
- Learning: Sales is a thing. Need a proper Sales pipeline
- Clojure Learnings
	- Hiring still needs attention
	- Smart != Getting Things Done (Joel Spolsky)
	- The Lisp Curse - Rudolf Winstock 
		- Lisp power is its own worst enemy
	- Software is not a democracy
		- Still need tech leads, smell dangers, awareness
		- Not flat           	  	  	
	- Companies will need to change
	- Try to spread the Clojure message

__Book by 4th December £95 + VAT for 2017__ 








