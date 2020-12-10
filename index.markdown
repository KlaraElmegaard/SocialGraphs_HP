<style>
td {
  font-size: 11px
}
th {
  font-size: 13px
}
</style>



## Networks, data and... Harry Potter??
Were you disappointed when you turned 11 and did not recieve a letter with an owl inviting you to start at Hogwarts School of Witchcraft and Wizardry? If so, you are like us! 
And if you still want to go to Hogwarts and explore the big universe and meet the characters, you have come to the right place! 

Through network theory we will analyze the known and unknown relationships between the fantastic and wonderful characters who appear in the universe. Maybe we will discover connections between blood status (muggles, pure-blood e.g.) and the four houses of Hogwarts. Using natural language processing, we will analyze the language of the character pages, the books and scripts of the movies through sentiment analysis and wordclouds.

## Data
Where can we get enough information to create and explore the universe of characters? Lucky for us, a huge [Fandom Wiki](https://harrypotter.fandom.com/wiki/Main_Page) exists for the Harry Potter Universe. We used this to download the Wikipedia pages for all the characters. From each wiki page, we used regular expression to get all the links but also to gather information such as house, blood status and gender. Since the language on wiki pages is (supposed to be) fairly neutral, we also use text analysis to analyze the [books](http://glozman.com/textpages.html) and the [movie scripts](https://github.com/asmitakulkarni/QuoteGenerator/tree/master/harrypotterscripts). Regarding the movie scripts, the sentiment of some of the main characters will be considered over time.

## Interactions Between Characters - The Harry Potter Universe as a Graph
To be able to use our cool network analysis tools, we first need to be able to represent the characters in a graph with nodes and edges. Each character will have a node. There will be an edge from let's say Harry Potter to Hermione, if Harry Potter's wiki page links to Hermione's. Doing this, we got a graph consisting of 3,930 nodes and 14,916 edges. Extracting the giant connected component, the graph ended up with 2,643 nodes and 14,525 edges. 

Before we go any further into analyzing the network, take a look at the graph below. If you hover over a node, the character's name and the number of links will appear. The nodes are also colored by their number of links. Can you guess who the bright yellow node represents? Harry Potter, of course, as he is the main character of our universe. Using the toolbar in the top right corner, you can e.g. zoom in and out. Press the little house to reset the illustration. 

{% include Network-of-Harry-Potter-Universe.html %}

## Looking into some Basic Statistics
If you look at the plot above again, a lot of the nodes are dark blue, meaning that they have very few links/edges. So a lot of characters have a very low number of edges? We will look further into this by analyzing the degree distribution of the network. We will do this twice, both for the in-degrees and for the out-degrees. To get an idea of our network, we first take a look at the five most connected characters, both in regards to in- and out-degrees. 

| Top in-going | Character | Number of in-going links | | Top out-going | Character | Number of out-going links |
| ----- | ------------- | ------------- | - | ----- | ------------- | ------------- |
| 1: | Harry Potter | 787 | | 1: | Albus Dumbledore | 183 |
| 2: | Hermione Granger | 330 | | 2: | Harry Potter| 162 |
| 3: | Albus Dumbledore | 316 | | 3: | Ronald Weasley | 126 |
| 4: | Sirius Black | 185 | | 4: | Tom Riddle| 124 |
| 5: | Severus Snape | 177 | | 5: | Hermione Granger | 115 |

We see that the character most other characters link to is Harry Potter (surprise). Number two to five are also big characters in the Harry Potter universe. It is noticeable that Harry Potter (nr. 1) is linked to more than twice as much as Hermione Granger (nr. 2). Imagine that you didn't have prior knowledge about the universe. Then this would tell you that Harry Potter indeed is the main character. We see that Albus Dumbledore is the character who links to most other characters, closely followed by Harry Potter. Next we see that Ronald Weasley and Tom Riddle did not appear in top five for the in-degree distribution. All of this implies that there might be a correlation between the number of outgoing links and the length of a character's wiki page. 

To get a better overview, we plot the degree distribution in the two histograms below. Here we see that most characters have an in-degree of 0, meaning that no characters link to their page. This makes sense, as we have included a lot of very small (and unknown) characters. We also see that very few characters have a high number of in-going links - so few you almost can't see them on the plot. If we consider the out-degree distribution, we again see many characters with a small number of outgoing links and few characters with a high number of outgoing links. Here we again conclude that less important characters have few outgoing links - probably due to their wiki page being very short and them not having very much interaction with the other characters. 

<img src="images/histindegree.png" alt="hi" class="inline"/>
<img src="images/histoutdegree.png" alt="hi" class="inline"/>

Next, we consider the counts from the histograms above on a log-log scale. We are able to identify that both the in- and the out degree distribution resemble that of a scale free network more than that of a random network. To get a more thorough and technical explanation of this, please visit the explainer notebook (link in the bottom). 

<img src="images/llinoutdegree.png" alt="hi" class="inline"/>

## Is there a separation into houses or maybe blood status in our network?
*“Not Slytherin, eh?” said the small voice. “Are you sure? You could be great, you know, it’s all here in your head, and Slytherin will help you on the way to greatness, no doubt about that — no? Well, if you’re sure — better be GRYFFINDOR!” - Harry Potter and the sorting hat*

So now that we have a better understanding of out network, we will begin to look for patterns in the network. 

On Hogwarts, the school is separated into four houses: Gryffindor, Hufflepuff, Rawenclaw and Slytherin. In the books and films, it is obvious that the house you end up in says a lot about who you befriend and spend a lot of time with. The separation between Gryffindor and Slytherin is special -  Gryffindor as the 'good' house and Slytherin as the 'evil' house.It is therefore interesting to see if this separation is transparent in the network as well. To investigate this, we will consider the number of links within each house and compare this to the number of links between the houses. If we see more links within the houses than between the houses, we can argue for a separation between the houses. In regards to the wiki pages, this would mean that characters wiki pages is more connected (link more) to characters from the same house than chracters from different houses.

In the Harry Potter books/movies, Voldemort (the evil guy) is out to kill all muggle-borns (wizards with non-magic parents) - also known as mudbloods! Thus the books exploit the separation of pure-bloods, half-bloods, muggle-borns and of course non-magic people. It is therefore interesting to see if these distinctions appear in the network. 

We create one subgraph consisting only of characters from the four houses and one consisting only of characters from the four types of blood status. Below, the number of nodes from each house and each blood status is shown.

| Number of characters in | | | Number of characters in | |
| ----------------------- | ---- | | ----------------------- | ---- |
| ravenclaw: | 95 | | half-blood: |	83 |
| slytherin: | 163 | | non-magic people: | 185 |
| hufflepuff: | 97 | | pure-blood: | 363 |
| gryffindor: |	155 | | muggle-born: | 23 |

In total we have 510 characters in the House-graph and 654 in the Blood-graph. Since we have $4^4=16$ different possible combinations, we consider the links in a heatmap.

<img src="images/heat_houses_blood.png" alt="hi" class="inline"/>

On the left, we see that characters from Gryffindor link most to characters from their own house. The same is the case for the Slytherin house. But characters from both Rawenclaw and Hufflepuff link mostly to characters in Gryffindor. An explanation could be that Gryffindor and Slytherin are both big/important houses with important characters whereas Ravenclaw and Hufflepuff mostly consist of smaller/less important characters - thus not characters that are linked to very much.

On the right, we see that pure-bloods, half-bloods and muggle-borns all link mostly to pure-bloods, whereas non-magic people link mostly to other non-magic people. All four groups link second most to half-bloods. In general, not many characters link to non-magic people and muggle-born. However, non-magic people link mostly to non-magic people and second most to half-bloods. Thus we might see a separation between non-magic people and magic people in general. This makes sense, since we also see a clear separation of the non-magic people and the magic people in the books. Thus even though the general purpose for the evil guy (Voldemort) is to separate pure-bloods and muggle-born (partly also half-bloods), we do not see this difference in the characters' wiki pages. In general, we do not see as pronounced differences for the links with regards to blood status as for the houses.

Since we mainly saw a separation between the houses, we illustrate this graph where the nodes are colored according to house.

{% include Houses-in-Harry-Potter-fandom-universe.html %}

Overall, we saw a separation between especially the Gryffindor house and the Slytherin house, where each house linked more to its own house than to the other three houses respectively. They also linked second most to each other. If we consider the Ravenclaw and the Hufflepuff house, they linked mostly to the Gryffindor house and second most to themselves. It is interesting that they link second must to themselfs and not second most to Slytherin. This shows that Gryffindor is a bigger or more important house than Slytherin. It is also noted that the distance in how much Gryffindor links to Slytherin compared to Ravenclaw and Hufflepuff is not as big as the distance in how much Slytherin links to Gryffindor compared to Ravenclaw and Hufflepuff. I.e. Slytherin do not link very much to Ravenclaw and Hufflepuff compared to Gryffindor. This again underlines that Gryffindor is the house everything centers about, with Slytheren being the second. 


## Communities between the characters - are all characters connected as we believe?
*"You're not going mad or anything. I can see them too." - Luna Lovegood*

Communities are smaller and locally dense connected subgraphS in a network, where the nodes are more likely to connect to other nodes in the same community ([description here](http://networksciencebook.com/chapter/9#basics)). Such communities appear in the network of all the characters in the Harry Potter universe! Some are obvious, but are there communities that we did not know about? Are some enemies more connected than friends, alliances or even family? Let's find out!

Check out how the Louvian algorithm ([check it out here](https://python-louvain.readthedocs.io/en/latest/api.html)), has seperated the graph into networks.

{% include Communities-in-Harry-Potter-fandom-universe.html%}

Many nodes and many edges, but funny to surf around! Can you find Harry Potter now? If not, then look at community 11. Explore some of the characters in his community. Many of them are "undefined" something or characters without a name. Exciting! Can you find any other major characters in this community? Hint: look at the mid-bottom... Here we see the Dursleys.

Let's dig a bit deeper into these communities and the distributions of characters in each community.

<img src="images/com_dist.png" alt="hi" class="inline"/>

So the size of the communities varies a lot, but would it be meaningful to look at all of these? Let's take a look at the first five characters of a small network and of s large network.

| Community 16 | Community 1 | 
| ----------------------- | ----------------------- |
|Celestina Warbeck| Bartemius Crouch Junior|
|Ignatia Wildsmith| Alphard Black |
|Lorcan d'Eath| Iola Black|
|Devlin Whitehorn| Phineas Black|
|Derwent Shimpling| Sirius Black|

Just by looking at the first five characters, a pattern emerges: The large community contains the major characters (here Bartemius Crouch Junior and Sirius Black) and the small community only contains minor characters. That's why we look at the largest communities, so that we actually see some character that we know. Let's take a look at the 6 most connected characters in the 11 communities which contain more than 100 characters. These characters would be the ones describing the features of the community the best.

| Community 1 | Community 2 | Community 3 |Community 4 |Community 5 |Community 7 |Community 8 |Community 9 |Community 10 |Community 11 |Community 18 |
| ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- |
|Sirius Black|Ronald Weasley|Albus Dumbledore|Miranda Goshawk|Rubeus Hagrid|Gellert Grindelwald|Severus Snape|Jacob's sibling |Hermione Granger|Harry Potter|Mathilda Grimblehawk|
|Horace Slughorn|Arthur Weasley|Tom Riddle|Merlin|Tom|Nagini|Draco Malfoy|Penny Haywood|Fenrir Greyback|Vernon Dursley|Grim Fawley|
|Bellatrix Lestrange|George Weasley|Salazar Slytherin|Cadogan|Buckbeak|Newton Scamander|Dolores Umbridge|Peeves|Griphook|Dudley Dursley|Constance Pickering|
|Nymphadora Tonks|Molly Weasley|Delphini|Ivy Warrington|Olympe Maxime|Credence Barebone|Minerva McGonagall|Patricia Rakepick|Corban Yaxley|Petunia Dursley|Penelope Fawley|
|Lucius Malfoy|Remus Lupin|Aberforth Dumbledore|Daniel Page|Walden Macnair|Porpentina Goldstein|Neville Longbottom|Barnaby Lee|Xenophilius Lovegood|Hedwig|Marcus Belby|
|Phineas Nigellus Black|Ginevra Weasley|Beedle the Bard|Fay Dunbar|Amelia Bones|Jacob Kowalski|Cedric Diggory|Rowan Khanna|Travers|Arabella Figg|Walter Parkin|

You don't have to be an expert on Harry Potter to see that many of these communities are well-defined. Look at community 2 as an example. This is the big "Weasley community" containing, at least, all the most prominent characters of the Weasley familiy. This surname or familiy pattern is actually a pattern present in many of these communities. Another element that connects some of the communities is places or occupation. Community 8 is clearly a "Hogwarts" network, containing many of the important characters attending or working at Hogwarts. A last pattern we want to point out is that some of the other series of the universe also take a part in the community separation. E.g. look at community 7. Here, most characters are from the "Fantastic beasts and where to find them" movie series. The "house" and "blood status" patterns are not directly showed in these large communities, indicating that e.g. the factors described in this sections have a stronger impact on the relationships between characters than the houses and blood status do.

Feel free to further explore the communities in the graph!

## Comparing language in books, movies and character pages 
*"Because that's what Hermione does,' said Ron, shrugging. 'When in doubt, go to the library."*

We have now looked into the connections between our upcoming friendships for when we hopefully get our letter from Hogwarts soon (in an age of way too much). We are ready to meet them all, good as bad, Bellatrix Lestrange as well as Neville Longbottom! Now we go to the "library" with Hermione Granger herself and look through all the written material we can find; we are ready for the natural language processing! Here the characters' (Fandom) wiki pages, the books and the scripts for the movies (except movie 5) will be analyzed.

### Are the terminologies of pages, books and movies comparable?

The terminology of written material can roughly be interpreted with wordclouds. Wordclouds give a quick overview of which words appear the most in a given text. The wordclouds for the combined text of all characters' pages, books and movies are showed below. Any guesses on prominent words?

<img src="images/wordclouds.png" alt="hi" class="inline"/>

You guessed correctly! Of course "harry" and "potter" are two of the most common words. 

Actually, many of the words are meaningful in the different wordclouds and it is clear which wordcloud reflects each of the sources (also without the titles). The wordcloud for the characters' wiki pages show many words connected to magic, the characters and the universe overall. The wordclouds for the books and the movies also include a lot of verbs, indicating what the characters/actors do - illustrating that these are narratives and not just statements of facts.

### Sentiment of the characters - are the evil guys really the saddest?

We all know that the different characters of the Harry Potter universe have a lot of different personalities and just by reading their lines in the books or hearing their lines in the movies, we get a sense of their personalities. With sentiment analysis, we can explore this! And questions like "is Dobby actually as happy as we believe or are other characters happier?" and "is Snape really that mean/sad?" can be answered!

In this section, a sentiment analysis is performed to compare the sentiment of all characters in the Fandom Wiki. Afterwards, the sentiment of the Fandom pages of some of the main characters will be compared to the sentiment of the same characters' lines in the movies. Furthermore, the sentiment development of these characters through the movies will be explored and the sentiment of the movies and books will be compared.

A sentiment analysis is performed to rank a text on a sad/happy score based on the words used. The happpiness ranking of words are defined in the [LabMT](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0026752). The distribution of sentiments are plotted below. 

<img src="images/HistPS.png" alt="hi" class="inline"/>

Yes, it is a bit disappointing that the span between the happiest and saddest characters is so small. Are the Death Eaters actually not as bad as we assume? But nothing is as bad as it looks like! The histogram almost reflects a normal distribution (a bit skewed to the right), which we actually expected since the Wiki texts are supposed to be written in a natural language. However, it could be fun to see which characters we will meet and inviting them for at chit chat over some pumpkin juice and which we will meet with a gloomy mind, ready to cast one of the Unforgivable Curses. Thus the 10 happpiest and saddest characters are found.

| Happiest characters| Saddest characters | 
| ----------------------- | ----------------------- |
|Constance Pickering's sister| Unidentified male Death Eater during the Battle of Hogwarts (IV)|
|Constance Pickering's mother| Unidentified Hogsmeade Death Eater (II)|
|Constance Pickering's brother (II)| Unidentified Death Eater knocked out by Alastor Moody|
|Nozéa Lestrange| Unidentified male bald Death Eater|
|Constance Pickering's brother (I)| Unidentified Death Eater killed by Kingsley Shacklebolt|
|Constance Pickering's grandfather| Unidentified Death Eater in the Forbidden Forest|
|Constance Pickering's grandmother| Unidentified Black Death Eater at the Battle of Hogwarts|
|Ravenclaw Wizard's Chess champion| Unidentified Light Male Death Eater (I)|
|Unidentified 2000s Hogwarts student's parents| Unidentified wizard killed at the Quad battlements|
|Falco Tremblay|Poppy Pomfrey's Death Eater Opponent|
 
Of course the Death Eaters are the saddest characters! And beside these, the undefined ones, who have been either knocked out or killed are sad as well. It is a sad life - even their "names" indicate that. The happpiest character on the other hand, is not popular/well known. Let's take a look at the character page for the happiest character of them all [Constance Pickering's sister](https://harrypotter.fandom.com/wiki/Constance_Pickering%27s_sister). This site is short, making the good words count a lot. And with words such as "christmas" (average happiness 7.96), "mother" (average happiness 7.68) and "dinner" (average happiness 7.4), this is almost meant to be one of the most happy characters!

### But what about the main characters?
Nozéa Lestrange is the only character among the 10 happiest and saddest characters that we can put in a little connection to some major characters that we know. And that is only due to surname Lestrange. The other characters only play a minor role in the series. So our analysis above of the most happy and sad characters is a bit boring for the greater audience, which do not give a sh.. about an undefined Death Eater or someone's sister. Therefore, we provide an insight of the sentiment of some of the main characters. The sentiment of 11 of the most prominent characters' Fandom pages are compared in the table below to the average sentiment of their lines in the movies. 

| Character | Fandom sentiment | Av. sentiment of movies| Difference |
| ----------------------- | ----------- |----------- |----------- |
|Minerva McGonagall                     |5.6696                   |5.5237        |0.1459|
|Albus Dumbledore                       |5.6569                   |5.5044        |0.1525|
|Harry Potter                           |5.4590                   |5.4521        |0.0068|
|Dudley Dursley                         |5.5922                   |5.4024        |0.1898|
|Rubeus Hagrid                          |5.4393                   |5.4503        |0.0110|
|Ronald Weasley                         |5.3623                   |5.4467        |0.0843|
|Hermione Granger                       |5.4129                   |5.4930        |0.0801|
|Neville Longbottom                     |5.4043                   |5.4253        |0.0210|
|Draco Malfoy                           |5.6533                   |5.4978        |0.1555|
|Tom Riddle                             |5.3153                   |5.4572        |0.1418|
|Severus Snape                          |5.4474                   |5.5311        |0.0837|

Well done, all you Harry Potter Fandom authors out there! The sentiment of the Fandom pages matches the sentiment of the movies pretty good. The lowest difference between the two sources is for Harry Potter while the largest difference is for Dudley Dursley. Lets dig even deeper and see a possible reason for this observations. Below a plot of the characters sentiment through the movies is shown. 

XXX KLARA

First of all, lets investigate the hig/low diffrences. We see no sentiment observation for Dudley for some of the movies, while the sentiment of Harry Potter is observed in all movies. This is a pretty good reason for the sentiment difference - few words makes the sentiment approximation weaker! 

Alright, lets look at the characters development over time. Overall, most of the characters follow the same sentiment pattern and the difference between them are quite small.  The sentiment patterns of the trio (Harry, Ron and Hermione) are especially similar. Harry actually variate a bit from the other two. An explanation is that he the overall leading role! Harry is in most of the scenes in the movie. In a large proportion of these, Ron and Hermione also appear, but he also appear in many scenes without them. From the plot we might expect a bigger propotion of these in movie four and six, as these differntiate the most. In the last movie, the sentiment is almost the same for the chosen characters, except Neville who has the overall lowest sentiment here. THis seems a bit odd. The same odd observation is for Draco Malfoy in movie four, where he has the highest sentiment. That's wierd right? This could indicate that the characters don't have many lines in this moviess. Again the fewer the words the weaker sentiment analysis.

Did you get closer to you new best freinds?? We did!

Feel free to explore the sentiment even more in the interactive plot!

### How does the overall sentiment of the books and movies develop?

Now, we have explored the sentiment of each character, but do you really want to go to Hogwarts if all the overall sentiment is sad (XXX er det overall sad KLARA? ... Ok, we don't actuallty think it is. But lets look at the sentment throughout the books and movies and compare them to each other. Below, the overall sentiment of each book and movie is plotted (except the fifth book and last part of the seventh movie, as data quality for these were not good enough). Lets find out which of the seven years on Hogwarts we shall really look forward to, when we finally get our letters! 

<img src="images/PS_BM.png" alt="hi" class="inline"/>

Overall, movies are "more happy" than the books, but they follow the same pattern. The highest sentiment is in fourth and sixth movie. It is also here that we have the largest difference between the book and the movies. But why is the sentiment of the movie scripts higher than the sentiment of the books? It could be beacuse the books have to explicitly write the sad words down, which brings the score down, whereas in the movies they can just show the feelings. Looking at the y-axis, it should be noted that the overall difference is small though.

So are you excited for fourth and sixth year? We are!

### Explainer Notebook and data
- [Explainer Notebook](https://nbviewer.jupyter.org/github/KlaraElmegaard/SocialGraphs_HP/blob/main/ExplainerNotebookFinal.ipynb).
- [Initial list of character names and links used to import Fandom character pages](https://raw.githubusercontent.com/KlaraElmegaard/SocialGraphs_HP/main/data/HPC.txt)
- [Cleaned dataset 1](https://raw.githubusercontent.com/KlaraElmegaard/SocialGraphs_HP/main/data/FDS.csv), [cleaned dataset 2](https://raw.githubusercontent.com/KlaraElmegaard/SocialGraphs_HP/main/data/FDS.csv) and [cleaned dataset 3](https://raw.githubusercontent.com/KlaraElmegaard/SocialGraphs_HP/main/data/FDS.csv)
