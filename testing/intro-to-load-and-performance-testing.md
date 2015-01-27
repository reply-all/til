#INTRODUCTION TO LOAD AND PERFORMANCE TESTING

In terms of testing load and performance, there are a couple of areas to be concerned with.  This introduction touches on initial latency and scalability.  Stress testing or saturation testing, also mentioned briefly, is performed in order to determine the performance of the system at capacity.  

[**Caveat -- there is a more to scalability than this touches on, but if it is the case that services are already built in a scalable fashion and you have the ability to quickly add capacity, testing should be enough to mitigate a reasonable amount of the damage but is often balanced against the cost (time and resources) of testing.  This introduction assumes that those more significant issues with scalability are not an issue.]

## Why test?

We need to test load and performance as part of our short and long term strategy. When testing, start with worst case scenarios.

In the short term, testing is done to determine whether the minimum service requirements for service performance have been met (as agreed upon in the discusion by your team or in technical specs for the product).  The basic question being asked is "When is performance good enough to consider the product ready for release?"  You are

In the long(er) term, testing is done to determine how to optimize the service and also to determine whether and where to add capacity.  


## How do we approach testing?

Start with a dialogue about the expectations around the service (how do we expect and need the service to perform, what do we expect it to do), and then design a series of experiments to determine how well we meet these expectations initially. 

When tests are developed, start with worst case scenarios, rather than average scenarios.  In related fashion, although we are concerned about the mean user, we also want to make sure that we are testing the experience of the outliers -- for example, our biggest clients, our most complex user roles, or our most involved transactions.  We design test cases to take both the worst case scenarios and outliers into consideration.

Once there are meaningful results, the data can be used to make decisions about whether we need to do anything to improve the performance of the system (i.e. the addition of capacity) and at what layers of the service those improvements should be made.

## What do we test?

### Initial latency

#### Goals
<ul>
	<li>	To determine whether we meet the minimum service requirements (as we have defined them) to say that the service is performant
</ul>
#### Questions we ask ourself:
<ul>
     <li>    How long does it to complete one transaction?
     <li>    How long does it take to complete multiple transactions serially?
     <li>    How long does it take to complete multiple transactions concurrently? 
     <li>    Does that differ? 
     <li>    Where and how is caching happen?  at what layer?
     <li>    What do I have to do to defeat caching so I am measuring the right thing (the performance of the response itself, not the effect of the cache)
     <li>    Have we run the test enough to have sufficient samples and meaningful data about performance
</ul>
### Scalability

#### Goals:
<ul>
     <li>	To assess how many requests that service can handle </li>
     <li>	To assess whether we want to or need to add capacity to our service</li>  
     <li>	To determine how we should be optimizing</li>
</ul>
#### Questions we ask ourself:
<ul>
     <li>    What happens if we increase the number of transactions 10x?  </li>
     <li>    At what point (how many requests), does the performance start to degrade?  </li>
     <li>    Can we keep increasing by 10x until we break the service completely?  Where does complete failure occur (if we get there)? </li>  
     <li>    How does it break/fail? Does it degrade gradually or all at once? </li>
     <li>    When there is a change in performance of the service, what is it driven by?  </li>
     <li>    At what layer of the service is the issue occurring (i.e. where is the resource constraint)?  </li>
     <li>    Is there a reason for the constraint (i.e. is it intentional in the design and done for a good reason?</li>  
     <li>    Has anything in the initial design decision changed that would warrant a change in our approach?)</li>
</ul>	
### Saturation/Stress Testing

#### Goals:
<ul>
     <li>	To observe the service performance under load</li>
     <li>	To observe the experience of different user types when the service is under load</li>
     <li>	To determine how we should be optimizing to improve user experience</li>
     <li>	To confirm our alerts and monitoring tools work effectively</li>
     <li>	To determine what information is produced by our alert and monitoring systems</li>
</ul>
#### Questions we ask ourself:
<ul>
     <li> How does the system perform under load?</li>
     <li> How is the user experience affected by the system load?</li>
     <li> What is the saturation point / capacity of the system?</li>
     <li> At what point, does the performance start to degrade for each user type?</li>
     <li> How does the performance start to degrade (by user type)?</li>
     <li> Are our alerts working?</li>
     <li> What information are our monitoring tools and alerts yielding?  What types of graphs or data do we need to assess our system performance?</li>
     <li> Are there things we need to do (i.e. request throttling) to improve the system performance?</li>
</ul>
## What are some types of tools used to test?

[Curl](http://curl.haxx.se/)

[Postman](http://www.getpostman.com/)

[Charles proxy](http://www.charlesproxy.com/)

[Apache JMeter](http://jmeter.apache.org/)

[Swagger](https://github.com/swagger-api/swagger-ui)
