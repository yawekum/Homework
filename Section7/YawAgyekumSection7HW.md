# Section 7.1
## Question 1
## Using EVregistry, Write a query to select the ModelYear, Make, and Model off all of the vehicles in the registry.

SELECT  ModelYear, Make, Model
FROM EVRegistry

## Question 2
## Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your reult set should have one column, ElectricVehicleType.

SELECT DISTINCT ElectricVehicleType
FROM EVRegistry

## Question 3
## Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry.

SELECT *
FROM EVRegistry
WHERE ElectricVehicleType LIKE 'Battery%'

## Question 4
## Using the EVRegistry, wirte a query that returns the Make and Model of all of the EV's that have a BaseMSRP between 20000 and 35000?

SELECT Make, Model
FROM EVRegistry
WHERE BaseMSRP BETWEEN 20000 AND 35000


# Section 7.2
## Question 1
## Using EVRegistry, write a query to find a record where the City attribute is NULL. Return all of the available columns.

SELECT *
FROM EVRegistry
WHERE City is NULL;


## Question 2
## Write a query to find the make, model, and ElectricVehicleType where the VIN number has that ends in '3E1EA1J'.

SELECT Make, Model, ElectricVehicleType
FROM EVRegistry
WHERE VIN like '%3E1EA1J'

## Question 3
## Select the ModelYear, make, model, ElectricVehicleType, and range of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest.

SELECT ModelYear, Make, Model, ElectricVehicleType, ElectricRange
FROM EVRegistry
WHERE Make =  'TESLA' OR Make = 'CHEVROLET'
ORDER BY Make, ModelYear DESC

## Question 4
## Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records.

SELECT stationId, count(userId) as 'numUsage'
FROM EVCharging
GROUP BY stationId
ORDER BY numUsage DESC
LIMIT 5;

## Question 5
## Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively.

SELECT userId, MIN (chargeTimeHrs) as 'minTime', MAX (chargeTimeHrs) as 'maxTime'
FROM EVCharging 
WHERE chargeTimeHrs > 0.5
GROUP BY 1
ORDER BY 2, 3

# Section 7.3
## Question 1 Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.

SELECT weekday, ROUND (AVG(chargeTimeHrs), 2) as 'highChargeAvg'
FROM EVCharging
GROUP BY weekday
ORDER BY highChargeAvg DESC

## Question 2
## Using, EV charging, Find the total power consumed from charging EV's by each User. Return the userId and name the calculated column, totalPower. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users.

SELECT userId, ROUND (SUM(kwhTotal), 2) as 'totalPower'
FROM EVCharging
GROUP BY userId
ORDER BY  totalPower DESC
LIMIT 15

## Question 3
## Using dimfacility and factCharge, write a query to find out which type of facility (GROUP BY) has the most amount of charging stations. Return type Facility and name the calculated column numStation. Order the result set from highest to lowest number of charging stations.

SELECT d.typeFacility, COUNT (stationId) as 'num_Station'
FROM factCharge f INNER JOIN dimFacility d ON f.facilityID = d.FacilityKey
GROUP BY typeFacility
ORDER BY num_Station DESC

## Question 4
## In your own words, Briefly explain Primary Keys and Foreign Keys.
### Foreignn keys are references from Primary keys when 2 tables are connected.

## Question 5
## Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be userid, minTime, and maxTime. Order this result set by the last two columns respectively. HINT: USE HAVING

SELECT userId, MIN(chargeTimeHrs) as 'minTime', MAX (chargeTimeHrs) as 'maxTime'
FROM EVCharging
GROUP BY userId
HAVING chargeTimeHrs > 1
ORDER BY minTime, maxTime