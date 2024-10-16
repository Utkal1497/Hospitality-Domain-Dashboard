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
 
  ![Snap_Percentage](https://github.com/user-attachments/assets/b7cd9452-24ee-42ee-a587-470f17e351fb)


- Snap of slicers used, through which the user can filter the report.

   ![Snap_Percentage](https://github.com/user-attachments/assets/903d019d-0029-43ea-b005-c0e21ebef49d)

- Snap of date filters used, through which the user can filter the report.

   ![Snap_Percentage](https://github.com/user-attachments/assets/9761135c-8667-4ca3-975c-01ea1472f24e)


- Card visuals represented the Revenue, RevPAR, DSRN, Occupancy %, etc.

  ![Snap_Count](https://github.com/user-attachments/assets/915a1108-4bde-4be0-9b09-3fb584fe3465)

 
- A column chart was used to represent the Realisation % vs ADR by booking platform.

  ![Snap_Count](https://github.com/user-attachments/assets/084beabf-a408-4a62-87f0-18d8f013c4c0) 


- A line chart was used to represent the trends by key matrix like RevPAR, ADR, and Occupancy for every week.               

  ![Snap_Count](https://github.com/user-attachments/assets/e75dbd07-f853-4ec6-ab1c-a989f7745f64) 


- A pie chart represents the revenue by room category (Luxury or Business).

  ![Snap_Count](https://github.com/user-attachments/assets/95f65d95-25b8-49c4-88f9-2c4c7811db45) 


- A Table chart was used to represent booking and revenue details based on weekdays and weekends.

  ![Snap_Count](https://github.com/user-attachments/assets/41c7ff49-ed73-4a73-80e5-b8cab601b068)


- Another Table chart was used to represent each property detail which is useful to make decisions based on property.

  ![Snap_Count](https://github.com/user-attachments/assets/9c6b01ce-e0a1-499b-a27f-c224e635f972)



## Analysis and Result:

By analyzing the data it was found that we have to take the following steps:

	- By analyzing the dashboard we can have an idea of demand and supply of rooms and make the prices dynamic accordingly.
	- Different promotions and coupons should be applied on various channels.
	- We can check the property details and occupancy % for each property and make changes to grab more bookings.
	- For each hotel, we can get the idea that it's using flat or dynamic pricing based on weekdays and weekends.
