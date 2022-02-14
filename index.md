<script type='text/javascript' src='https://public.tableau.com/javascripts/api/viz_v1.js'></script>
 

 

                    <div class='tableauPlaceholder'>

                        <object class='tableauViz' width='100%' height='100%' style='display:none;'>

                            <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' />

                            <param name='embed_code_version' value='3' />

                            <param name='site_root' value='' />

                            <param name='name' value='MinimumWageSized&#47;Dashboard2' />

                            <param name='tabs' value='no' />

                            <param name='toolbar' value='yes' />

                            <param name='showAppBanner' value='false' />

                            <param name='filter' value='iframeSizedToWindow=true' />

                        </object>

                    </div>
                    # Free Music Archive: An Analysis of Popular Artists, Albums and Songs

Free Music Archive (FMA), founded in 2009 by radio station WFMU, offers free access to open licensed, original music.

In this data story I plan to explore the currently available FMA data to answer the following questions:

1. What genre of artist post their music to the Free Music Archive? 
2.	Who are the popular artists on the Free Music Archive?
3.	What are the popular albums on the Free Music Archive?
4.	What are the popular tracks on the Free Music Archive?
5.	Is there a correlation between listens and interest?
6.	Where are the popular Free Music Archive artists located?


Metadata

The FMA provides 917 GiB and 343 days of Creative Commons-licensed audio from 106,574 tracks from 16,341 artists and 14,854 albums, arranged in a hierarchical taxonomy of 161 genres. The dataset was published in 2017 and contains data from 2009 to 2017.  

There are 9 datasets included in the FMA GitHub repository but for our purposes I focused on a select portion of metadata from 2 data tables. I analyzed these two data tables separately because they don’t have a common key for a union or join. I analyzed a select portion of data information on the following variables:

genre.csv
-	genre title
-	#tracks 

tracks.csv
-	artist name 
-	track title
-	#listens 
-	interest
-	album title
-	album type 
-	album #listens 
-	location 
-	longitude 
-	latitude
-	genres_top
-	active_year_begin


Cleaning
The data I am interested in analyzing was organized well so there wasn’t much of cleaning to be done. I utilized Tableau Prep to clean up the column headers and remove unwanted columns. I created a custom calculation in Tableau Prep to calculate how long each individual artist has been active on the website. I used the artist_date_created column which provides a date for when each artist became active on the website. Since the data table includes data up to and including 2017 I decided to create a DATEDIFF calculation between artist_date_created and 2018-01-01.

