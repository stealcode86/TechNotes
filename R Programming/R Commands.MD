	1) Citation()
	2) Q()
	3) install.packages("tidyverse") -- to install packages ( this needs to be done only once )
	4) library(tidyverse)  -- to load the package ( to be done always )
	5) Library(lubridate)
	6) Alt + Shift + K - keyboard shortcuts cheat sheet 
	7) ggplot(data=penguins,aes(x=flipper_length_mm, y=body_mass_g))+geom_point(aes(color=species))
	8) ?print() --- this syntax gives definition of a function and helps us learn more about the function 
	9) First_variable <-" This is mny variable" ( variable name, assignment operator, value )
	10) vec_jers <-c(20,85, 181.5, 2002) # Define vector ....... > vec_jers    … # Dsiplay vector 
	11) head(diamonds) -- to display first few columns and rows
	12) `str()` and `glimpse()` functions will both return summaries of each column in your data arranged horizontally.
	13) `colnames()` function. It returns a list of column names from your dataset.
	14) For example, you might need to rename the columns, or variables, in your data. There is a function for that: `rename().`      rename(diamonds, carat_new = carat)   ----- ( dataset name, new col name = col name )
	rename(diamonds, carat_new = carat, cut_new = cut) -- to replace 2 column names 
	15) `summarize().` You can use it to generate a wide range of summary statistics for your data. For example, if you wanted to know what the mean for `carat` was in this dataset,  summarize(diamonds, mean_carat = mean(carat))
	16) ggplot(data = diamonds, aes(x = carat, y = price)) + geom_point()………….. The code above takes the `diamonds` data, plots the carat column on the X-axis, the price column on the Y-axis, and represents the data as a scatter plot using the `geom_point()` command. 
	17) ggplot(data = diamonds, aes(x = carat, y = price, color = cut)) + geom_point()…………….. if you wanted to change the color of each point so that it represented another variable, such as the cut of the diamond
	18) Sometimes when you are trying to represent many different aspects of your data in a visual, it can help to separate out some of the components. For example, you could create a different plot for each type of cut. `ggplot2` makes it easy to do this with the `facet_wrap()` function …. 
	ggplot(data = diamonds, aes(x = carat, y = price, color = cut)) + geom_point() + facet_wrap(~cut)
	19) Installed.packages() --- to check the packages that have been installed 
	20) Update.packages() will update all of your packages
	21) browseVignettes(“ggplot2”) --  To check out vignettes for one specific package, type browseVignettes(“packagename”) and press Enter
	22) Ctrl + Shift + M - shorcut for pipe symbol
	23) Head(diamonds) - gives a quick preview of just first 6 rows of a table
	24) penguins %>% arrange(bill_length_mm) -- arrange in asc order of bill length…..  penguins %>% arrange(-bill_length_mm) -- arrange in descending order of bill length 
	25) penguins %>% group_by(species, island) %>% drop_na() %>% summarize(max_bl = max(bill_length_mm), mean_bl = mean(bill_length_mm)) -- grouping by and dropping values having NA and summarizing by mean and max of the grouped by criteria
	26) example_df <- bookings_df %>%
	  select(arrival_date_year, arrival_date_month) %>% 
	  unite(arrival_month_year, c("arrival_date_month", "arrival_date_year"), sep = " ")  --- selecting the columns and uniting the columns into one column and saving it to a DF
	27) separate(employee,name,into = c("first_name","last_name"),sep =' ' ) ---- separate name column from employee data into f and l name cols and sep in the blank space
	28) unite(employee, 'name',first_name, last_name, sep=' ') ---- uniting f and l name into name col. and sep by blank space from employee data
	29) penguins %>% 
	30) mean(hotel_bookings$lead_time) --- mean of lead time column in hotel booking DF
	31) ggplot(data=penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g, shape=species, color=species))
	32) ggplot(data=penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,alpha=species))
	33) ggplot(data=penguins) + geom_smooth(mapping=aes(x=flipper_length_mm,y=body_mass_g))    ---- smooth line 
	34) ggplot(data=penguins) + geom_smooth(mapping=aes(x=flipper_length_mm,y=body_mass_g, linetype=species))
	35) ggplot(data=penguins) + geom_jitter(mapping = aes(x=flipper_length_mm,y=body_mass_g))
	36) ggplot(data=diamonds) + geom_bar(mapping = aes(x=cut,color=cut))   -- bar graph and shows count on y axis 
	ggplot(data=diamonds) + geom_bar(mapping = aes(x=cut,fill=cut))
	ggplot(data=diamonds) + geom_bar(mapping = aes(x=cut,fill=clarity)) (note: if you don't specify a variable for the y-axis, the code defaults to 'count')
	
	37) ggplot(data=penguins, aes(x=flipper_length_mm,y=body_mass_g)) + geom_point(aes(color=species)) + 
	  facet_wrap(~species)    -- 3 different graphs representing each of the species  ( facet_wrap did this )
	
	38) ggplot(data=diamonds) + geom_bar(mapping = aes(x=color,fill=cut)) + facet_wrap(~cut)
	
	39) ggplot(data=penguins) + geom_point(mapping = aes(x=flipper_length_mm,y=body_mass_g,color=species)) +
	  facet_wrap(sex~species)   --- gives sex and species plotted in various graphs
	40) ggplot(data = hotel_bookings) +
	  geom_bar(mapping = aes(x = distribution_channel, fill= deposit_type ))   ---- bar graph with deposit types filling the bars in different colors 
	41) ggplot(data = hotel_bookings) +
	  geom_bar(mapping = aes(x = distribution_channel)) +
	  facet_wrap(~deposit_type) +
	  theme(axis.text.x = element_text(angle = 45))  -- labels are rotated 45 degrees
	42) ggplot(data=penguins) + geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g, color = species))
	
	ggsave("Three Penguin Species.png")  -- saves the file  …………..The `ggsave()` function in the code chunk below will save the last plot that was generated, so if you ran something after running the code chunk above, run that code chunk again. 
	
	43) install.packages(“vitae”)   — This will give us CV templates which we can build a Resume on.
	
	
	
	



	Clean	                    Organize	    Transform
	Rename_with()	            Group_by()	  Separate()
	Select()	                Drop_na()	    Unite()
	Skim_without_charts()	    Mean()	      Mutate()
	Clean_names()	            Arrange()	
	Glimpse()	                Summarize()	
	Rename()	                Filter()	
		                        Max()	

	
Notes
	1) R is  case sensitive
![image](https://user-images.githubusercontent.com/49140843/172023618-1b875e61-f784-4873-b140-4de833b4fc15.png)
