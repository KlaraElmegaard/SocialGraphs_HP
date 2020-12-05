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
And if you, still want to go to Hogwarts and explore the big universe and meets characters, you have come right place! \n
Using the Through network thoery, the known and unknown relationships between the fantastic and wonderful characters that appear in the universe, together with the connections between bloodtype (muggles, pure-blood e.g.) and the four houses of Hogwarts, will be analyzed. 
With natural language processing the language of the character pages, the books and manuscripts of the movies will be analysed through sentiment analysis and wordclouds.

## Data
Where do one get a lot if information? Lucky for us a huge Fandom Wiki exists for the Harry Potter Universe. We used this to download the wikipedia pages for all the characters LINK. From each wiki-page we used regular expression to get all the links but also to gather informations such af house, blood and gender. Since the language on wiki-pages are fairly neutral, we also usd text analysis to analyse the books LINK and the movie scripts LINK. Regarding the movie scrips, the sentiment of some of the main characters will be considered over time. LINK TO DATA

## Interactions Between Characters - The Harry Potter Universe as a Graph
To be able to use a lot of cool netowrk analysis, we first need to be able to represent the characters in a graph with nodes and edges. Each character will have a node. There will be an edge from lets say Harry Potter to Hermione, if Harry Potters wiki-page links to Hermione. Doing this we got a graph consisting of 3,930 nodes and 14,916 edges. Extracting the giant connected componant, the graph ended up with 2,643 nodes and 14,525 edges. Before we go any further into analysing the network, take a look at the graph below. If you hover over a node, the character name and the number of links appear. The nodes are also collered by their number of links. Can you guess who the brigth yellow node represent? Harry Potter, of cause, being the center of our unniverse. Using the toolbar in the topright, you can e.g. zoom in and out. Press the little house to reset the illustrateion. 

{% include file.html %}

## Looking into some Basic Statistics
The main statistics that we will look into here, if the degree distribution. We will do this twice, both for the in-degrees and for the out-degrees. To get an idea of our network, we first take a look at the five most commected characters both in regards to in- and out-degrees. 

| Top in-going | Character | Number of in-going links | | Top out-going | Character | Number of out-going links |
| ----- | ------------- | ------------- | - | ----- | ------------- | ------------- |
| 1: | Harry Potter | 787 | | 1: | Albus Dumbledore | 183 |
| 2: | Hermione Granger | 330 | | 2: | Harry Potter| 162 |
| 3: | Albus Dumbledore | 316 | | 3: | Ronald Weasley | 126 |
| 4: | Sirius Black | 185 | | 4: | Tom Riddle| 124 |
| 5: | Severus Snape | 177 | | 5: | Hermione Granger | 115 |





## Comparing language in books, movies and on characters pages 

| Community 1  | Community 2 | Community 3 | Community 4 | Community 5 |
| ------------- | ------------- | ------------- | ------------- | ------------- | 
| Madonna (Dance Pop)  | Kendrick Lamar (West Coast) | Paris (West Coast) | Planet Asia (West Coast) | Snoop Dogg (West Coast) |
| Britney Spears (Dance Pop)  | Chris Brown (Dance Pop) | Subnoize Souljaz (West Coast) | Dilated Peoples (West Coast) | Dr. Dre (West Coast) |
| Rihanna (Dance Pop) | Wiz Khalifa (West Coast) | Kottonmouth Kings (West Coast) | Murs (West Coast) | Ice Cube (West Coast) |
| Michael Jackson (Dance Pop) | Dom Kennedy (West Coast) | Havoc (West Coast) | Gorillaz (Dance Pop) | The Game (West Coast) |
| Janet Jackson (Dance Pop) | Tyga (West Coast) | Young Murder Squad (West Coast) | Evidence (West Coast) | Tha Dogg Pound (West Coast) |
| Lady Gaga (Dance Pop) | Problem (West Coast) | Kingspade (West Coast) | Del the Funky Homosapien (West Coast) | Kurupt (West Coast) |
| Nicki Minaj (Dance Pop) | Alchemist (West Coast) | Potluck (West Coast) | People Under The Stairs (West Coast) | Eazy-E (West Coast) |
| Mariah Carey (Dance Pop) | Ty Dolla $ign (West Coast) | Delinquent Habits (West Coast) | Pigeon John (West Coast) | N.W.A (West Coast) |
| Katy Perry (Dance Pop) | YG (West Coast) | Hed PE (West Coast) |  Domino (West Coast) | DJ Quik (West Coast) |
| Justin Timberlake (Dance Pop) | Schoolboy Q (West Coast) | Sen Dog (West Coast) | The Grouch (West Coast) | Kam (West Coast) |
