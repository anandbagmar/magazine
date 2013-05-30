# Feature: Allow admin to suspend a sale
## Background: Create a simple Live Sale (Buyer Group)
    Given admin lrigdon logs into ove

Incidential detail. Unless your testing user authentication then this information not required.
[Anand] I agree we can hide the user details in most cases.
    
    And Following users have logged in to manheim live
      | role       | username  | password | bid_on_behalf_of              |
      | auctioneer | jmatas    | password |                               |
      | seller     | dwoodrum  | password |                               |
      | buyer_1    | guccitown | password | TOWNSENDS MAGNOLIA NISSAN BMW |
      | buyer_2    | jcoope    | password | CONYERS NISSAN                |

The user names and passwords are not required here. 
[Anand] Passwords are not required, but usernames and bid_on_behalf_of have significance in the application.

The roles potentially useful but having buyer_1 and buyer_2 as unique for something that represents a class is a smell. 
[Anand] The test opens multiple browsers, and each role (admin / auctioneer / buyer_1 / etc) represent which browser you want to execute the action in

Who they bid for is never mentioned again so that is also incidental detail.
[Anand] When registering, the buyers have to select a particular account on whose behalf they need to bid. This has implications in the subsequent steps for execution + validation

    And Live Sale is created and published with automatic run assignment

And a live sale is published with automatic run assignment. Created can be implied from the fact you are publishing it.
[Anand] The assumption is not valid in this application. 
> The sale can be created, but not published. 
> A previously created sale can be published later on,
> A sale created, but not published can be edited,
> A published sale cannot be edited, etc.

    And 2 listings are added to the Live Sale through the web service

# Scenario: Admin suspends and resumes the Live Sale  
### Verify admin cannot suspend the Live Sale before Preview Start Time
    Then admin verifies that they "cannot" suspend the Live Sale

The "before Preview Start Time" refers to a state that a sale exists in. Don't imply state, make it a first class part of your system. I'm not sure what this state is but it might be something like 'presale'. Here is a refactored version.

    > Given a Live Sale in 'presale'.
    > Then the admin can't suspend the Live Sale.

Next.
    
    And Live Sale is updated to start now
    And auctioneer enters into the Live Sale
    And seller enters into the Live Sale
    And Following buyers have registered for the Live Sale
      | role    |
      | buyer_1 |
      | buyer_2 |
    When auctioneer starts the Live Sale

This bit appears to be the setup for the following steps. I do notice however the use of the word auctioneer which implies that these Live Sales are auctions. In which case perhaps we should rename them to Auctions.
[Anand] Business uses the terminology "Live Sale" and "auctioneers". Live Sale is to indicate an online sale, compared to what this product is intending to replace - a physical sale. Hence that use.

### Admin suspends the Live Sale
    And admin verifies that they "can" suspend the Live Sale

Ok, now we can suspend the sale as it has started. So we should make this a separate test rather than a flow.

    > Given a Live Sale that is in progress
    > Then the admin can suspend the Live Sale.

[Anand] A huge problem of this application is the setup time and the concurrent access of different roles causing different behaviors.
Hence we had to combine related flows / tests into one larger test.

Next.

    When admin suspends the Live Sale
    Then Following users should see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |

Ok, so now we have some behavior where logged in users are given a message when the sale is suspended. Not that the test title indicates that. 
[Anand] In this case the test title is generic - related to the suspend sale functionality. To overcome the setup problem, we are validating various functionalities related to suspend sale.


It's also not clear why buyer_2 does not see get notified. I can't see any buyer_1 steps earlier on that show that don't include buyer_2.
[Anand] In this application, one action (by auctioneer / seller / winning buyer / losing buyers / etc.) results in different behaviors for the other roles participating in the sale. So what we do is verify behaviors for different roles where changes should be seen. However if say, 2 buyers should not see the notification, if we have validated 1 buyer, then we don't really need to validate the same thing for another buyer.


