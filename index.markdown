<style>
td {
  font-size: 11px
}
th {
  font-size: 13px
}
</style>

## Networks, data and... Harry Potter??

Was you disappointed when you turned 11 and did not recieved a letter with an owl inviting you to start at Hogwarts, School of Witchcraft and Wizardry? If so, you are like us! 
And if you, still want to go to Hogwarts and explore the big universe and meets characters, you have come right place! 

Through network thoery, the known and unknown relationships between the fantastic and wonderful characters that appear in the universe, together with the connections between bloodtype (muggles, pure-blood e.g.) and the four houses of Hogwarts, will be analyzed. With natural language processing the language of the character pages, the books and manuscripts of the movies will be analysed through sentiment analysis and wordclouds.

## Data
Where do one get a lot of information? Lucky for us a huge [Fandom Wiki](https://harrypotter.fandom.com/wiki/Main_Page) exists for the Harry Potter Universe. We used this to download the wikipedia pages for all the characters. From each wiki-page we used regular expression to get all the links but also to gather informations such af house, blood and gender. Since the language on wiki-pages are fairly neutral, we also use text analysis to analyse the books LINK and the movie scripts LINK. Regarding the movie scrips, the sentiment of some of the main characters will be considered over time. LINK TO DATA

## Interactions Between Characters - The Harry Potter Universe as a Graph
To be able to use the cool netowrk analysis, we first need to be able to represent the characters in a graph with nodes and edges. Each character will have a node. There will be an edge from lets say Harry Potter to Hermione, if Harry Potters wiki-page links to Hermione. Doing this we got a graph consisting of 3,930 nodes and 14,916 edges. Extracting the giant connected componant, the graph ended up with 2,643 nodes and 14,525 edges. Before we go any further into analysing the network, take a look at the graph below. If you hover over a node, the character name and the number of links appear. The nodes are also colored by their number of links. Can you guess who the brigth yellow node represent? Harry Potter, of cause, being the center of our universe. Using the toolbar in the topright, you can e.g. zoom in and out. Press the little house to reset the illustrateion. 

{% include file.html %}

## Looking into some Basic Statistics
If you again look at the above plot, a lot of the nodes are dark blue meaning that they have very few links/edges. Thus the main statistics that we will look into here, is the degree distribution. We will do this twice, both for the in-degrees and for the out-degrees. To get an idea of our network, we first take a look at the five most connected characters both in regards to in- and out-degrees. 

| Top in-going | Character | Number of in-going links | | Top out-going | Character | Number of out-going links |
| ----- | ------------- | ------------- | - | ----- | ------------- | ------------- |
| 1: | Harry Potter | 787 | | 1: | Albus Dumbledore | 183 |
| 2: | Hermione Granger | 330 | | 2: | Harry Potter| 162 |
| 3: | Albus Dumbledore | 316 | | 3: | Ronald Weasley | 126 |
| 4: | Sirius Black | 185 | | 4: | Tom Riddle| 124 |
| 5: | Severus Snape | 177 | | 5: | Hermione Granger | 115 |

We see that the character most other characters link to is Harry Potter (surprise). Number two to five is also big characters in the Harry Potter Universe. One notices that the number of other characters linking to Harry Potter is more than twice as big as for Hermione Granger (number two). It makes sense that most characters from the Harry Potter Books link to Harry Potter. We see that ALbus Dumbledore is the character that links to most other characters closely followed by Harry Potter. Next we see Ronald weasley and Tom Riddle who with did not see in top five for the in-degree distribution. 

To get a better overview, we plot the degree distribution. First in two histograms below. Here we see that most has an indegree of 0, meaning that no characters link to their page. This makes sense as we have included a lot of very small character that was unknown to us. We also see that very few characters has a high number of ingoing links. If we consider the out-degree distribution, we again have that most characters have a small number of outgoing links and few characters with a high number of outgoing links. Here we again look at the less importent characters not have very many outgoing links - probabaly due to their wiki-page being very short and them not having very much interaction with other characters. 

<img src="images/histindegree.png" alt="hi" class="inline"/>
<img src="images/histoutdegree.png" alt="hi" class="inline"/>

If we next consider the above histograms on a log-log scale, we a able to identify that both the in- and the out degree distribution resembles that of a scale free network more than that of a random network. To get a more thorough and technical explanation of this, please visit the explainer notebook. 
<img src="images/llinoutdegree.png" alt="hi" class="inline"/>



## Is their a seperation of the houses or maybe the blood-types in out network?
*“Not Slytherin, eh?” said the small voice. “Are you sure? You could be great, you know, it’s all here in your head, and Slytherin will help you on the way to greatness, no doubt about that — no? Well, if you’re sure — better be GRYFFINDOR!” - Harry Potter and the sorting hat*

So now that we have a better understandig of out netowrk, we will begin to dig deeper in the network. 

On Hogwards, the school is seperated into four houses: Griffendor, Hufflepuff, Rawenclaw and Slytherin. In the books and films, it is obvious that which house you end up in says a lot about who you befrind and spend a lot of time with. The seperation between Griffendor and SLytherin and especially - Griffendor as the 'good' house and Slytherin as the 'evil' house. It is therefore interesten to see if this separation is transparent in the network as well. To investigate this, we will consider the number of links within each house and compare this to the number of links between the houses. If we see more links within the houses than between teh house, we can argue for a sepearation between the houses. This meaning that characters wiki pages is more connected (link more) to characters from the same house than chracters from different houses. 

In the Harry Potter books/movies, Voldemort (the evil guy) is out to kill all muggle-borns (wizards with non-magic parrent) - also known as mudbloods! Thus the books exploit the seperation of pure-blood, half-bood, muggle-born and of cause non-magic people. It is therefore interesting to see if we see the same seperation in the network. 

We create one subgraph consisting only of characters from the four houses and one subgraph consisting only of characters from the above four blood-types. 

| Number of characters in | | | Number of characters in | |
| ----------------------- | ---- | | ----------------------- | ---- |
| ravenclaw: | 95 | | half-blood: |	83 |
| slytherin: | 163 | | non-magic people: | 185 |
| hufflepuff: | 97 | | pure-blood: | 363 |
| gryffindor: |	155 | | muggle-born: | 23 |

Since we have $4^4=16$ different posibilities, we consider the links in a heatmap

<img src="images/heat_houses_blood.png" alt="hi" class="inline"/>

On the left, we see that Griffendor characters link most to characters from their own house. The same is the case for the Slytherin house. But characters from both Rawenclaw and Hufflepuff links mostly to characters in Gryffendor. An axplanation could be that Gryffendor and SLytherun is both big/importent houses with importing characters whereas Ravenclaw and Hufflepuff mostly consists of smaller/less importent characters - thus not characters that are linked to.

On the right, we see that pure-bloods, half-bloods and muggle-borns all link most to pure-blood where non-magic people link mostly to other non-magic people. All four group links the second most til half-bloods. In generel not many characters link to non-magic people and muggle-born. All in all, we do not see as pronounced differences for the blood as for the houses. We see that half-bloods, muggle-borns and pure-bloods link mostly to pure-bloods. All three also links the second most to half-bloods. On the other hans non-magic people links mostly to non-magic people ad second most to half-bloods. Thus we might see a seperation between non-magic people and magic people in general. This makes sense, since we also in the book see a clear seperation of the non-magic people and the magic people. Thus even though the generel purpose for the evil guy (Voldemort) is to seperate pure-bloods and muggle-born (partly also half-bloods), we do not see this deference in the wikipages of the characters.

Since we mostly saw a seperation between the houses, we illustrate this graph where the nodes are colored per house.

{% include Houses-in-Harry-Potter-fandom-universe.html %}

All in all we saw a seperation between especially the Griffendor house and the Slytherin house, where each house linked more to its own house than to the other three houses respectively. They also linked second most to each other. If we consider the Ravenclaw and the Hufflepuf house, they linked mostly to the Griffendor house and second most to them selves. It is interesting that they link second must to them selfs and not second most to Slytherin. This shows that Griffendor is a bigger or more importens house than Slytherin. It is also noted that the distance in how much Griffendor links to Slytherin compared to Ravenclaw and Hufflepuf is not at big as the distance in how much Slytherin links to Griffendor compared to Ravenclaw and Hufflepuf. Meaning that Slytherin do not link very much to Ravenclaw and Hufflepuf compared to Griffendor. This again underlines that Griffendor is the house everything centers about with Slytheren being the second biggest. 


## Communities between the characters - are all characters connected as we believe?
*"You're not going mad or anything. I can see them too." - Luna Lovegood*

Communities are smaller locally dense connected subgraph in a network, where the nodes are more likely to connect to other nodes in the same community [1](http://networksciencebook.com/chapter/9#basics). Of course the network of all characters in the Harry Potter universe forms such communities! Some are obvious, but is there communites that we did not know about? Are some enimies more connected than friends, alliances or even family? Let's find out!

Check out how the Louvian algorithm[2](https://python-louvain.readthedocs.io/en/latest/api.html), has seperated the graph into networks.

{% include Communities-in-Harry-Potter-fandom-universe.html%}

Many nodes, many edges, but funny to surf around! Can you find Harry Potter now? If not, then look at community 11. Explore some of the characters in his community, many of them are "undefined" or characters without a name, exciting! Can you find any other major characters in this community? Hint, look at the mid-bottom... Maybe the Dursleys.

Let's dig a bit deeper into these communities, and the distributions of characters in each community.

<img src="images/com_dist.png" alt="hi" class="inline"/>

So the size of the communities variate a lot, but would it be meaningful to look at all of these. Let take a look at the first five characters of a small network and and large.

| Community 16 | Community 1 | 
| ----------------------- | ----------------------- |
|Celestina Warbeck| Bartemius Crouch Junior|
|Ignatia Wildsmith| Alphard Black |
|Lorcan d'Eath| Iola Black|
|Devlin Whitehorn| Phineas Black|
|Derwent Shimpling| Sirius Black|

So just by looking at the first five characters a pattern is shown: The large community contains the major characters (here Bartemius Crouch Junior and Sirius Black) and the small community only containing minor characters. That's why we look at the largest communities, so that we actually see some character that we know. Lets take a look at the 6 most connected characters in the 11 communities that contains more than 100 characters. These characters would be the ones, describing the features of the community the best.

| Community 1 | Community 2 | Community 3 |Community 4 |Community 5 |Community 7 |Community 8 |Community 9 |Community 10 |Community 11 |Community 18 |
| ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- | ----------------------- |
|Sirius Black|Ronald Weasley|Albus Dumbledore|Miranda Goshawk|Rubeus Hagrid|Gellert Grindelwald|Severus Snape|Jacob's sibling |Hermione Granger|Harry Potter|Mathilda Grimblehawk|
|Horace Slughorn|Arthur Weasley|Tom Riddle|Merlin|Tom|Nagini|Draco Malfoy|Penny Haywood|Fenrir Greyback|Vernon Dursley|Grim Fawley|
|Bellatrix Lestrange|George Weasley|Salazar Slytherin|Cadogan|Buckbeak|Newton Scamander|Dolores Umbridge|Peeves|Griphook|Dudley Dursley|Constance Pickering|
|Nymphadora Tonks|Molly Weasley|Delphini|Ivy Warrington|Olympe Maxime|Credence Barebone|Minerva McGonagall|Patricia Rakepick|Corban Yaxley|Petunia Dursley|Penelope Fawley|
|Lucius Malfoy|Remus Lupin|Aberforth Dumbledore|Daniel Page|Walden Macnair|Porpentina Goldstein|Neville Longbottom|Barnaby Lee|Xenophilius Lovegood|Hedwig|Marcus Belby|
|Phineas Nigellus Black|Ginevra Weasley|Beedle the Bard|Fay Dunbar|Amelia Bones|Jacob Kowalski|Cedric Diggory|Rowan Khanna|Travers|Arabella Figg|Walter Parkin|

You donøt have to be an Harry Potter expert to see that many of these communities are well-defined. Just look at community 2. This is the big "Weasley community" containing, at least all the most prominent characters of the Weasley familiy. This surname or familiy pattern are actually a pattern presented in many of these community. Another element that connects the community is places or occupation. Community 8 is clearly a "Hogwarts" network, containing many of the important characters attending or working on Hogwarts. A last pattern, among many others that can be explored in the graph, we want to point out is that the universe part series also have takes a part in the community seperation. Look at community 7, mostly containing characters from the "Fantastic beasts and where to find them" movies series. The "house" and "blood-type" patterns, are not directly showed in these large communities, which indicates that e.g. the factors described in this sections, have a stronger impact on the relationships between the characters.

Feel free to further explore the communities in the graph!

## Comparing language in books, movies and on characters pages 
*"Because that's what Hermione does,' said Ron, shrugging. 'When in doubt, go to the library."*

We have now looked into the connections between our new friendships, when we in the hopefully soon get our letter from Hogwats (in an age of way to much) and we are ready to meet them all, good as bad, Bellatrix Lestrange as Neville Longbottom! So now we go to the "library" with Hermione Granger herself and look all thw written material we can find - we are ready for the natural language processing! For this part the character pages of the Fandom wiki, the books and the manuscripts for the movies (besides movie 5) will be analyzed.

### Is the terminology of pages, book and movies compareable?

The terminology of wrttien material can roughly be interpreted with wordclouds. Wordclouds gives a quick overview of which words that apears at most in a given text. The wordclouds for the combined text of all character pages, books and movies are showed below respectively.

<img src="images/wordcluds.png" alt="hi" class="inline"/>

You've? Of guessed it! Of course "harry" and "potter" are two of the most common. 

Actually many of the words are meaningful in the different wordsclouds and it is almost clearly to see which wordcloud that reflects each of the sources (also withour thee titles). While the wordcloud for the character pages showing many words that are connected to magic, the characters and the universe overall, the two other wordclouds also showing a lot of verbs, related to what the characters/actors do. 

### Sentiment of the characters - is the evil guys really the saddest?

We all know that the different characters of the Harry Potter universe have a lot of different personalities and just by reading their speech in the books or hearing their lines in the movies, we get an intuition about the this personality. With sentiment analysis, we can explore this! And questions like "is dobby actual as happy as we believe or are other characters happier?" can be answered!
In this section a sentiment analyzis is performed to compare the sentiment of all characters of the Fandom Wiki. Afterwards the sentiment of the Fandom pages of some of the main characters, will be compared to the sentiment of the same characters given by the lines in the movies. Furthermore the sentiment development of these characters through the movies will be explored and the sentiment of the movires and books will be compared.

A sentiment analyze is performed to happiness rank a text, due to the words that is used. The happpiness ranking of words are defined in the [LabMT](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0026752). The distribution of sentiment are plotted below. 

<img src="images/HistPS.png" alt="hi" class="inline"/>

Yes it is a bit disappointing, that the span between the happiest and saddest characters is so small. Is the Death Eaters actual not as bad as we assume? But nothing are as bad as it looks like! The histogram almost reflects a normal distribution (a bit skewed to the right), which we actually expected since the Wiki texts are supposed to be written in a natural language. However it could be fun to see which characters we should meet with the happy face and which we should meet with a gloomy mind, ready to cast one of the Unforgivable Curses. Thus the 10 happpiest and saddest characters are found.

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
 
Of course the Death Eaters are the saddest characters! And even the undefined ones, that has been either knocked out or killed... OR ARE BALD! It is a sad life - even their "names" indicates that. The happpiest character, on the other hand, thet are nor popular. Let's take a look at the character page for the happiest character of them all [Constance Pickering's sister](https://harrypotter.fandom.com/wiki/Constance_Pickering%27s_sister). This site is short, making the good words count a lot. 
 
[View Explainer Notebook here](https://nbviewer.jupyter.org/github/KlaraElmegaard/SocialGraphs_HP/blob/b7e9289e5e11f6d094204dc59c0d2ea6b877fd11/ExplainerNotebook.ipynb)
