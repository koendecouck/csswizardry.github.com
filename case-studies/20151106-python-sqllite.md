---
layout: post
title: "Python, SQLite"
meta: "python-sqllite"
permalink: /case-studies/python-sqllite/
next-case-study-title: "000"
next-case-study-url: /case-studies/000/
hide-hire-me-link: true
---

The following is a 2015 growth analysis case study I made for British company TransferWise.

For this assignment I received a few xlsx data tables, along with a few issues the company was interested in. I took a look at the data (<strong>MS Excel, with filters</strong>), decided to import it all to self-made local database file (<strong>SQLite</strong>) and write the interface through <strong>Python</strong>. I relied on three packages: sqlite3 (db interface), numpy (basic stats) and scipy (for doing t-tests).  

<strong>ARTEFACTS</strong>
<a href="https://docs.google.com/document/d/1vl9jYu4eWLeToT3Xx4J9RLuyutC45yHmgj88QjS1Qp4/edit?usp=sharing">View the full report</a>.

<strong>EXECUTIVE SUMMARY</strong>
These results are based on 2014 Survey responses, as relating to the TransferWise Referral Program. Within this user sample (n = 862), 11% identify as feeling ‘part of the revolution’ or ‘both [revolutionary and saving money]’ (n = 322). This group is hereafter referred to as revolutionaries. Revolutionaries differ from other users in that they refer more friends (M = 3.4, Med = 1; t = 3.5, p  < .001). Not only that, but their referred friends are also more likely to sign up than those referred by non-revolutionaries (M = 0.83, Med = 0; t = 2.5, p = 0.01). Also of interest is the highly skewed distribution of referrals, with the majority of referrals being sent by a handful of high revenue customers. These customers don’t necessarily identify as revolutionaries (Only 51% of them do). Also, most growth continue to be UK-based (60% of our general user base).
My recommendation is to follow-up with these high referring customers to see what features they still like to see. While revolutionaries might be excellent drivers of referrals, we stand to learn much from the other half of high-referrers currently neglected if only considering revolutionaries.

<strong>ANALYSIS</strong>

<strong><em>Q: Are users who consider themselves “part of the revolution” significantly better users of the referral program?</em></strong>
A: Yes, they are. Both in quantity and quality of the referral!
Revolutionaries refer on average 3 friends each (M = 3.4, Med = 1), while non-revolutionaries refer slightly less (M = 2.1, Med = 0). This difference is statistically significant, as measured by a weighted two-tailed t-test (t = 3.5, p < .001). Revolutionaries provide a higher quantity of referrals.
Similarly, if we restrict ourselves to the number of ‘successful referrals’ (i.e. where the new user actually signs up) revolutionaries also outperform other users (M = 0.83, Med = 0; t = 2.5, p = 0.01). Revolutionaries provide a higher quality of referrals too.

<strong><em>Q: What else should we know about our revolutionaries based on the data provided?</em></strong>
 A: There are big differences amongst revolutionaries. Most referrals come from a handful of very engaged individuals:

<a href="/_post_images/2015/11/transferwise-referrals.png"><img src="/_post_images/2015/11/transferwise-referrals.png" alt="transferwise-referrals" width="425" height="222" class="aligncenter size-full wp-image-6266" /></a>

As we can see here, a small group of users is driving most of our growth. Of the 1107 referrals made by revolutionaries, 172 were made by just the top four people. This is highly useful to develop our service, yet not necessarily unique to ‘revolutionaries’. The same pattern shows for non-revolutionaries. A small group of ‘high referrers’ is driving most of our growth, whether revolutionary or not.
Also of note: Most revolutionaries are males (77%). They’re likely to be without kids (68%), although this number may be inflated because of the data format (‘No kids or not answered’). User lifetime transfers is somewhat higher for revolutionaries, although the effect size is not very big (M = 12, Med = 11; t = 2.11, p = 0.04). 
The lack of certain differences can also be telling. Country-wise, the profile for revolutionaries is identical with the general user profile for TransferWise users. Most are based in the UK (59%), followed by Spain (7%), France (4%) and Germany (4%). Hence we can however rule out cultural differences. That’s surprising, you’d expect there would be some cultural differences in the perception of banks… Surprisingly, the age distribution is similar both for revolutionaries and non-revolutionaries as well. This is probably because TransferWise users tend to be predominantly young adults anyway (43% is 26 - 34 years old). Revolutionaries’ lifetime revenue also doesn’t differ compared to other users (t = -0.52, p = 0.60): while they love our service and refer us, they don’t particularly earn us more money.
Q: What would you recommend TransferWise do based on your analysis?
A: For growth, consider the user profile of high referrers instead. Apply the Pareto rule: spend 80% of your effort improving product and service for these 20% top users. Ask them what features would make our great service even more awesome to them.
According to this data set, about 20% percent of our users make more than 5 referrals to friends. (One user appears over 62 times!) Only half of these superstars self-identify as revolutionaries, so we’re missing out on a lot of feedback if we focus solely on the other half. This top 20% percent refers more AND generates significantly more life revenue (M = 105.31, Med = 33; t = x, p = x). Our revolutionaries on the other hand only referred more.

