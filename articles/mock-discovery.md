# Brief
This would be a satirical look at building an enterprise system through the poorly thought out approach of adding functionality into stubs until the stubs are the actual system itself. 

Length: 1000 words

The story explains how an organisation ends up with smart stubs that replicate their entire business layer and then, when production fails, they switch over to the stubs which because the stubs only cover what is tested; is actually less behaviour than prod but all the need.

# Working Draft
###### Abstract
What started out as a way of trying to cope with an inter-weaved tangle of services resulted in us having simpler service implementations, no enterprise service bus, a test automation suite, a single consolidated platform for all services and I could sleep at night. Nobody told us this would be achieved when we started with Virtual Services. If they had, we wouldn't have believed them.

###### Where we started
To explain how we go there I have to back to where we started. This won't surprise anyone whose worked in our industry. We had many services all hanging off our ESB. Embedded vendors were brought in on a cheapest cost model which meant they produced new changes and new services using only manual tests. Things became harder to change, production would break frequently. It has horrible and I was having a hard time sleeping.

We knew we had to bring in test automation but we just couldn't do it. We would deploy on Tuesdays and Thursdays and the tests would break. We'd waste time getting them fixed before we could start shaking out the new build.

###### Enter the virtual service
The change started when one of our consultants told us to try out virtual services. We build a fake version of our dependencies so we can isolate the behaviour of our services. They promised that this would make our tests more reliable.

They were right but as consultants always do, they missed the point and solved one problem by slicing out lots of little problems for others to solve. These little problems were that each virtual service we created could only serve a handful of tests. We started having to manage all these miniture virtual services.

"I don't want any more single use virtual services being deployed into the Cross Enterprise Acceptance Test (CEAT) Environment!" I yelled across the development floor. I had lost it.

###### Test complexity
The next problem we faced was that our tests had lots of duplicated behaviour and they were'nt well written. So we asked our virtual service developers to move the behaviour out of the tests and into the virtual services. The mantra was "simple tests" and printed out on a banner on the development floor.

###### Introducing Stub complexity
So the team came on the weekend and we devised a thin layer that would sit above our micro virtual service and would route the incoming message to the correct handler based on some data in the message. The routing was also tested by using a virtual consumer to put our virtual service into the sytem under test role.

###### Mock discovery
In production we used an ESB and all the messages would route through it. We couldn't affort one for our CEAT environment so our services were communicating directly with each other. It was a risk but one we accepted because our ESB was routing messages using SOAP headers. The behaviour was similar but these were just too many services. The virtual service layers did help but it wasn't enough.

We did some research and this kind of problem can be solved using a service registry. So we built a mock service registry. 

[continue]

###### Prod fails and the crossover
something happens to make prod go down / have an issue
virtual services are in prod, as prod.

Then we realised the ESB wasn't even being used. So we sold it to one of our competitors. It was the first real saving we made.