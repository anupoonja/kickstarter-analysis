# Kickstarting with Excel

## Overview of Project

### Purpose
This kickstarter project was to analyze:
* The outcome of the theater campaign based on the launch date; and
* The outcome of the plays sub-category under the theater campaign based on the funding goals.

The main purpose of the project was to explore the excel tool, which I learnt is very vast and powerful, and to apply the skills that was learnt in this project. 

## Analysis and Challenges

### Analysis of Outcomes Based on Launch Date

This analysis was about understanding the outcome of the campaign based on the launch date.
The information needed to analyse were the date of creation, outcome and the parent category.

We had already created a column to convert the "launched_at" in Unix timestamp, to "Date Created Conversion" in Date format using the conversion method :
```
(((J2/60)/60)/24)+DATE(1970,1,1)
```
We had to then extract the year information, by creating a new column for "Years" and using the formula: 
```
YEARS() : =YEARS(S2)
```

The Pivot Table is then generated to be filtered based on "Parent Category" and "Years".
The "Date Created Conversion" will be selected in the row and the "Outcomes" will be selected in the column section.

The Pivot Table looked like this without any filtering:

![Unfiltered Pivot Table](https://github.com/anupoonja/kickstarter-analysis/blob/master/extra_resource/Pivot_Table_Launch_Date.png)

Had to fiddle around to see how to group/ungroup to be able to view the column in the date/time format.

Final filtered Pivot Table looked like this:

![Filtered Pivot Table](https://github.com/anupoonja/kickstarter-analysis/blob/master/extra_resource/Filtered_Pivot_Table_Launch_Date.png)


For the final filtered Pivot Table to look like above had to make the below changes:
 - group the column based on months
 - sort the outcome column in descending order
 - deselect the live and (blank) option in the outcome column
 - Filter the “Parent Category” to show the data for "theater"

Created the line chart from the pivot table to visualize how the "outcome" changed with the launch date, years and months.

The below options had to be selected for the chart to look similar:
* Select the chart "Line with Markers"
* Remove the button for filter fields for "Parent Category" and "Years"
* Remove the buttons on chart for outcomes
* Change the color of the lines for each of the outcome
* The chart title should be added as "Theater Outcomes Based on Launch Date"

The snapshot of the line chart **Theater Outcomes vs Launch Date** based on the filtered Pivot Table can be found below:

![Theater Outcomes vs Launch Date](https://github.com/anupoonja/kickstarter-analysis/blob/master/resources/Theater_Outcomes_vs_Launch.png)


### Analysis of Outcomes Based on Goals

This analysis was to visualize the percentage of successful, failed and canceled plays based on the funding goal amount using the powerful visualization tool - excel.

To analyze we needed to create a new page "Outcomes Based on Goals" and include columns to hold the data needed:
 * Goal
 * Number Successful
 * Number Failed
 * Number Canceled
 * Total Projects
 * Percentage Successful
 * Percentage Failed
 * Percentage Canceled

The 'Goal' column was created with the dollar amount range to group the project based on the goal amount.

![Goal](https://github.com/anupoonja/kickstarter-analysis/blob/master/extra_resource/Goal%20Range.png)

**1.** To fill the columns "Number Successful", "Number Failed" and "Number Cancelled", we have to use the excel function 
```
COUNTIFS()
```

The data is filled with criteria range and the criteria. There can be any number of criteria range and criteria. There is no limit on the number of criteria to be filled.
The data have to be filled by extracting the information from the "Kickstarter" sheet.

The different criteria are:
 * Goal amount: that is extracted from the "Kickstart" sheet in the column D
 * The range like "<1000", "<=2999", ">=3500" or ">=50000" depending upon the value in the "Goal" column.
 * The outcomes are selected from the "Kickstarter" sheet in the column F
 * The outcome is selected for the subcategory "plays", by using the information in the "Sub-category" column R.
 * The formula used to fill the "Number Successful" column is below:
   ```
   =COUNTIFS(Kickstarter!$D:$D,"<1000",Kickstarter!$F:$F,"successful",Kickstarter!$R:$R,"plays")
   ```
 * The formula used to fill the "Number Failed" for range 1000 to 4900 will be
  ```
  =COUNTIFS(Kickstarter!$D:$D,">=1000",Kickstarter!$F:$F,"failed",Kickstarter!$R:$R,"plays",Kickstarter!$D:$D,"<=4999")
  ```
 * Every cell has to be manually edited.

**2.** Next we have to fill the column "Total Projects" using the function and copy them to the column using double click :
  ```
  SUM() : =SUM(B2,C2,D2)
  ```

**3.** To fill the column "Percentage Successful" we have to get the percentage of successful outcomes out of the total
 * Use the formula ```=B2/E2```
 * Copy the formula for the entire row by double clicking
 * Change the column type from "General" to "Percentage"

**4.** Repeat the same process for "Percentage Failed" and "Percentage Canceled" by using the columns "Number Failed" and "Number Canceled"

The snapshot of the Pivot Table with the data populated using the functions can be found below:

![Pivot Table for Outcome Based on Goals](https://github.com/anupoonja/kickstarter-analysis/blob/master/extra_resource/Goal%20Table.png)

We have to create a line chart to visualize the relationship between the goal amount ranges and the percentage of successful, failed and canceled.
* The line chart has to be plotted by selecting the columns "Goal", "Percentage Successful", "Percentage Failed" and "Percentage Canceled"
* The title should read "Outcomes Based on Goal"
* The chart should be wide enough for all the fields in the x-axis to be clearly visible

The snapshot of the line chart **Outcomes vs Goals** based on the filtered Pivot Table is attached below:
![Outcomes vs Goals](https://github.com/anupoonja/kickstarter-analysis/blob/master/resources/Outcomes_vs_Goals.png)

### Challenges and Difficulties Encountered

* In this exercise learnt how to use the function YEARS(), COUNTIFS(), SUM() and lookups from different sheet.
* Creating the pivot table with the filter option, rows, columns and values were straight forward. However, it was challenging to figure out how to display date in the row column and how to group/ungroup. After fiddling a bit figured out and was able to group based on the month.
* Creating the line chart was straight forward. Had to fiddle around to change the color of the lines and remove the buttons from the chart.
* Manually inserting all the values in the Number Successful/Failed/Canceled field was changeling and rewarding.
* Getting the percentage formula right was a challenge and then figured out we could just change the type to "Percentage" and use (B2/E2) instead of multiplying (B2/E2) by 100
* Didn’t have any issues while creating the second line chart for "Outcomes vs Goals".

## Results

- What are two conclusions you can draw about the Outcomes based on Launch Date?
  Based on the line chart that was plotted we can conclude that:
  * The plays that got launched in *May* has higher success rate.
  * The success rate picked up in the first half of the year and slowly dropped in the second half of the year.

  The line chart for the overall "Parent Category" looked pretty much the same with high success rate in *May* and lowest in *December*.

- What can you conclude about the Outcomes based on Goals?

   We can conclude that the percentage of success dropped down as the Goal amount increased. Only exception being in the range of 35000 to 45000.

- What are some limitations of this dataset?

  Making conclusions based on the data of one category might not necessarily give the full picture of the overall campaign. Though 'theater' has highest campaigns, it is still only ~34% and 'plays' is only ~26% of the total campaign.

- What are some other possible tables and/or graphs that we could create?

  * We can derive conclusion based on the number of backers for each range of goal amount to approximate the ideal goal.
  * We could derive conclusion based on the launch date and the number of backers to derive the trend in month when people would pledge for campaigns. This could help determine the ideal start date and the deadline.
  * For the canceled project we could plot the percentage that was funded and determine the ideal budget for the campaign to be successful.