Reach out to these users, starting with the highest referrer and ask what we can do to improve our value to them. Rince and repeat.


(2) Talk among the web design staff on how to cater best to a predominantly male 24 - 36 year old, British audience while also looking appealing to our other markets (like our second-biggest one, Spain). Having multiple, parallel landing pages with subtle differences might make us look more homemade to Spanish users and convince new revolutionaries there. The same image and colour palette does not come across the same way to a Spaniard as it does to a Brit. We should also split the survey option of ‘No kids’ and ‘No answer’ next time to deeper dig into that.

<strong><em>Q: What would you recommend TransferWise to build or look into next to shed further light on this question?</em></strong>
A: It’s puzzling how dependent growth still is on UK-based individuals. Why is that? I would love to have a deeper look at user data from other countries to see if there are cultural barriers in play here. Or it might just correlate with media mentions. That too should be easy enough to check. If nothing else, other English-speaking markets like the US should be higher represented. Looking into places like Germany and Estonia might also be interesting considering our local offices there.
I also have more advanced tricks that I could use. Principal component analysis (PCA) to make a more complete profile for the revolutionaries for instance. That would show which characteristics matter the most. A/B testing on some alternative web designs (to test their effectiveness). I made a international design summary last year after tackling a similar challenge. That would be a cool project to try for TransferWise: ‘what language or visual elements appeal more to foreign revolutionaries?’
Use the data provided (green tab) to build a one-page dashboard or report to help us measure in which ways and in which subcategories performance is getting better or worse. The report should only show the last 12 weeks performance.

<strong>CASE COMPARISON: UK vs SPAIN</strong>

<a href="/_post_images/2015/11/transferwise-uk-spain.png"><img src="/_post_images/2015/11/transferwise-uk-spain.png" alt="transferwise-uk-spain" width="627" height="516" class="aligncenter size-full wp-image-6263" /></a>

<strong>PYTHON/SQL CODE FRAGMENT</strong>
The whole analysis was done from within Python, to allow me to rapidly regenerate data tables and manipulate queries. The following code fragment shows the numbers on UK referral traffic. The queries themselves are pretty straightforward, like the one generating the UK graph:
--
<code>
	weekly_GBR = []
	for i in range(27,40): #week40 is only 13, so probably still ongoing
	    cursor.execute("SELECT id from referral_weekly_data where user_addr_country = 'Gbr' AND invite_sent_week = '2014-" + str(i) + "';")
	    query = cursor.fetchall()
	    weekly_GBR.append((i,len(query)))
	print('Referrals by GBR: ', weekly_GBR)
</code>
--

The following part has some basic table drop/update management and an inner join on the revolutionaries’ id’s. It then looks at the gender split. 
I could have used a more complex query with ‘COUNT’ and more joins for this too.
-- 
<code>
	cursor.execute("DROP TABLE IF EXISTS revolutionaries;")
	cursor.execute("CREATE TABLE revolutionaries(id INT NOT NULL PRIMARY KEY, id_user TINYTEXT);")
	cursor.execute("SELECT distinct id_user FROM survey_responses where survey_responses.question_response = 'Revolutionary' or survey_responses.question_response = 'Both';")
	query = cursor.fetchall()
	for i in range(0,len(query)-1):
	    cursor.execute("INSERT INTO revolutionaries VALUES(" + str(i+1) + ",'" + query[i][0] + "');")

	cursor.execute("SELECT question_response from survey_responses inner join revolutionaries  on survey_responses.id_user = revolutionaries.id_user where question = 'Gender';")
	query = cursor.fetchall()
	print('Gender (revolutionaries')
	print(Counter(elem[0] for elem in query))
	print('########')
</code>
--


---

{% include promo-next.html %}
