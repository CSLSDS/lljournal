# Build a Team, Build an App

   In the course of the journey through Lambda School's Data Science program, I had the great fortune to build an application with not one, but **three** phenomenal teams; one specific to data science (the one I was a member of) and two great web teams.  
   
   While there were a number of products we could have been tasked with, we were given the opportunity to work with an internal stakeholder in Lambda Labs to create a solution for the problem facing many in our modern age:  **researching cities in order to compare and contrast them against one another when faced with the need to move somewhere new**.  
   
   **The essential concept of the product** is to *enable users, through a simple interface, to **search for**, **choose**, and then **compare** the metrics available for U.S. cities over 30k population*.  The name of this product is _**Citrics**_, which is a [portmanteau](https://en.wikipedia.org/wiki/Portmanteau) of "city" and "metrics". (Though it _does_ sound like a delicious new citrus cultivar 🍊)  
   
   This would be no simple feat; while the concept is straightforward, sourcing consistent and clean data for what was to be a list of _**well over 1,000 cities**_ on a variety of inter- and unrelated metrics would require cooperation and diligence on the part of every member of our data science team, and delivering these in usable format promptly enough to our web teams that they would have sufficient time to build around that data would take all of us working in concert (and no small amount of good luck).  
   
   The first step to tackle to begin to give our roadmap to achievement it's shape and structure was **to break down the vision of the end product into discrete, manageable tasks.  **
   
   ## Trello to the rescue!
   
<img src="https://raw.githubusercontent.com/CSLSDS/lljournal/main/labsblog00.png" width = "600" />  
   We made significant use of a Trello board to organize, track, and communicate our efforts with one another.  
   
   Here, for example, we delineated the key task of gathering our "core" city metrics, derived from whichever suggestions reached sufficient interest from team members to warrant inclusion, such as demographics, cost of living factors, and weather.  
   **We used the checklist feature** to list the attributes we hoped to find viable data sources for, and iteratively added plausible sources to the entries in the checklist as we explored possibilities. 
   This enabled us to take responsibility for individual sources, and communicate who was working on which source at which time, as well as which task was incomplete and needed work.  
   Once the sources were checked and found to be a _viable candidate for our database_, it was checked off the checklist, and this was how we kept track of where we were in the process of gathering our "minimum-viable-product" attributes.   
   
   <img src="https://raw.githubusercontent.com/CSLSDS/lljournal/main/labsblog01.png" width = "600" />  
   
   ### Use of asynchronous organizational communication was absolutely KEY for our team process; 
   ...with many data scientists on the hunt for sources, and two separate web teams, each comprised of folks with different specializations in the stack, we relied heavily on Trello, Slack, GitHub, and multiple Agile-style standups every day through Zoom, both with our respective teams, and as a larger group developing on Citrics.  
   
   ***This workflow enabled us to quickly iterate***, and gave us **tighter feedback loops** to see where we could improve our flows, or pinpoint issues as they came up, ***before*** they became major roadblocks for the project.  
   
   ## The 'meat' of the Data team's contributions  
        
   While the essential *task* was clear, the *method* of arriving at our delivery was open-ended.  We worked together to determine a simple architecture, and to check in with our Web support teams to clarify what their expectations were as we moved through the developent process.  
   We developed iteratively, with the first iteration being a simple, scraped, single-source .csv that the API could import and deliver, to give the web team a starting point from which to begin development. 
   
   As the project unfolded, we came to a conclusion to serve an API endpoint that returns individual city entries by a unique ID number, which would eventually be drawn from a PosgreSQL relational database hosted by the AWS Relational Database Service.  This API was built with FastAPI, Docker, and hosted through AWS Elastic Beanstalk, routed through SSL also provided by AWS Route 53.  
   
   #### We discovered that sourcing some features were more complex than others: 
   - ...while we attempted to leverage several APIs, we found many had paywalls, request limitations on frequency and size, and other unique attributes we had to either account for, or give up on that source as viable.  We learned a lot about polite webcrawling, and functionalizing our requests to ensure reproduceability.  

- We also found that there were many features of cities that were ***required*** for us to be able to merge and collect the appropriate data: numerous sources were not granular at the city level, so we needed to base our merging on the **county**, **zipcode**, **coordinates**, and even zoom out as far as state-level to get the metrics we were seeking.   
- We had also hoped to find historical, time-series data on as many of our features as possible, to enable more robust visualization as well as prepare for potential predictions ini the future.  This added a lot of complexity and legwork to our gathering process, and made formatting the data we serve a much more nebulous task...   

####  ...We found ourselves uncertain about datatypes and expectations of our web team, based on the subtle nuances of difference between JavaScript Object Notation ([JSON](https://en.wikipedia.org/wiki/JSON)) and [Python's dictionaries](https://docs.python.org/3/tutorial/datastructures.html#dictionaries), which we discovered are known more broadly as "associative arrays".  
   - This data structure was "KEY" (pun intended) in formatting our relational information while keeping those relationships explicit, as we served individual "rows" or entries per-city to the web team, with the "keys" being the name of the "column" or feature being appropriately paired with the value for that particular city.  
   
   - These nuances of difference made formatting and reformatting the data a bit tricky, and demanded some particular skills from our team: leveraging the vectorization made possible by the Pandas library, and encoding the results in a way that could be stored in a SQL database as well as served in a format that is legible and useful to the web team. 

   - We used vectorization and the `ast` python library (`ast.literal_eval()` in particular) to enable us to translate multiple datatypes to and from strings as needed, which enabled us to vectorize our operations to the entire dataset, and with the use of comprehensions, include caveats and conditions to those vectorized operations, e.g.  
    
	[<img src="https://raw.githubusercontent.com/CSLSDS/lljournal/main/labsblog02.png"width="600"/> ](https://colab.research.google.com/drive/1i-koHjYmu3Kd0AOQPL9KQTt2ZlBVZBoP#scrollTo=PeKMLjS5n6cR&line=1&uniqifier=1)  

In the end, the backend for web found themselves able to tweak formatting as they saw fit, and our struggle to understand their needs were not pivotal to the success of our project, but we found many useful workarounds and tricks to format and reformat as we found a need, and this brought us all to a more well-rounded position as developers.  
   
   ## The Big Payoff
   <img src="https://raw.githubusercontent.com/CSLSDS/lljournal/main/labsblog03.png"width="400"/>  
   
  As our tenure on this project came to a close, we found ourselves with a generous database, with both current and historical context, robustly delivered to multiple web teams to serve to users as they saw fit.    
  **This means** we have enabled users to **search for and compare hundreds of major U.S. cities** by myriad attributes, ideally serving a broad swath of user-types, regardless of their individual priorities for what makes a city a desireable place to move and live.  
  
  Users can search for any city that had over 30k population as of the 2010 U.S. Census, as well as those that had a population above this threshold by the Census Bureau's estimates for 2019. 
  
  Once a city is chosen, it's core attributes are automatically displayed in comparison to national averages.
  
  Users can then search for a second city for comparison, and it's details will appear along with the previously displayed information for the first city and national average; this can be done for up to three cities to compare against national averages simultaneously.  (There are also additional city stats available in the sidebar containing cities being compared.)  

  ## The Future of Citrics
  Features we have discussed but have not built in to the project are:
  - providing simple predictions about what the cities will look like in the future, based on the gathered historical precedents. 
  - drawing the data gathered from APIs in a way that keeps them updated as new data becomes available (this is especially useful and relevant for high-frequency measurements, such as COVID-19 case statistics, which are updated daily.)
  - creating other endpoints and database tables as is sensible to make visualization and data service simpler and more efficient
  - adding unique and interesting features such as attractions, popular meetup groups, 'walkscores', political trends, and industry-specific information for professionals seeking ideal conditions for career development 
  - incorporating location-based NLP analysis on public data that brings unique insights about cities to our user base
  - researching the implementation of `asyncio` and `asyncpg` for database interaction, as many sources cite it as being up to 3x faster than `psycopg2` (though the performance gains may not be worth the effort, it's a direction that would likely provide some great learning opportunities that may see relevance in our profesisonal lives down the road)   
  
  I suspect that functionalizing regular updates to pipeline the latest statistics into the database would be the most technically challenging of these goals, as it will be a separate process for each feature for which it is developed, though the structure of the API should allow for a high degree of customization for implementing this, at least for some features.  

## Lessons Learned
  Some precious learning and development has come about due to the nature of this effort.  In particular, I cherish the deep appreciation I have built for team members, communication, and the technologies we utilize for asyncronous syncronization of our work that enabled us to build as far as we have.  

