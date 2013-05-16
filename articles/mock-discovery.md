# Brief
This would be a satirical look at building an enterprise system through the poorly thought out approach of adding functionality into stubs until the stubs are the actual system itself. 

Length: 1000 words

The story explains how an organisation ends up with smart stubs that replicate their entire business layer and then, when production fails, they switch over to the stubs which because the stubs only cover what is tested; is actually less behaviour than prod but all the need.

# Working Draft
###### Abstract, sort of like a case study
The learning is that because we only stubbed the behaviour we used and tested they stubs are smaller than the original services and we ended up with all service (virtual) on the same platform.

Technological consolidation.

###### Where we started
No services, no tests

###### Enter the virtual service
let's bring some virtual services to stub integration

###### Stub complexity
increasing stub complexity (reuse stubs across environments, mimic systems they can't replicate, move complexity from the test into the stub)

###### Mock discovery
mock discovery to resolve mock services because there are too many

###### Prod fails and the crossover
something happens to make prod go down / have an issue
virtual services are in prod, as prod.
 
###### conclusion
This was how I learned to stop stubbing and love virtual services.