Dave Coombes

Big Data

1. How did you get into Big Data?
2. What's Big about Big Data?
3. - Nothing
4. - Well, something
5. How do you approach data/analysis in an agile way
6. - The DW isn't the be-all-end-all
7. - Iterate over analytics
8. - Raw data over DW
3. Analytics Life Cycle ?
4. Quote from Dave on why he likes big data?

===============================
"What we're doing, both in the global analytics practice and certainly in Australia is we're taking the same sort of principles and approaches and practices that we would use in application development to the areas of analytics, reporting and business intelligence.

My approach was to learn "just enough" about the incumbent technologies so that I could have a meaningful conversation with people. Star-schema this and snowflake that.

Spent a not-insignficant amount of time learning about the traditional approaches. People who see most of the benefits of agile are people who've worked in another way first. This describes or codifies a better way of doing stuff.

"I will never experience the pain of a big, broken data warehouse rollout. But I know enough/spoken to enough people who wear the scars."

There are some genuinely interesting technologies, Hadoop, Dreml, BiqQuery.

=========================
Is this a separate set of tech and practices to what you'd normally use in application development? 

The technologies are different, but the approaches are similar. It sounds a bit facetiuos when I say it, but what we've just done at my last client is take a completely tactical approach to the data problem.

A strategic problem would be (eg whats everything we could possibly know about these people are the data), and then co-oerce everything into that form.

A more agile approach. Take a case, a problem we want to solve and build backwards until we've solved it. Ken Collier and John Spence(?) goes back to "What is the next most important thing, that if the business knew the answer to, they'd be able to make an informed decision."

"It's a pull based model of information, rather than a push based model of data."

=======================================
The traiditional DW model is When you draw it's like:
 - insert data sources
 - point and click ETL
 - some intermediate relationship
 - built some schemas on top of that
 - choose a reporting tool of choice
 - roll that out to people
 
Then hope that you can deliver new insights at a speed that is useful to the business. Instead go to the business people, find out what's the next most important thing you want to know, and then work from that.

=====================================
"Big data is such an overhyped term. There are few examples of 'We had these huge amount of data and then we shuffled it and you know, it told us the answer to life, the universe and everything', and (often apocryphal stories) They are few and far between, not a valid approach.

It's much better to in with a hypothesis of "This is what we think. Or is this is what we think if we had this information we'd be able to infer x, y and z. Let's go."

"It's more exploratory in a fairly-directed manner. Driven by a real business question." Eg at this client "We knew there was a bunch of disparate consumer data out there but what we really wanted to know was, can we put a user (you) into a socio-demographic segment such that we can serve you ad inventory which is more tailored to what you want. Because the more confidence you have that an advertisement is being tailored to a given user, the more you can sell that advertising space for. And obviously the benefits to the end users are that 'I see something in context thats both behaviourally and contextually relevant, that I Just see the ads as "another service this site is giving me"'".

===============================================
Why do we say "Big" data? What is the Big part of this? Or are we just talking about analysis?

They asked us this at the client. When people talk about big data, "I take it to mean, by definition almost, anything which your current tools and approaches and storage and access mechanisms can't cope with." It's beyond your capability (volume, variety, velocity, veracity).

Dependant on the business.

(GET A LINK: paper that dampens down the hype)

"We've always been at the point where we don't quite have the capacity to handle what we want." We're always overstretching. Dave's hypothesis: the reason it's grown RECENTLY, is because traditional transactional applications tend to grow linearly. "If you're a bank, you double the amount of customers, you double the amount of data." The Post-Internet boom companies (eg Google and Facebook etc) they're whole business model is based on network effects which scale n^2. THey were always going to do that.

(STILL ON BIG DATA)

When we talk to clients, not many people have a volume problem. They may have a high volume analysis (eg TWitter sentient analysis or logs) it's not their core business data. But the analysis is always very descriptive. Here's what happened last week, last month or last year. It's not particularly predictive and it's predicated on a model that isn't particularly scientific.

The "big" thing is really just you're handling more data or messier data than your technology can handle then it falls within that realm.

But we see it's people whose analytics capabilities are not supporting the needs.

===================================
I went to a conference and heard "We're making a significant shift towards more fact-based decision making. And I was kind of like, what do people usually use? Horoscopes? Gut feel?" There's now a big drive to see to be more data-analytical.

Storage isn't the critical factor and it's a solveable problem.
Also data cleaning, you spend a lot of time. Eg addresses, people make a point of storing addresses in an idiosynchratic form.

(Novel Approach?)
======================================
Pump it through Gooogle which is very good at taking something fuzzy and making it concrete and then you take that to another data source to get an identifier.

What are the other parts of the analytics practice?
(GOES WITH AGILE ANALYSIS)

The analytics lifecycle which is a way to embed analytics in your business. Identify the problem, come up with a statistical model to validate that, get the data, then iterate that. Then ultimately operationalise that within Line of Business applications. The end game is that analytics shouldn't be some sort of esoteric thing that sits off in a bunch of Excel spreadsheets that no-one really knows about, it should be something you drive into your LOB applications.

I used to hate it you know, on inceptions when people are like "Oh yeah, we'll need Reporting. And they write it on one card."

Much better to say, what's the informational metrics that you want to have, what's useful to know. Adhoc reporting even the phrase gives me the shivers. We need an extensible reporting engine.
===================================

David Johnson and Will High are our dedicated data scientists. Astrophysicists. 

If you're doing operational reporting eg something that goes to the ATO, something that is used once, then you value accuracy over special. If there are financial transactions based around this data. You may not get a chance to iterate.

"If you know nothing about your consumers, or close to nothing, then anything you learn is an improvement." So use that, the first thing we know is our gender split is (this). So you can use that. There's a trade off between accuracy and speed. Part of the skill is knowing where that balance is. If you're going to report this bottom line number to the market, you better be pretty certain around it. But in our case, do you want a +10/-10% confidence on whether you're showing this advertisement to a woman? Then yeah. Use that."

(APPROACH RAW DATA)
=======================================
Raw data vs some intermediary data. DW vs Raw Data

At a client, we found that data warehouse was influenced by the quality of the data that was coming in. In a lot of occasions they'd had to make tacit assumptions, and codify business rules about what the other applications were putting in. "It effectively means the data warehouse has become it's own semantic model." It stops being an aggregator and now becomes a place where people have made assumptions.

Try and keep things closer to the raw form as you can. We kept things close to the raw form and supplemented that with a service that says "here's our best view of that data at the moment." We stored all the raw data for the consumers, but then the service we built on top, sort of said "Here's out best view of that data at the moment." Decoupling the storage from the interpretation.


Why do you like Big Data?

I have a scientific background in theoretical physics, even though the validity of what I've done has long since passed. Still value the scientific method, posit some hypothesis and then run an experiment where that experiment is looking at your data and working out if what you *think* is true, is true. 

Sounds a bit facetious, a lot of people in TW are interested in mobile/front-end but: "I have absolutely no affinity for that at all, I have no visual design. When it moved away from green screen, a little bit of me died. So the fact that this relies on the other side of the brain is great. As a science, in a way with a real practical application. You're doing this because you're genuinely trying to improve your knowledge of a business or product.
