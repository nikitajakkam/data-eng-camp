# Data Engineering Camp
Intro to Data Engineering 

## Homework 1
- Q1: **Answer**: 24.3.1
```
docker run -it --entrypoint bash python:3.12.8
pip --version
```

- Q2: **Answer**: db:5432
 
- Q3: **Answer**: 104,802; 198,924; 109,603; 27,678; 35,189
```
SELECT 
    COUNT(*)
FROM 
    green_taxi_data
WHERE 
    CAST(lpep_pickup_datetime AS DATE) >= '2019-10-01' 
    AND CAST(lpep_dropoff_datetime AS DATE) < '2019-11-01'
	AND trip_distance > 3 AND trip_distance <= 7;
```

- Q4: **Answer**: 2019-10-31
```
SELECT *
FROM green_taxi_data
ORDER BY trip_distance DESC;
```

- Q5: **Answer**: East Harlem North, East Harlem South, Morningside Heights
```
SELECT
    CONCAT(zpu."Borough", ' / ', zpu."Zone") AS "pick_up_loc",
    SUM(t.total_amount) AS total_amount
FROM
    green_taxi_data t LEFT JOIN zones zpu ON t."PULocationID" = zpu."LocationID"
			LEFT JOIN zones zdo ON t."DOLocationID" = zdo."LocationID"
WHERE
    CAST(lpep_pickup_datetime AS DATE) = '2019-10-18'
GROUP BY
    pick_up_loc
ORDER BY
    total_amount DESC;
```

Q6: **Answer**: East Harlem North
```
SELECT
    lpep_pickup_datetime,
    lpep_dropoff_datetime,
    total_amount, 
    CONCAT(zpu."Borough", ' / ', zpu."Zone") AS "pick_up_loc",
    CONCAT(zdo."Borough", ' / ', zpu."Zone") AS "drop_off_loc"
FROM
    green_taxi_data t LEFT JOIN zones zpu ON t."PULocationID" = zpu."LocationID"
			LEFT JOIN zones zdo ON t."DOLocationID" = zdo."LocationID"
WHERE
    zpu."Zone" = 'East Harlem North'
ORDER BY
    t.tip_amount DESC;
```

- Q7: **Answer** terraform init, terraform apply -auto-approve, terraform destroy
