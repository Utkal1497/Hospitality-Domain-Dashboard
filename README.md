# Hospitality Domain Dashboard


## Problem Statement

A multi-national company owns multiple five-star hotels across India. They have been in the hospitality industry for the past 20 years. Due to strategic moves from other competitors and ineffective management decision-making, the company is losing its market share and revenue in the luxury/business hotels category. As a strategic move, the managing director of AtliQ Grands wanted to incorporate “Business and Data Intelligence” to regain their market share and revenue.


- #### Objective:

  The objective of this case study is to develop a data-driven strategy that:

        - Show the property details and take a decision based on that.

        - Analyzes different trends and gives ideas for growth in revenue and bookings.

## Demo of the dashboard:

### Level 1: 
Slicers and date filters are given using which we can filter the visuals based on

	- City
	- Room Class
	- Category
	- week
	- year month

### Level 2: 
Card visuals, column charts, pie charts, and line charts are used to show detailed trends.

##### 6 card visuals shows

	-Revenue
	-RevPAR
	-DSRN
	-Occupancy %
	-ADR
	-Realisation %
 
 ##### Column chart shows

 	-Realisation % vs ADR by booking platform

  ##### Pie chart shows

  	-Revenue by category

   ##### Line chart shows

   	-Trend comparison of RevPAR, ADR, and Occupancy % for every week.

### Level 3: 
The Table visual is used to show individual property details. Another table visual shows numeric details based on weekdays and weekends. These visuals filter out based on the slicers.

## Preparation of dataset:

- The transformation and data cleaning is done in Power Query and then the data is loaded.
- Multiple key measures are created.

  	-ADR = DIVIDE([Revenue],[Total Booking],0)
  		-Avg rating = AVERAGE(fact_bookings[ratings_given])
  		-Booking % by Platform = DIVIDE([Total Booking],CALCULATE([Total Booking],ALL(fact_bookings[booking_platform])))
  		-Booking % by Room class = DIVIDE([Total Booking],CALCULATE([Total Booking],ALL(dim_rooms[room_class])))
  		-Cancellation % = DIVIDE([Total cancelled bookings],[Total Booking])
  		-DBRN = DIVIDE([Total Booking],[No of Days])
  		-DSRN = DIVIDE([Total Capacity],[No of Days])
  		-DURN = DIVIDE([Total Checked out],[No of Days])
  		-No of Days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY)+1
  		-No Show % = DIVIDE([Total No show],[Total Booking])
  		-Occupancy % = DIVIDE([Total Successful bookings],[Total Capacity],0)
  		-Realisation % = 1-([Cancellation %]+[No Show %])
  		-Revenue = SUM(fact_bookings[revenue_realized])
  		-RevPAR = DIVIDE([Revenue],[Total Capacity])
  		-Revpar WoW change % = 
			Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
			var revcw = CALCULATE([RevPAR],dim_date[wn]= selv)
			var revpw =  CALCULATE([RevPAR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))
			
			return
			
			
			DIVIDE(revcw,revpw,0)-1
  		-Total Booking = COUNT(fact_bookings[booking_id])
  		-Total cancelled bookings = CALCULATE([Total Booking],fact_bookings[booking_status]="Cancelled")+0
  		-Total Capacity = SUM(fact_aggregated_bookings[capacity])
  		-Total Checked out = CALCULATE([Total Booking],fact_bookings[booking_status]="Checked out")
  		-Total No show = CALCULATE([Total Booking],fact_bookings[booking_status]="No show")+0
  		-Total Successful bookings = SUM(fact_aggregated_bookings[successful_bookings])


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
