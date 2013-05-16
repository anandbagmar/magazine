# Feature: Allow admin to suspend a sale
## Background: Create a simple Live Sale (Buyer Group)
    Given admin lrigdon logs into ove

Incidential detail. Unless your testing user authentication then this information not required.
    
    And Following users have logged in to manheim live
      | role       | username  | password | bid_on_behalf_of              |
      | auctioneer | jmatas    | password |                               |
      | seller     | dwoodrum  | password |                               |
      | buyer_1    | guccitown | password | TOWNSENDS MAGNOLIA NISSAN BMW |
      | buyer_2    | jcoope    | password | CONYERS NISSAN                |

The user names and passwords are not required here. The roles potentially useful but having buyer_1 and buyer_2 as unique for something that represents a class is a smell. Who they bid for is never mentioned again so that is also incidental detail.

    And Live Sale is created and published with automatic run assignment

And a live sale is published with automatic run assignment. Created can be implied from the fact you are publishing it.

    And 2 listings are added to the Live Sale through the web service

# Scenario: Admin suspends and resumes the Live Sale  
### Verify admin cannot suspend the Live Sale before Preview Start Time
    Then admin verifies that they "cannot" suspend the Live Sale

The "before Preview Start Time" refers to a state that a sale exists in. Don't imply state, make it a first class part of your system. I'm not sure what this state is but it might be something like 'presale'. Here is a refactored version.

    Given a Live Sale in 'presale'.
    Then the admin can't suspend the Live Sale.

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

### Admin suspends the Live Sale
    And admin verifies that they "can" suspend the Live Sale

Ok, now we can suspend the sale as it has started. So we should make this a separate test rather than a flow.

    Given a Live Sale that is in progress
    Then the admin can suspend the Live Sale.

Next.

    When admin suspends the Live Sale
    Then Following users should see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |

Ok, so now we have some behavior where logged in users are given a message when the sale is suspended. Not that the test title indicates that. 

It's also not clear why buyer_2 does not see get notified. I can't see any buyer_1 steps earlier on that show that don't include buyer_2.

I don't like to include implementation details in these tests and because of the implication that only currently online users will be notified of the Live Sale suspension, I will rewrite the behaviour.

    Given a Live sale with 2 registered users.
    When a Live Sale is suspended
    Then all registered users are notified of the suspension
    Then the auctioneer is notified of the suspension
    Then the seller is notified of the suspension
    
We notify users of the suspension but no how they are notified.

### Admin resumes the Live Sale
    When admin resumes the Live Sale
    Then Following users should not see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |
      
Here we are testing for the absence of something. Do any users see the popup? If not, how can we test for something that was never built.

### Auctioneer starts the Live Sale
    And auctioneer sets a starting bid of 4000
    And buyer_1 bids
    
The Live Sale (should be an auction) starts with an initial bid. However it's not clear if we are testing that only an auctioneer can set the starting bid or, if setting the start bid starts the auction.

    Given an auction that has not started
    Then the auctioneer can start the auction.

Or,

    Given an auction that has not started
    When the auctioneer sets the starting bid
    Then the auction has started.
    
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

### Admin resumes the Live Sale again
    When admin resumes the Live Sale
    Then Following users should not see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |
      | buyer_2    |
      
Duplicate. Delete it.

### Sale continues
    When buyer_2 bids
    And auctioneer does a "Sell" on the listing
    And auctioneer does a "No Sale" on the listing
    Then admin verifies that they "can" suspend the Live Sale

Ok, so buyer 1 and 2 have both bid now. Then the auctioneer does a Sell and then a No Sake on the listing.

What is a listing? Is that the same as a Live Sale. Is a bid a listing? We're mixing our domain terminology here. We either are talking about two things (mixing concerns) or using words interchangably.

The real verification implies that sales can be suspended but only if it is in the No Sale state.

    Given a No Sale auction
    Then the admin can suspend the auction.

### Admin cannot suspend the Live Sale after the auctioneer has ended it
    When auctioneer ends Live Sale after all listings have run
    Then admin verifies that they "cannot" suspend the Live Sale
    
Ok, so listings are back and they can run. But it seems the important thing here is that the auctioneer ends the Live Sale after the listings have run. Not that having the listenings finishing running automatically ends the auction. Therefore listings are not important.

    Given an completed auction
    Then the admin can't suspend the Live Sale.