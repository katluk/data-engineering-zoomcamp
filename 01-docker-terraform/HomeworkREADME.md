### Question 1: 
Which tag has the following text? - Automatically remove the container when it exits
```
docker run --help
```
### Question 2:
What is version of the package wheel ?
```
docker run -it --entrypoint=bash python:3.9
pip list
```
### Question 3:
How many taxi trips were totally made on September 18th 2019?
```
SELECT COUNT(*) FROM green_taxi_data WHERE DATE(lpep_pickup_datetime) = '2019-09-18' AND DATE(lpep_dropoff_datetime) = '2019-09-18'
```
### Question 4:

Which was the pick up day with the longest trip distance? 
```
SELECT DATE(lpep_pickup_datetime) AS pickup_day, MAX(trip_distance) AS max_distance FROM green_taxi_data GROUP BY DATE(lpep_pickup_datetime) ORDER BY max_distance DESC LIMIT 1
```
### Question 5:
Consider lpep_pickup_datetime in '2019-09-18' and ignoring Borough has Unknown

Which were the 3 pick up Boroughs that had a sum of total_amount superior to 50000?
```
SELECT z."Borough", SUM(g.total_amount) AS total_revenue FROM green_taxi_data g JOIN zone z ON g."PULocationID" = z."LocationID" WHERE DATE(g.lpep_pickup_datetime) = '2019-09-18' AND z."Borough" != 'Unknown' GROUP BY z."Borough" HAVING SUM(g.tota
 l_amount) > 50000 ORDER BY total_revenue DESC LIMIT 3
 ```
 ### Question 6:
 For the passengers picked up in September 2019 in the zone name Astoria which was the drop off zone that had the largest tip? We want the name of the zone, not the id.
 ```
 SELECT z_drop."Zone" AS drop_off_zone, MAX(g.tip_amount) AS max_tip FROM green_taxi_data g JOIN zone z_pick ON g."PULocationID" = z_pick."LocationID" JOIN zone z_drop ON g."DOLocationID" = z_drop."LocationID" WHERE z_pick."Zone" = 'Astoria' AND D
 ATE_TRUNC('month', g.lpep_pickup_datetime) = '2019-09-01' GROUP BY z_drop."Zone" ORDER BY max_tip DESC LIMIT 1
 ```