# Dave Coombes

## Big Data

1. How did you get into Big Data?
2. What's Big about Big Data?
3. How do you approach data/analysis in an agile way
4. Analytics Life Cycle ?
5. Quote from Dave on why he likes big data?

## How did you get into Big Data

My approach was to learn "just enough" about the incumbent technologies so that I could have a meaningful conversation with people. 

I spent a not-insignficant amount of time learning about the traditional approaches. People who see most of the benefits of agile are people who've worked, and maybe failed, in another way first. This describes or codifies a better way of doing things. "And I will never experience the pain of a big, broken data warehouse rollout. But I know enough/spoken to enough people who wear the scars."

## What's so Big about Big Data?

They asked us this at my last client. When people talk about big data, "I take it to mean, by definition almost, anything which your current tools and approaches and storage and access mechanisms can't cope with." It's beyond your capability (volume, variety, velocity, veracity) and it's dependant on the business so it varies.

(GET A LINK: paper that dampens down the hype)

And it's not that new. "We've always been at the point where we don't quite have the capacity to handle what we want." We're always overstretching. Dave's hypothesis: the reason it's grown RECENTLY (ie that Big Data is interesting now), is because traditional transactional applications tend to grow linearly. "If you're a bank, you double the amount of customers, you double the amount of data." The Post-Internet boom companies (eg Google and Facebook etc) their whole business model is based on network effects which scale n^2. So they were always going to reach a problem.

But when we talk to clients, not many have a pure volume problem. They may have a high volume analysis that they need to do, (eg "Twitter sentient analysis" or logs) but it's not their core business data. 

And the analysis is always very descriptive. Here's what happened last week, last month or last year. It's not particularly predictive and when it is it's predicated on a model that isn't particularly scientific.

The "big" thing is really just you're handling more data or messier data than your technology can handle then it falls within that realm. We see it as people whose analytics capabilities are not supporting their needs.

## Approaching Big Data in an agile way.

"What we're doing, both in the global analytics practice and certainly in Australia is we're taking the same sort of principles and approaches and practices that we would use in application development to the areas of analytics, reporting and business intelligence.

(On: is this a separate set of tech and practices to what you'd normally use in application development?)

The technologies are different, but the approaches are similar. It sounds a bit facetiuos when I say it, but what we've just done at my last client is take a completely tactical approach to the data problem.

A strategic problem would be (eg whats everything we could possibly know about these people are the data), and then co-oerce everything into that form.

A more agile approach. Take a case, a problem we want to solve and build backwards until we've solved it. Ken Collier and John Spence(?) goes back to "What is the next most important thing, that if the business knew the answer to, they'd be able to make an informed decision."

"It's a pull based model of information, rather than a push based model of data."

### The DW isn't the be all end all

The traiditional DW model is When you draw it's like:
 - insert data sources
 - point and click ETL
 - store this in some intermediate, relational model
 - build some schemas on top of that
 - choose a reporting tool of choice
 - roll that out to people

Then hope that you can deliver new insights at a speed that is useful to the business. Instead go to the business people, find out what's the next most important thing you want to know, and then work from that.

### Raw data vs some intermediary data. DW vs Raw Data

At a client, we found that data warehouse was influenced by the quality of the data that was coming in. In a lot of occasions they'd had to make tacit assumptions, and codify business rules about what the other applications were putting in. "It effectively means the data warehouse has become it's own semantic model." It stops being an aggregator and now becomes a place where people have made assumptions.

Try and keep things closer to the raw form as you can. We kept things close to the raw form and supplemented that with a service that says "here's our best view of that data at the moment." and decoupled the storage from the interpretation.


### Iterate over analytics

"Big data is such an overhyped term. There are few apocryphal stories like 'We had these huge amount of data and then we shuffled it and you know, it told us the answer to life, the universe and everything' but they are few and far between, and generally not a valid approach.

It's much better to go in with a hypothesis of "This is what we think. Or: this is what we think if we had this information, then we'd be able to infer x, y and z."

"It is exploratory, but in a fairly-directed manner. It's driven by a real business question." Eg at this client "We knew there was a bunch of disparate consumer data out. And what we really wanted to know was, can we put a user (you) into a socio-demographic segment such that we can serve you ad inventory which is more tailored to what you want. Because the more confidence you have that an advertisement is being tailored to a given user, the more you can sell that advertising space for. And obviously the benefits to the end users are that 'I see something in context thats both behaviourally and contextually relevant, so that I start to see the ads as "another service this site is giving me"'" not an annoying separate stream.

If you're doing operational reporting eg something that goes to the ATO or if there are financial transactions that will be based on this data, then you value accuracy over speed and you may not get a chance to iterate. There's always going to be a trade-off between these two, and part of the skill in this field is knowing where that balance is.

"But", Dave says, "if you know nothing about your consumers, or close to nothing, then anything you learn is an improvement." If you're going to report a bottom line to the market, then you'd better be pretty certain about it. But if you want to start by increasing your confidence by 10, or 20% that you're showing an advertisement to a woman, then you can swing the lever to the speed side. 


# I went to a conference and heard "We're making a significant shift towards more fact-based decision making. And I was kind of like, what do people usually use? Horoscopes?" There's now a big drive to see to be more data-analytical.

## Analytics Life Cycle

The analytics lifecycle which is a way to embed analytics in your business. Identify the problem, come up with a statistical model to validate that, get the data, then iterate that. Then ultimately operationalise that within Line of Business applications. The end game is that analytics shouldn't be some sort of esoteric thing that sits off in a bunch of Excel spreadsheets that no-one really knows about, it should be something you drive into your LOB applications.

I used to hate it you know, on inceptions when people are like "Oh yeah, we'll need Reporting. And they write it on one card."

Much better to say, what's the informational metrics that you want to have, what's useful to know. Adhoc reporting even the phrase gives me the shivers. We need an extensible reporting engine.

## Why do you like Big Data?

I have a scientific background in theoretical physics and so I still value the scientific method, posit some hypothesis and then run an experiment to look at your data and work out if what you *think* is true, is *actually* true.

"It sounds a bit facetious", he says, "but a lot of people are interested in mobile and front-end development but I have absolutely no affinity for that at all. I have no visual design skills. So the fact that this relies on the other side of the brain is great. As a science, in a way with a real practical application. You're doing this because you're genuinely trying to improve your knowledge of a business."

