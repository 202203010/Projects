# Grow More Reading Library
CREATE DATABASE seat_booking;
USE seat_booking;

-- Step 2: Create Seats Table
CREATE TABLE seats (
    id INT AUTO_INCREMENT PRIMARY KEY,
    seat_number INT,
    is_booked BOOLEAN DEFAULT FALSE,
    is_premium BOOLEAN DEFAULT FALSE,
    end_date DATE DEFAULT NULL,
    library_name VARCHAR(50),
    student_name VARCHAR(100),
    phone_number VARCHAR(15),
    email VARCHAR(100),
    target_exam VARCHAR(100)
);

-- Step 3: Create Inquiries Table
CREATE TABLE inquiries (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    phone_number VARCHAR(15),
    email VARCHAR(100),
    interested_in VARCHAR(100),
    message TEXT,
    inquiry_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Step 4: Insert 60 seats for Rajkot (seat_number = 1 to 60)
INSERT INTO seats (seat_number, library_name)
SELECT n, 'Rajkot'
FROM (
    SELECT @row := @row + 1 AS n
    FROM (SELECT 0 UNION ALL SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 
          UNION ALL SELECT 4 UNION ALL SELECT 5 UNION ALL SELECT 6 
          UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9) t1,
         (SELECT 0 UNION ALL SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 
          UNION ALL SELECT 4 UNION ALL SELECT 5 UNION ALL SELECT 6 
          UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9) t2,
         (SELECT @row := 0) t0
) AS numbers
WHERE n <= 60;

-- Step 5: Insert 60 seats for Morbi (seat_number = 1 to 60)
INSERT INTO seats (seat_number, library_name)
SELECT n, 'Morbi'
FROM (
    SELECT @row := @row + 1 AS n
    FROM (SELECT 0 UNION ALL SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 
          UNION ALL SELECT 4 UNION ALL SELECT 5 UNION ALL SELECT 6 
          UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9) t1,
         (SELECT 0 UNION ALL SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 
          UNION ALL SELECT 4 UNION ALL SELECT 5 UNION ALL SELECT 6 
          UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9) t2,
         (SELECT @row := 0) t0
) AS numbers
WHERE n <= 60;

-- Step 6: Set 5–10 premium seats randomly in Rajkot
UPDATE seats
SET is_premium = 1
WHERE library_name = 'Rajkot'
ORDER BY RAND()
LIMIT 8;

-- Step 7: Set 5–10 premium seats randomly in Morbi
UPDATE seats
SET is_premium = 1
WHERE library_name = 'Morbi'
ORDER BY RAND()
LIMIT 7;



CREATE TABLE transactions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100) NOT NULL,
    phone_number VARCHAR(15) NOT NULL,
    seat_number INT NOT NULL,
    transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    amount DECIMAL(10, 2) NOT NULL,
    library_name VARCHAR(50) NOT NULL
);
