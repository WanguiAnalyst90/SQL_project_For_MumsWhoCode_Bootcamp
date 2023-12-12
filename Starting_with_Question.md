Answer the following questions and provide the SQL queries used to find the answer.

Question 1: How many total listings are there in the Capetown AirBnB data? Would you say there are inactive listings in the data? If yes, What percentage of total listing is active or inactive?

SQL Queries: 
SELECT COUNT(*) AS total_listings
FROM listings;

SELECT COUNT(*) AS active_listings
FROM listings
WHERE host_total_listings_count >0;

SELECT COUNT(*) AS active_listings
FROM listings
WHERE host_total_listings_count =0;

SELECT(COUNT(*)*100/SELECT COUNT(*) FROM listings)) AS percentage
FROM listings
WHERE host_total_listings_count>0;

SELECT(COUNT(*)*100/SELECT COUNT(*) FROM listings)) AS percentage
FROM listings
WHERE host_total_listings_count=0;

Answer:There are 21120 total listings in Capetown, there are no inactive listings in the data. Active listings is 100% and inactive listings is 0%.

Question 2: How many distinct hosts are present in the CapeTown AirBnB listing? How many listings does each of this distinct hosts have? Which host have the most listings

SQL Queries:
SELECT COUNT(DISTINCT host_id) AS distinct_hosts
FROM listings;

SELECT host_id, COUNT(*) AS number_listings_per_host
FROM listings
GROUP BY host_id
ORDER BY number_listings_per_host DESC
LIMIT 10;

SELECT host_id, COUNT(*) AS number_listings
FROM listings
GROUP BY host_id
ORDER BY number_listings DESC
LIMIT 10;

Answer:Distinct hosts that are present in Capetown are 11,303. Host with the most listing is host_id 487012580 with 155 listings.

Question 3: On Availability, What is the total number of listings available for more than 90 days a year? How many listings have availabil ity for less than 30 days a year? What percentage of listings are available for instant booking?

SQL Queries:
SELECT COUNT(*) AS listings_more_than_90days
FROM listings
WHERE CAST(availability_365 AS INTEGER)>90;

SELECT COUNT(*) AS listings_less_than_30days
FROM listings
WHERE CAST(availability_365 AS INTEGER)<30;

SELECT(COUNT(*)*100/(SELECT COUNT(*) FROM listings)) AS percentage
FROM listings
WHERE instant_bookable='t';

Answer:Total number of listings available for more than 90 days a year are 14,998 and less than 30 days a year are 3842. Availability of instant_bookable is 27%.

Question 4: What are the different types of properties available and their counts? Which property type has the highest average price? Write a query to show the correlation between review and pricing.

SQL Queries:
Answer:
Entire rental unit-	7932
Entire home-4063
Private room in home-	1375
Entire condo-1060
Entire guest suite-1011
Entire villa-791
Private room in guesthouse-652
Private room in rental unit-631
Entire serviced apartment-484
Entire guesthouse-407
Private room in bed and breakfast-374
Entire cottage-335
Private room in guest suite-278
Entire townhouse-227
Entire loft-221
Room in boutique hotel-148
Entire vacation home-128
Private room in villa-99
Private room in condo-75
Entire bungalow-65
Room in bed and breakfast-62
Room in hotel-61
Private room in townhouse-51
Tiny home-51
Entire place-40
Room in serviced apartment-37
Shared room in home-30
Private room-30
Farm stay-30
Entire cabin-28
Private room in farm stay-23
Private room in serviced apartment-23
Room in aparthotel-21
Private room in bungalow-17
Private room in casa particular-17
Private room in hostel-17
Private room in vacation home-16
Private room in chalet-16
Private room in cottage-15
Shipping container-15
Entire chalet-15
Room in hostel-13
Shared room in rental unit-11
Shared room in hostel-11
Camper/RV-9
Private room in loft-9
Private room in nature lodge-8
Casa particular-7
Private room in tiny home-7
Shared room in bed and breakfast-6
Private room in cabin"	6
Shared room in guesthouse-5
Shared room in boutique hotel-5
Earthen home-4
Private room in dome-4
Private room in camper/rv-3
Shared room in townhouse-3
Tower-3
Room in guesthouse-3
Barn-3
Shared room in dome-3
Shared room in villa-2
Shared room-2
Shared room in loft-2
Hut-2
Private room in earthen home-2
Treehouse-2
Shared room in tiny home-1
Castle-	1
Dome-1
Shared room in houseboat-1
Houseboat-1
Private room in treehouse-1
Private room in barn-1
Room in heritage hotel-1
Private room in hut-1
Floor-	1
Shared room in serviced apartment-1
Shared room in earthen home-1
SELECT AVG(review_score_rating) AS average_review_scores_rating, AVG(CAST(REPLACE(REPLACE(price, '$', ''), ',', '') AS NUMERIC)) AS average_price 
FROM listings 
WHERE review_score_rating IS NOT NULL

Shared room in hotel-1The Entire Villa also has the highest average price at $13742.745891276865. The correlation between review scores ratings and pricing on the average is 4.6958293224731581 Vs 2328.1151425398000740

Question 5: How do individual listings or hosts perform compared to the average or top-performing ones in terms of ratings, pricing, and booking frequency?

SQL Queries:
SELECT review_score_rating
FROM listings
WHERE review_score_rating IS NOT NULL;

SELECT AVG(review_score_rating)	AS average_review_score_rating
FROM listings
WHERE review_score_rating IS NOT NULL;

SELECT id, AVG(CAST(REPLACE(REPLACE(price, '$', ''), ',', '') AS NUMERIC)) AS average_price,
CAST(REPLACE(REPLACE(price, '$', ''), ',', '') AS NUMERIC) AS listing_price 
FROM listings 
GROUP BY 1, 3;	

SELECT AVG(CASE WHEN instant_bookable = 't' THEN 1 ELSE 0 END) AS average_instant_booking_frequency 
FROM listings;

Answer:With an average score of 4.6958293224731581 across all ratings, the review does well. The listing id of 52754312 also has the highest listing price with the average price also pegged at a similar value. The average instant booking frequency across all listings is also 0.278125.
