# Final-Project-Tableau

## Project/Goals
### Data File Chosen: FAA Wildlife Strikes, 2015
This is a cleaned table of wildlife strikes from 2000-2015 in the United States. 

Using the dataset, the goal is to find a relationship between time, species, location, number of strikes, cost, damage, and trends.
Determine if there are any outliers.
There are also several questions to be answered.
How many animals are struck by planes annually?
When and where are they struck?
Which species are most vulnerable and where?
What is the damage of the strikes?
What is the cost associated?

## Process and Results
The data was reviewed and datasets were looked at.  
The initial query was to try and find a relationship between time and number of strikes.  
First the time of day and frequency of strikes was isolated in a dashboard.
It was found that most of the collisions take place during the day at 8:00 am. This is correlated with airport peak time around 6:00 am in the U.S.
The states with the most strikes are the most populus ones with highest air traffic.

Next the category of animal and number of strikes per month was looked at.
It was found that the most struck category of animal by airplane are birds and that the amount of animals struck increases between migration periods.
There is also a yearly increase in the amount of animals struck.  The most pronounced increase is between 2008 and 2009.

Further analysis of the graph showed that on top of migration, the increase in strikes against all animals can be due to a higher frequency of flights,
(as indicated by the most populus states), and an increase in the amount of animals present.  
Both factors increase during the summer.

A relationship between stage of flight and animals struck found that the highest struck species was the Eared Grebe at 20,000 feet during the climb phase.
The max height of all categories for each stage was for birds.
The chart also showed that the average height is skewed lower for birds because most strikes take place on ground level.
Because there are a higher frequency of birds struck at a low level, bats have a higher average height.
There were too many variables shown at once which oversaturated the figure.  This is explained more in the challenges section.

A plot of the number of animals struck vs year showed that the number of projected animals struck followed an exponential increase.
After answering how many animals are struck by time and where, the next question was which species are most vulnerable?

Several calculated fields were created:
- Cost per Amount of Damage: ```{ FIXED [Effect: Amount of damage (detailed)] : SUM([Cost: Total $]) }```.  Used to aggregate total cost for the category "Effect: Amount of damage (detailed)".
- Number of Strikes per Year: ```{ FIXED DATETRUNC('year', [Collision Date and Time]) : SUM([Number of Strikes])}```.  Used to aggregate the total amount of strikes recorded per year.
- Fixed Animals Hit: ```{ FIXED [Number of Strikes]: COUNT([Number of Strikes]) }```.  Used to record the total number of strikes to show in multiple categories.
- Percent animals hit: ```COUNT([FAA Wildlife Strikes])/SUM([Fixed Animals Hit])```.  Uses "Fixed Animals Hit" to find the percent of total for different categories.
These Calculated fields were used to clarify information in the story and dashboards in case the cursor was hovering over a datapoint,
or a filter was used to shorten excessively long lists.  

The number of strikes per the Top x Species, (Top x Species being a filter), was plotted in a dashboard.
Out of the top 5 species most struck, the highest number was for Mourning dove in Texas.  
The second most common were Gulls in more populus coastal regions, such as New York and California.
The Barn Swallow is most struck in Florida.
European Starling most struck in Pennsylvania.
Horned Lark most struck in Colerado.

After damage to wildlife, what's the damage and cost to flights?
Isolating for damage, impact on flight, and number of species struck found that around 
83% of hits cause no damage and no impact to flight.

A plot compared the effect strikes had against category of animal, which also listed the average and total cost.
It was found that the average cost of having the vehicle destroyed is greater than substantial and other types of damage.
It's also found that terrestrial mammals have a higher cost compared to birds.
However substantial damage and birds being struck are more frequent than destroyed and terrestrial mammals, so this causes a greater total cost.

After answering the damage and cost associated, another question to look into are which species are associated with the greatest cost?
A dashboard plotting the total cost per species and assiciated state showed that out of the Top x Species,
the most costly mammals are deer with $30,963,668, mostly occuring in Alabama.
The most costly birds are Geese with $103,792,693.

Geese was a big outlier in New York which warrented further investigation.
Plotting each data point against indiviual cost found that the outlying datapoint had:
Wildlife: Canada goose        
Airport: LA GUARDIA ARPT
Effect: Destroyed
Date: Jan. 15, 2009        
Cost: $41,071,585
The most costly collision in the dataset was discovered to be the historic event when captain Sully Sullenberger made an emergency landing in the Hudson River.

A final plot was constructed to look at the average total cost per year and relook at the number of strikes per month.
A trendline for the average cost showed a linear decrease the total cost built up each year, (other than a few costly outliers).
This was compared to the exponential trendline shown in the number of strikes per month plot.
What the trendline shows is that while the number of animals struck each year is increasing exponentially,
the average cost in comparison is linearly decreasing.  
So the total cost per species hit is actually becoming more cost effective.

### Files Saved
All the worksheets used are saved to "Rough Worksheets Filtered in Inderactive Story and Dashboards.pdf".
It should be noted that these are not the final results of what was presented.
The worksheets were used to clarify information in the story and dashboards in case the cursor was hovering over a datapoint,
or filters were used to shorten excessively long lists.

Dashboards used in the story were saved in the file "Dashboards.pdf".

The Tableau file was saved to "LHL-Tableau-Project.twbx".

The story and presentation is in the file "TableauPresentation_Option2_faa_data_subset_Frood_Michael.pdf",
but the interactive story is also available in the "LHL-Tableau-Project.twbx" file.

## Challenges 
Some of the challenges faced was trying to find a pattern between locations, time, and animals/species.
A lot of the problems came from trying to tie together several variables at once and to make the graph more palatable.
NOTE: Some of the graphs included, (such as "Ave Feet Above Ground vs Flight Stage"), are an example of this challenge.
Some graphs are too oversaturated and harder to read and are included in the storyboard as an example of such.

I could not figure out how to save the file from Tableau public as a .twb file but I did save it as a .twbx file.

## Future Goals
If I had more time I'd look deeper into a multivariable geographic location where animals were struck and try to relate that to cost per location.
One way would be to create a worksheet to isolate information to each airport code, e.g. cost, number of strikes, distance from airport, average height, etc. in a table.
The table would be divided by state.  Then, I would create a map of the states, and place that worksheet information into a tooltip.
One could then get a list of all the state airport information by hovering the cursor it.
