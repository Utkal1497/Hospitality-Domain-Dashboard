# Hospitality Domain Dashboard


## Problem Statement

A multi-national company owns multiple five-star hotels across India. They have been in the hospitality industry for the past 20 years. Due to strategic moves from other competitors and ineffective management decision-making, the company is losing its market share and revenue in the luxury/business hotels category. As a strategic move, the managing director of AtliQ Grands wanted to incorporate “Business and Data Intelligence” to regain their market share and revenue.


- #### Objective:

  The objective of this case study is to develop a data-driven strategy that:

        - Show the property details and take a decision based on that.

        - Analyzes different trends and gives ideas for growth in revenue and bookings.

## Demo of the dashboard:

### Level 1: 
Slicers are given using which we can filter the visuals based on

	- Plant ID
	- Market Segment
	- Division
	- City
	- State/Province
	- Priority level of sites based on immediate to long-term investments in five waves.

### Level 2: 
Card visual, Bar Chart, column chart, gauge chart and line chart are used along with tooltip and drill through features.

##### 3 card visuals shows

	-Total number of plants/sites
	-Plants without SAS(Safety Assessment Score)
	-Average of SAS(Safety Assessment Score)
	-The bar chart shows segment wise retention rate which further connected with tooltips showing the total number of lost days due to injury
	-Gauge chart shows the average retention rate
	-Column chart shows the number of plants based on priority
	-Line chart shows turnover rate based on market segment

### Level 3: 
The Table visual is used to show the detailed data which can be filtered based on the slicers.

## Preparation of dataset:

- The transformation and data cleaning is done in Power Query and then the data is loaded.
- One calculated column is created based on the below conditions (assumptions) to decide the priority of the sites/plants.

        -Retention Rate < 0.5
	    -Severity Rate > 2.5
	    -Lost Days due to Injuries > 2
	    -Active Employees < 60

- Based on that the dataset is categorized into 5 priorities where P1 is the highest and P5 is the lowest priority site.

  for creating a new column following the DAX expression was written;

    Priority =  IF('Plant Details'[Retention Rate ]<0.5,
			        IF('Plant Details'[Severity Rate]>2.5,
				        IF('Plant Details'[Lost Days due to Injuries]>2,
					        IF('Plant Details'[Active Employees]<60,"P1","P2"),
				        "P3"),
			        "P4"),
		        "P5")

- Snap of the new calculated column,

  ![Snap_1](https://github.com/user-attachments/assets/0211662d-a90f-44af-9817-c3b141e3fe09)

- Multiple measures are created like Average retention rate, Average safety assessment score, etc.

        Avg Retention Rate = AVERAGE('Plant Details'[Retention Rate ])+0

        Avg Safety Assessment Score = AVERAGE('Plant Details'[Safety Assessment Score])+0

        Safety Assessment Score NA = COUNTBLANK('Plant Details'[Safety Assessment Score])+0

- One date table is added to show the last refresh timing of the report.

## Report Snapshot (Power BI Desktop)
 
  ![Snap_Percentage](https://github.com/user-attachments/assets/e6f7f7fc-0e0d-45c8-b951-32b23f13031d)


- Snap of slicers used, through which the user can filter the report.

   ![Snap_Percentage](https://github.com/user-attachments/assets/63fa1042-5265-4db0-b7c1-d5581bced91f)


- Card visuals were used to represent the Total number of Plants, Plants without Safety Assessment Scores, and Average Safety Assessment Scores.

  ![Snap_Count](https://github.com/user-attachments/assets/2a7db2bf-509f-4cf5-adbe-4c08857a1e26)

 
- A gauge chart was used to represent the Average retention rate.

  ![Snap_Count](https://github.com/user-attachments/assets/ccd7dbb0-d808-4a7f-9857-7a9bbf8003cd) 


- A bar chart was used to represent the Retention rate by Market Segment. Tooltip is used to show Total lost days due to Injuries. By hovering over the data bars it will show the related field data.               

  ![Snap_Count](https://github.com/user-attachments/assets/0aed8645-9955-4e31-a471-f6089672dd97) 


- A Column chart was used to represent the Number of Plants by Priority. The drill-through feature is used to further dig into the data. Drill-through option is visible by right-clicking on the graph.

  ![Snap_Count](https://github.com/user-attachments/assets/1f94456b-0941-4b19-be6e-9ab7d8e72094) 


- A Line chart was used to represent the Turnover rate by Market Segment.

  ![Snap_Count](https://github.com/user-attachments/assets/63646547-5d86-45d5-8291-27c769f96d60)


- A Table chart was used to represent detailed data based on the Plants.

  ![Snap_Count](https://github.com/user-attachments/assets/7c88ac52-5e15-490a-9aaa-b50a6f1a65f1)


## Analysis and Result:

By analyzing the data it was found that we have to take the following steps:

	- First, we have to calculate the plants' safety assessment score, which is not done yet.
	- From the report we found that 16 plants need immediate action on high priority (P1) then P2, P3, P4, and P5.
	- We have to get more manpower in the plants that fall in category P1.
	- In the retention rate graph we can check the market segments ranked at the bottom and invest in them.
