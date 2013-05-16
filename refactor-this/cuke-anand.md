Feature: Allow admin to suspend a sale

  Background: Create a simple Live Sale (Buyer Group)
    Given admin lrigdon logs into ove
    And Following users have logged in to manheim live
      | role       | username  | password | bid_on_behalf_of              |
      | auctioneer | jmatas    | password |                               |
      | seller     | dwoodrum  | password |                               |
      | buyer_1    | guccitown | password | TOWNSENDS MAGNOLIA NISSAN BMW |
      | buyer_2    | jcoope    | password | CONYERS NISSAN                 |
    And Live Sale is created and published with automatic run assignment
    And 2 listings are added to the Live Sale through the web service

 @live_sale_smoke_3
  Scenario: #15503 : Admin suspends and resumes the Live Sale
  # Verify admin cannot suspend the Live Sale before Preview Start Time
    Then admin verifies that they "cannot" suspend the Live Sale


    And Live Sale is updated to start now
    And auctioneer enters into the Live Sale
    And seller enters into the Live Sale
    And Following buyers have registered for the Live Sale
      | role    |
      | buyer_1 |
      | buyer_2 |
    When auctioneer starts the Live Sale

  # Admin suspends the Live Sale
    And admin verifies that they "can" suspend the Live Sale
    When admin suspends the Live Sale

    Then Following users should see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |

  # Admin resumes the Live Sale
    When admin resumes the Live Sale
    Then Following users should not see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |

  # Auctioneer starts the Live Sale
    And auctioneer sets a starting bid of 4000
    And buyer_1 bids

  # Admin suspends the Live Sale again & buyer_2 enters the Live Sale
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

  # Admin resumes the Live Sale again
    When admin resumes the Live Sale
    Then Following users should not see the splash popup
      | role       |
      | auctioneer |
      | seller     |
      | buyer_1    |
      | buyer_2    |

  # Sale continues
    When buyer_2 bids
    And auctioneer does a "Sell" on the listing
    And auctioneer does a "No Sale" on the listing
    Then admin verifies that they "can" suspend the Live Sale

  # Admin cannot suspend the Live Sale after the auctioneer has ended it
    When auctioneer ends Live Sale after all listings have run
    Then admin verifies that they "cannot" suspend the Live Sale