I don't like to include implementation details in these tests and because of the implication that only currently online users will be notified of the Live Sale suspension, I will rewrite the behaviour.
[Anand] Agreed. However, the splash popup does have a lot of significance. It has a specific message about the sale suspension, it also means that no other action can be done on the sale. 
Also, our tests potentially can have huge number of registered buyers in the sale. If we say "all registered users" - then we potentially need to check for all those registered users if the suspension message is seen - which does not really add a lot of value. As long as a subset of user's are verified, we should be ok. Else this will increase the test duration even more.


    > Given a Live sale with 2 registered users.
    > When a Live Sale is suspended
    > Then all registered users are notified of the suspension
    > Then the auctioneer is notified of the suspension
    > Then the seller is notified of the suspension
    
We notify users of the suspension but no how they are notified.

### Admin resumes the Live Sale
    When admin resumes the Live Sale
    Then Following users should not see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |
      
Here we are testing for the absence of something. Do any users see the popup? If not, how can we test for something that was never built.
[Anand] By not seeing the popup - the registered user can now resume normal sale activity. So yes, we can maybe reword it more appropriately.


### Auctioneer starts the Live Sale
    And auctioneer sets a starting bid of 4000
    And buyer_1 bids
    
The Live Sale (should be an auction) starts with an initial bid. However it's not clear if we are testing that only an auctioneer can set the starting bid or, if setting the start bid starts the auction.
[Anand] Each live sale has 100s of listings / vehicles part of it. Each listing is auctioned off in a particular sequence. For each listing, the auctioneer needs to set the starting bid for bidding to start.
There is a different set of rules / behaviors that occur when the live sale starts, and when starting bid is set for each listing.


    > Given an auction that has not started
    > Then the auctioneer can start the auction.

Or,

    > Given an auction that has not started
    > When the auctioneer sets the starting bid
    > Then the auction has started.
    
The buyer_1 bids thing. Not sure. It could be setup for one of the next steps.

### Admin suspends the Live Sale again & buyer_2 enters the Live Sale
    When admin suspends the Live Sale
    And Following users refresh the page
      | role    |
      | buyer_2 |
    Then Following users should see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |
      | buyer_2    |

Ok. So this appears to be a repeated test but with the implication that when a single buyer refeshes the page then all users are notified of the sale suspension.
[Anand] Not really. The app / live sale is essentially a single page which renders different information for different participants - based on roles + permissions.
The intent of the above steps is to ensure the action of one, should not affect any other participant.

### Admin resumes the Live Sale again
    When admin resumes the Live Sale
    Then Following users should not see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |
      | buyer_2    |
      
Duplicate. Delete it.
[Anand] Potentially can be deleted. Intent here was to ensure that the same live sale can indeed by suspended and resumed multiple times, and not just once.


### Sale continues
    When buyer_2 bids
    And auctioneer does a "Sell" on the listing
    And auctioneer does a "No Sale" on the listing
    Then admin verifies that they "can" suspend the Live Sale

Ok, so buyer 1 and 2 have both bid now. Then the auctioneer does a Sell and then a No Sake on the listing.

What is a listing? Is that the same as a Live Sale. Is a bid a listing? We're mixing our domain terminology here. We either are talking about two things (mixing concerns) or using words interchangably.
[Anand] Listing is a vehicle to be sold. It is a domain term. There can be a huge number of bids for each listing.
When the auctioneer sells / no sales a listing, the next listing (in appropriate sequence) comes on the block. When the auctioneer sets a starting bid amount for this new listing, buyers can again bid for it.
The above Sell is done for one listing, and the auctioneer in this case, for some reason, has directly done a "No Sale" on the next listing - instead of providing starting bid and inviting bids on that listing. This is a very real world (actual live sale) scenario - happens quite often.


The real verification implies that sales can be suspended but only if it is in the No Sale state.
[Anand] No - the sale can be suspended only when there are listings that are not yet processed in the sale. If all listings are processed, then the sale cannot be suspended.
This complete sale orchestration is quite heavily tied with the number of listings in the sale, what happens with each listing (sale, no sale, jump to run, etc.)


    > Given a No Sale auction
    > Then the admin can suspend the auction.

### Admin cannot suspend the Live Sale after the auctioneer has ended it
    When auctioneer ends Live Sale after all listings have run
    Then admin verifies that they "cannot" suspend the Live Sale
    
Ok, so listings are back and they can run. But it seems the important thing here is that the auctioneer ends the Live Sale after the listings have run. Not that having the listenings finishing running automatically ends the auction. Therefore listings are not important.

    > Given an completed auction
    > Then the admin can't suspend the Live Sale.
