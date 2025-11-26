# British Airways Review – Tableau Dashboard


![British Airways Review Dashboard](https://github.com/maryamsh62/Tableau-Portfolio-Project---British-Airways-Review/blob/master/British%20Airways%20Review%20Dashboard.png)

[TableauPublic](https://public.tableau.com/app/profile/maryamsadat.shakeri/viz/BritishAirwaysReview_17616194116050/Dashboard1)

## Project Overview

This Tableau project analyzes British Airways customer reviews to show how satisfaction differs by route, aircraft type, traveler segment, and region. The interactive dashboard lets users switch between rating metrics—such as overall rating, seat comfort, and cabin staff service—and drill down into specific countries and aircraft to uncover detailed performance patterns.

**The goal of this project is to:**

- Visualize customer satisfaction trends over time
- Compare service quality across aircraft types and routes
- Identify high- and low-performing regions/countries
- Provide a reusable Tableau template for parameter-driven KPI exploration

## Project Files

- `British Airways Review.twbx`: Packaged Tableau workbook containing the full interactive dashboard and data model.
- `ba_reviews.csv`: Main review dataset with 1,324 rows and 19 columns of British Airways customer reviews (2016–2023). 
- `Countries.csv`: The country mapping table is used to enrich each review with continent and region information.
- `British Airways Dashboard.png`: The picture of the Tableau Visualization Dashboard


## 🧱 Data Model & Relationships

**The dashboard uses two tables connected via a relationship in Tableau:**
- Left table: ba_reviews
- Join key: place (reviewer’s country)
- Right table: Countries
- Join key: Country

**Relationship:**
`ba_reviews[place] ⟷ Countries[Country]`

This enables the use of continent and region as filters and for building a filled map. For mapping, the place field is converted to a Geographic Role → Country/Region in Tableau. 


## 🧮 Key Tableau Features & Calculations

**1. KPI Parameter: “Choose a Metric”**

   To make the dashboard flexible, a string parameter called "Choose a Metric" is created. It allows the user to toggle which rating metric is shown in the visuals.

   Parameter settings:
       1. Name: Choose a Metric
       2. Data type: String
       3. Allowable values: List
       4. List of values:
         - Overall Rating
         - Cabin Staff Service
         - Entertainment
         - Food
         - Ground Service
         - Seat Comfort
         - Value (Value stands for “Value for Money”)

**2. Calculated Field: Metric Selected**

   A calculated field is created to map the parameter choice to the correct numeric field:  

   CASE [Choose a Metric]
    WHEN 'Overall Rating'        THEN [Rating]
    WHEN 'Cabin Staff Service'   THEN [Cabin Staff Service]
    WHEN 'Entertainment'         THEN [Entertainment]
    WHEN 'Food'                  THEN [Food Beverages]
    WHEN 'Ground Service'        THEN [Ground Service]
    WHEN 'Seat Comfort'          THEN [Seat Comfort]
    WHEN 'Value'                 THEN [Value For Money]
END

   This "Metric Selected" field is then used in charts (e.g., as AVG([Metric Selected])) so that all main visuals update automatically when the user changes the metric parameter.


 **3. Aircraft Grouping**

   For the aircraft filter, only aircraft with at least 50 reviews are shown individually. All aircraft types with fewer than 50 reviews are grouped into a single category called "Various". This keeps the visualizations readable while still preserving the long tail of less-frequent aircraft.
    

## Dashboard Overview
 
The dashboard is designed to be fully interactive:

- **Metric selector:**

  - Parameter control to switch between: Average Overall Rating, Cabin Staff Service, Entertainment, Food & Beverages, Ground Service, Seat Comfort, Value for Money 


- **Geographic exploration:**

  - Map view by Country, with additional filters for Continent and Region (from Countries.csv)
  - Ability to click on a country on the map to filter all other charts
 
 
- **Dynamic filters:**

  - Each visual is configured as a dynamic filter, so clicking on a bar, map area, or mark filters the entire dashboard to that selection (e.g., click a specific country or aircraft type to see its detailed metrics).



## Results

 The dashboard shows that British Airways’ customer satisfaction is **generally low to middling** over the 2016–2023 period:
- The overall average rating is 4.2, while sub-scores are modest: Cabin Staff Service 3.3, Ground Service 3.0, Seat Comfort 2.9, Value for Money 2.8, Food & Beverages 2.4, and Entertainment only 1.4. Entertainment and food clearly stand out as the weakest parts of the experience.

- The monthly trend in overall ratings is unstable. From 2016 to 2019, scores hover around mid-range levels. Still, from 2020 onward, there are several sharp declines and more months with ratings below 4, indicating increasing inconsistency and a gradual downward shift in customer satisfaction.

- Customer satisfaction varies by country, with some markets showing noticeably lower average ratings (darker shaded regions on the map), indicating that the perceived quality of service is not uniform across the network.

- By aircraft type, Boeing 747-400 has the highest average rating (4.7), followed by Boeing 747, 787, and 777 (≈4.4), and A320 (4.3). At the lower end, the A321 scores 3.6, and the A319/777-200 around 3.8. The “Various” group attracts the highest number of reviews but only a moderate rating (4.1), highlighting that not all fleets deliver the same level of satisfaction.


## Conclusion
British Airways delivers an uneven customer experience: while cabin crews perform relatively well, passengers are consistently dissatisfied with in-flight entertainment, food quality, seat comfort, and value for money. Since 2020, ratings have become more volatile and often lower, suggesting possible impacts from post-pandemic operations or cost-cutting measures. Wide-body aircraft such as the 747-400, 787, and 777 are associated with higher satisfaction than narrow-body types like the A319 and A321, and ratings also vary by country. Together, these patterns point to clear priorities for improvement: enhancing soft products, improving comfort on weaker aircraft, and targeting service upgrades in persistently low-scoring markets to raise overall customer satisfaction.