Artist Duration Calculation Field
-	DATEDIFF('day',[artist date_created], #2018-01-01#)



What genres of music are available on the Free Music Archive?

My initial question when looking at the data is who uses the FMA? Initially, I wanted to find out what are the most popular genres on the FMA but I found that many artists categorize themselves by multiple genres for their music. It was difficult to analyze top genre based on the artist “listens” or “interest” data because of the overlapping and multiple genres. 

<script type='text/javascript' src='https://prod-ca-a.online.tableau.com/javascripts/api/viz_v1.js'></script><div class='tableauPlaceholder' style='width: 1640px; height: 914px;'><object class='tableauViz' width='1640' height='914' style='display:none;'><param name='host_url' value='https%3A%2F%2Fprod-ca-a.online.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='&#47;t&#47;charlesroberts' /><param name='name' value='GenreBook&#47;Dashboard1' /><param name='tabs' value='no' /><param name='toolbar' value='no' /><param name='showAppBanner' value='false' /></object></div>

I analyzed genre title and the number of tracks for each genre which shows that Experimental, Electronic and Rock genres have the highest number of tracks on the FMA compared to the other the music genres. These results suggest that creators of Experimental music are predominant users of the FMA.   


Who are the most popular artists on the Free Music Archive?

I want to know who is the most popular artist on FMA but this can be a tricky question because there are a lot of ways to measure whether an artist is popular or successful. For my analysis I measured an artist’s popularity on the FMA by listens and interest counts of their songs.

Bar - artist/listens

The above bar chart shows the artists with the largest amount of track listens. The chart shows us that Podington Bear has the largest amount of track listens with a count 7,287,253.

Bar - artists/interest

The above bar chart shows the artists with the largest amount of interest. The chart shows us that Podington Bear has the largest amount of interest with a count 9,922,230.

Counting the number of listens and interest is a good indicator of the popular artists on FMA but I also wanted to measure how long they have been active on the website. If an artist has been active on the FMA for a long period of time they would have more time to gain listens and interest.
 
Bar - # of days artist has been on the site

The above chart shows the number of days the most popular artists have been active on the FMA. I used a calculated field to calculate the artist duration on the FMA by using the DATEDIFF function to find the difference in days with the artist_date_created field and the year 2018 because the dataset only has data up to and including 2017.

Podington Bear has been on the site the longest, at 2814 days, which may be a good indicator why they have the most listens and interest. Kevin Macleod, Chris Zabriskie and Jahzzar have been on the site less time but have similar most listens and interest counts to Podington Bear. Kai Engel has only been on the site for 1600 days at this point but still ranks quite high for listens and interest so they should be noted as a quite popular. 


What is the most popular album on the Free Music Archive?

The FMA categorizes album type into five categories:
-	Album
-	Radio Program
-	Live Performance
-	Single Tracks
-	Contest

Bar - album listens by type 

The above bar chart shows that the category type Album has the most album listens which is a good indicator that this is a popular category.

I want to know what is the most popular album on FMA. For my analysis I measured each albums popularity on the FMA by comparing the album listens count.

Bar - album listens w/ distinct count of artist on album

The above bar chart shows the albums with the largest amount of listens. The chart shows us that the album called Entries has the largest amount of album listens, by far, with a count 495,429,777. microSong Entries album is the next most listened to album with 100,934,450 listens followed by Bonus Beat Blast 2011 with 58,985,533 listens. 

It should be noted that the Entries and microSong Entries are contest albums where artists submit tracks that get compiled into an album. These contest albums are promoted on the FMA thus drawing a lot of attention interest which may drive the album listens count. Entries features 108 artists with 139 tracks and microSong Entries features 115 artists with 310 tracks. The fact that these contest albums are promoted on FMA and the number of artists and tracks on these two albums are quite large are a good indicator as to why the album listen counts are large. The Bonus Beat Blast 2011 album features 31 artists with 73 tracks and may possibly be the most popular album that doesn’t have over 100 artists and is not part of any FMA promotions or contests.

Expanding on my analysis of what is the most popular album on FMA, I looked at albums released by individual artists rather that aren’t contest albums. For my analysis I measured each albums popularity on the FMA by comparing the album listens count for each artist.

Stacked - album listen by artist

The above bar chart shows that Podington Bear is ranked the highest because they have 40 albums with 6,356,117 album track listens. If we’re looking at individual albums, we can clearly see that the Nameless: Hacker RPG Soundtrack by BoxCat Games is a very popular album with 1,533,769 listens; it should be noted that the album is a soundtrack by independent video game developer BoxCat Games, but it is impressive to that many listens. Chris Zabriskie has the most popular album, by an individual artist, called Cylinders with 1,363,291 listens.


What is the most popular song on the Free Music Archive?

I want to know what is the most popular song on the Free Music Archive. For my analysis I measured a song’s popularity on the FMA by comparing track listens and interest counts.

Stacked - track listens for each artist

The above bar dot chart shows the songs with the largest amount of track listens. The chart shows us that Happy Birthday is the most popular song but it should be noted that 23 different artists have this same song title with most of Happy Birthday tracks being featured on the Entries contest album. The most popular song, measured by track listens, is Night Owl by Broke For Free with 543,242 track listens.

Stacked - track interest for each artist

The above bar dot chart shows the songs with the largest amount of interest. The chart shows us that the most popular song, measured by interest, is Night Owl by Broke For Free with 3,293,557 track interests. 

Overall, the most popular song on the FMA by an individual artist is Night Owl by Broke For Free with the largest number of listens and interest.


Is there a correlation between listens and interest?

I want to know if there is a correlation between listens and interest on the Free Music Archive. For my analysis I measured the correlation between FMA artist’s track listens and track interest counts. It should be noted that for this analysis normalizing the data didn’t alter the results.


Scatter – artist listens vs interest

The above scatter plot shows the correlation between track listens and track interest for each artist. The plot shows us that there is a strong correlation between listens and interest for artists that have under 1 million track listens and interest counts. As the counts gets larger most artists exist around the trend line. The most popular artists sit above the trend line with larger track listen counts but still correlated with track interest. Overall, there is a correlation between listens and interest for the majority of artists on the FMA because as track listen counts increase so does the track interest count.

I want to know if there is a correlation between listens and interest between songs for the popular artists on the Free Music Archive. For my analysis I measured the correlation between FMA artist’s track listens and track interest counts for each song.

Scatter – Podington Bear listens vs interest
Scatter – Chris Zabriskie listens vs interest
Scatter – Jahzzar listens vs interest
Scatter – Kevin Macleod listens vs interest

The above scatter plots shows the correlation between track listens and track interest for Podington Bear, Chris Zabriskie, Jahzzar and Kevin Macleod. It is interesting to see that there is a strong correlation between listens and interest for Chris Zabriskie songs with an even distribution along the trend line.
 

Where are the most popular FMA artists located around the world?

I want to know where the most popular artists on the Free Music Archive are located around the world. For my analysis I used latitude and longitude coordinates to position all the artists on a map. I used a size label to represent track listens and differentiate the popular artists. 

Symbol Map – artist locations, symbol sizes by track listens

The above symbol map show that most of the FMA artists are located in the U.S.A. and Western Europe.


## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/charlesrroberts/Free-Music-Archive-Analysis-/edit/main/docs/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/charlesrroberts/Free-Music-Archive-Analysis-/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.

