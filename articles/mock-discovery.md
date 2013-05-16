This would be a satirical look at building an enterprise system through the poorly thought out approach of adding functionality into stubs until the stubs are the actual system itself. 

Length: 1000 words

The story explains how an organisation ends up with smart stubs that replicate their entire business layer and then, when production fails, they switch over to the stubs which because the stubs only cover what is tested; is actually less behaviour than prod but all the need.

# Article / Case Study
The learning is that because we only stubbed the behaviour we used and tested they stubs are smaller than the original services and we ended up with all service (virtual) on the same platform.

Technological consolidation.


 1. No services, no tests
 2. let's bring some virtual services to stub integration
 3. increasing stub complexity (reuse stubs across environments, mimic systems they can't replicate, move complexity from the test into the stub)
 4. mock discovery to resolve mock services because there are too many
 4. something happens to make prod go down / have an issue
 5. virtual services are in prod, as prod.

This was how I learned to stop stubbing and love virtual services.


