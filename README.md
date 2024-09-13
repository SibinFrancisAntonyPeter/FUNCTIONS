# FUNCTIONS
# USING COUNTRY TABLE AND PERSON TABLE

SELECT * FROM Country;
SELECT * FROM Persons;

# 1. Add a new column called DOB in Persons table with data type as Date.

ALTER TABLE Persons 
ADD DOB DATE;

UPDATE Persons
SET DOB = CASE 
             WHEN Id = 1 THEN '1990-05-15'
             WHEN Id = 2 THEN '1985-12-22'
             WHEN Id = 3 THEN '2000-03-10'
             WHEN Id = 4 THEN '1992-07-25'
             WHEN Id = 5 THEN '1988-11-30'
             WHEN Id = 6 THEN '1975-06-18'
             WHEN Id = 7 THEN '1999-09-14'
             WHEN Id = 8 THEN '2001-01-01'
             WHEN Id = 9 THEN '1993-04-12'
             WHEN Id = 10 THEN '1980-08-20'
             WHEN Id = 11 THEN '2005-03-21'
             WHEN Id = 12 THEN '1996-02-29'
          END
WHERE Id IN (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12);

# 2. Write a user-defined function to calculate age using DOB.

DELIMITER $$
CREATE FUNCTION Calculate_age (DOB DATE)
RETURNS INT
DETERMINISTIC
BEGIN
RETURN TIMESTAMPDIFF(YEAR, DOB, CURDATE());
END $$
DELIMITER ;

# 3. Write a select query to fetch the Age of all persons using the function that has been created. 

SELECT Id,Fname,Lname, Calculate_age(DOB) AS Age FROM Persons;

# 4. Find the length of each country name in the Country table.

SELECT Id, Country_name,length(Country_name) AS Namelength FROM Country;

# 5. Extract the first three characters of each country's name in the Country table. 

SELECT SUBSTRING(Country_name,1,3) AS First_Three_Characters FROM Country;

-- SELECT ID, Country_name, LEFT(Country_name, 3) AS First_Three_Characters FROM Country;

# 6. Convert all country names to uppercase and lowercase in the Country table.

SELECT Id, Country_name, 
	ucase(Country_name) AS UppercaseName,
	lcase(Country_name) AS LowercaseName
FROM Country;

-- SELECT ID, Country_name, UPPER(Country_name) AS UppercaseName, LOWER(Country_name) AS LowercaseName FROM Country;
