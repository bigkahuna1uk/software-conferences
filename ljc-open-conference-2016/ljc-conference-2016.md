# LJC Conference 2016

## Keynote


__An Introduction To Using NAO To Assist Children With Autism__

* Carl Clement - Emotion Robotics
* [Reason I Jump](https://www.amazon.co.uk/Reason-Jump-voice-silence-autism/dp/1444776770)

## Sessions


###Microservices###

__Daniel Bryant@OpenCredo__

* 7 Deadly Sins of Microservice
* How build a Microservice ecosystem
	* Ask if microservices are a good fit?  
		* Business value - build service around business functionality not around technology i.e. business slice. 
		* Arch principles
		* Well defined DevOps (culture, learning, metrics)
* Microservices just aggregation of good engineering practices
	* Principles more important than technology 	
* 12 factors - Don't create mini-monoliths
* Getting started - Context mapping (DDD) and Event Storming
	* [http://info.com/articles/ddd-contextmapping]()
	* [http://ziobrando.blogspot.com/2013/11/introducing-event-storming.html]()
	* ACL - Anti-corruption layer
* Testing
	* Test Pyramid 
	* See Acceptance testing blog
	* Integration test with contracts
	* Semantic monitoring in production through critical journeys of application
		* add to basket, order, payment
	* Contract testing  - Add contracts to build pipeline - Pierre Vincent
		* Pact (a bit like WSDL though with its shortcomings)
		* Pact Broker
		* Examples - Microservices-Pact 
		* Spring Cloud Contract (uses Wiremock underneath)
	* Smart endpoints, dumb pipes.  ESB may not be a good approach as introduces complexity for pipes.  
	* API gateway for separating concerns but should not house business functionality
	* 	Move from ACID to eventual consistency. Basic assertional state
	* Techonologies
		* Ratpack (reactive microservices) 
		* Lagom
		* Spring Boot for microservices
		* JEE Microprofile
		* Go microservices  
		* Docker Kubernetes	
		* Mesos/Kronos/HyperCron for scheduling jobs
		* Google RPC (GRPC) - binary protocol
	* Log monitoring
		* Dashing.io
		* Spring boot actuator
		* Logging
			* What every engineer should know
			* 10 tips for poper application logging  		* OpenTracing / Openzipkin
		* Spring Cloud Sleuth


###12 Factors###

__Daniel Bryant__

* Containerizing Continous Delivery in Java (Minibook to be published)
* Heroku apps - follwong 12 factors leads to applications that scale etc
* Now 15 factors
	* Configuration 
		* HashiCorp Volt
		* Spring Cloud Config
* Mechanical Sympathy
* Charity Majors - [O'Reilly Database migration](http://shop.oreilly.com/product/0636920039761.do)
* Bounded contexts so each participant receiving same event so services don't need to inform one another. Each may have different performance charateristics. 

###Property testing###

* Java
	* pholser: junit-quickcheck
* Kotlin  
	* Spec
	* Kotlin-Test
* Need simple examples to prove algorithm works but needs coverage by example for other cases.  
* Defining manually is cumbersome. 
* Define the rules of algorithms and let the randomized test values prove your proposition

###Java 8 Parallel Streams##

* Be wary of unintended string concatenation
* Be wary of effective final variables.  Better to collector rather than collect to variable outside the lambda
* Use specific fork-join pool rather than common one. 
	* [http://stackoverflow.com/questions/21163108/custom-thread-pool-in-java-8-parallel-stream](http://stackoverflow.com/questions/21163108/custom-thread-pool-in-java-8-parallel-stream)
* Hard to tell if stream executed in parallel or not.
* Reduce identity element
	* [https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html](https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html)
	* [http://stackoverflow.com/questions/32866581/in-stream-reduce-method-must-the-identity-always-be-0-for-sum-and-1-for-multipl](http://stackoverflow.com/questions/32866581/in-stream-reduce-method-must-the-identity-always-be-0-for-sum-and-1-for-multipl)
	* *[https://www.google.co.uk/search?q=java+streams+%2B+reduce+identity&oq=java+streams+%2B+reduce+identity&aqs=chrome..69i57j69i64l3.11751j0j7&sourceid=chrome&ie=UTF-8#safe=active&q=java+streams+%2B+reduce+identity+element+%2B+parallel](https://www.google.co.uk/search?q=java+streams+%2B+reduce+identity&oq=java+streams+%2B+reduce+identity&aqs=chrome..69i57j69i64l3.11751j0j7&sourceid=chrome&ie=UTF-8#safe=active&q=java+streams+%2B+reduce+identity+element+%2B+parallel)
	* Collectors are thread safe.
		* joins are thread local, then pairs of threads results will be joined so 8 will become 4 will become 2 will until the final result.
		* See 'joining'.  Other collectors use concurrent hashmap under the covers. 
	* Method references should be used if they're side effect free. 
	* Use mutilple stream intermidiate operations for clarity rather than a map operation doing multiple things
	* Don't construct multiple streams unless intermediate results are required. Try to construct a single stream.
	* See Cliff Click GPU talk 		

### Java 9 ###
* [http://iteratrlearning.com/articles](iteratrlearning.com/articles) - New features of Java 9
* JShell REPL
* New Collection Factory Methods  - produce immutable collections
	* But not persistent collections.   i.e. List.of(1,2) is immutable 
	* [http://openjdk.java.net/jeps/269](http://openjdk.java.net/jeps/269)
	* [Collections Refueled](https://www.youtube.com/watch?v=LgR9ByD1dEw)	
* Streams
	*   Stream.ofNullable()
	*   takeWhile/dropWhile can be used instead of filter but needs an "ordered" sequence
	*   iterate used with a terminating condition
	*   Optional
		* flatmap(Optional:stream) 
		* ifPresentOrElse improvement on ifPresent
		* orElse, orElseGet -> or.  orElseThrow still exist.    		

## Lightning Talks

* LJC should be London JVM Community not London Java Community :D
* __JCache - JSR107__
	* [cache2k](http://cache2k.org) 
	* Lock free caches - fully concurrent read/writes
	* [http://crufrex.net](http://crufrex.net)
* [BeFaster.io](BeFaster.io) - What slows you down?
	* Need quality to add more features, sustainable 
	* Hacking will work then but will slow you down in future. 
		* More refactoring to add new features.
		* Empirical data on adding new features (test study with different stages/rounds)
	*  Results:
		* Wrong abstraction
		* Unjustified complexity
		* Failing to refactor  	 

* See Derryck Jones - Empircal development 


* __Maven Mixins - Dan Haywood__
	*  Composition over inheritance
	*  Use mixen-maven-plugin.  Inline behaviour rather than inheriting from parent POM
	*  See danhaywood on github.  (TBD)

* __Making Software Documentation Fun__
	* 	[PlanText.com](PlanText.com)
	*  Structuralizer - Simon Brown

* __Tom Stuarts' Favourite Algorithm__
	* Understanding Computation
	* Impossible Programs
	* BWT Algorithm
	* See SpeakerDeck 

* __Simon Maple__
	*  RebelLabs Developer report 2016 	

## Other

- Software Architecture for Developers
- Continous Architecture
