# OLA Ride Bookings – Data Analysis Project
![OLA_LOGO](https://github.com/alhansidd70/OLA_Data_Analysis_Projects/blob/main/Ola%20logo.png)


This project analyzes July ride booking data from OLA using **SQL** and **Power BI** to extract insights, identify patterns, and visualize trends in customer behavior, ride performance, and revenue.

## 🛠 Tools Used
- **SQL**: For data querying and transformation
- **Power BI**: For interactive dashboard creation

##  Key Insights
- Total bookings: **103,024** | Total revenue: **₹35M**
- Top payment methods: **Cash** (₹19.3M) and **UPI** (₹14.2M)
- **E-Bikes** recorded the longest average ride distance (25.15 km)
- Major cancellations due to personal/car issues (drivers) and plan changes (customers)
- Average ratings across vehicle types are consistent (~4.0)

##  Dashboard Highlights
- Ride Volume Over Time
- Booking Status Breakdown
- Revenue by Payment Method
- Top Customers by Booking Value
- Ride Distance & Rating Distributions
- Cancellations by Reason
-- Create Database


# OLA SQL queries
```sql  
CREATE DATABASE Ola;
USE Ola;
```

-- 1. Successful Bookings
```sql
CREATE VIEW Successful_Bookings AS
SELECT * FROM bookings
WHERE Booking_Status = 'Success';
```

-- 2. Average Ride Distance per Vehicle Type
```sql
CREATE VIEW ride_distance_for_each_vehicle AS
SELECT Vehicle_Type, AVG(Ride_Distance) AS avg_distance
FROM bookings
GROUP BY Vehicle_Type;
```

-- 3. Cancelled Rides by Customers
```sql
CREATE VIEW cancelled_rides_by_customers AS
SELECT COUNT(*) AS total_cancellations
FROM bookings
WHERE Booking_Status = 'cancelled by Customer';
```

-- 4. Top 5 Customers by Rides
```sql
CREATE VIEW Top_5_Customers AS
SELECT Customer_ID, COUNT(Booking_ID) AS total_rides
FROM bookings
GROUP BY Customer_ID
ORDER BY total_rides DESC
LIMIT 5;
```

-- 5. Rides Cancelled by Drivers (Personal & Car Issues)
```sql
CREATE VIEW Rides_cancelled_by_Drivers_P_C_Issues AS
SELECT COUNT(*) AS total_driver_cancellations
FROM bookings
WHERE cancelled_Rides_by_Driver = 'Personal & Car related issue';
```

-- 6. Max and Min Driver Ratings for Prime Sedan
```sql
CREATE VIEW Max_Min_Driver_Rating AS
SELECT MAX(Driver_Ratings) AS max_rating,
       MIN(Driver_Ratings) AS min_rating
FROM bookings
WHERE Vehicle_Type = 'Prime Sedan';
```

-- 7. Rides Paid via UPI
```sql
CREATE VIEW UPI_Payment AS
SELECT * FROM bookings
WHERE Payment_Method = 'UPI';
```

-- 8. Avg Customer Rating per Vehicle Type
```sql
CREATE VIEW AVG_Cust_Rating AS
SELECT Vehicle_Type, AVG(Customer_Rating) AS avg_customer_rating
FROM bookings
GROUP BY Vehicle_Type;
```

-- 9. Total Booking Value of Successful Rides
```sql
CREATE VIEW total_successful_ride_value AS
SELECT SUM(Booking_Value) AS total_successful_ride_value
FROM bookings
WHERE Booking_Status = 'Success';
```

-- 10. Incomplete Rides and Their Reasons
```sql
CREATE VIEW Incomplete_Rides_Reason AS
SELECT Booking_ID, Incomplete_Rides_Reason
FROM bookings
WHERE Incomplete_Rides = 'Yes';`
```

