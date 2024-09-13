# Create dataset
In the Explorer menu, find one of your projects. It may be titled “My First Project” or a title you gave it. Click the three dot icon, then select Create dataset. Fill in “mydataset” for the Dataset ID and set the location to “us (multiple regions in United States).” Then select Create dataset.
![image](https://github.com/user-attachments/assets/4088a10c-c199-4ce4-adb0-dda64366bfa1)

# Load the avocado data into a table
Next to mydataset, click the three-dot icon and select Create table.
![image](https://github.com/user-attachments/assets/4c2a10eb-9b5a-4c89-92f8-a17e15638590)
Next, use the Create table from the dropdown menu and select Upload. Choose the CSV file you downloaded earlier in this activity.
![image](https://github.com/user-attachments/assets/1473992a-d4f7-483b-ad47-24f6a0853c4b)
Then, name the table avocado_base.” Make sure the Dataset field reads “mydataset” and the Table type field reads “Native table.”
![image](https://github.com/user-attachments/assets/18c57ca9-b2b5-42ff-ade5-63cd12503c23)

In the Schema section of the interface, check the box for Auto detect.

Then select Create table.
![image](https://github.com/user-attachments/assets/0b927141-0367-4cf8-91b3-e0f6e3729f45)

# Part 2: Create tables with partitions and clusters

## Step 1: Create tables with partitions and clusters
To begin, create a new table without a partition or cluster. This will serve as a baseline to compare to the partitioned and clustered tables. Name it avocados.

Then, in the Editor tab, copy and paste the following SQL code and click Run. 
CREATE TABLE
    `mydataset.avocados`
AS (
    SELECT
        *
    FROM `mydataset.avocado_base`
);

When you finish running the code, switch to the Results tab. Click Go to table and take note of the Details pane. Save the details for later by taking a screenshot or copying and pasting the information into another document. The dates on your screen might differ, but the table size, long-term storage size, and number of rows should be the same as in the following image.
![image](https://github.com/user-attachments/assets/3329be64-9979-470d-b269-7cf370b6ee99)

## Step 2: Create a table with a partition
Next, create a table partitioned by an integer range (the years 2015 through 2022). Name it avocados_partitioned.

Return to the tab you entered the SQL code into. Delete that code then copy and paste the following SQL code. Click Run.

CREATE TABLE
    `mydataset.avocados_partitioned`
PARTITION BY
    RANGE_BUCKET(Year, GENERATE_ARRAY(2015,2022,1))
AS (
    SELECT
        *
    FROM `mydataset.avocado_base`
);

When you finish running the code, switch to the Results tab. Click Go to table and take note of the Details pane. Save the details for later by taking a screenshot or copying and pasting the information into another document. After this activity, you’ll compare this to the exemplar.

## Step 3: Create a table with a partition and a cluster
Next, create a table partitioned by an integer range and clustered by type. Name it avocados_clustered.

Return to the tab where you entered the SQL code. Delete that code, then copy and paste the following SQL code. Click Run.
CREATE TABLE
    `mydataset.avocados_clustered`
PARTITION BY
    RANGE_BUCKET(Year, GENERATE_ARRAY(2015,2022,1))
CLUSTER BY
    type
AS (
    SELECT
        *
    FROM `mydataset.avocado_base`
);

When you finish running the code, switch to the Results tab. Click Go to table and take note of the Details pane. Save the details for later by taking a screenshot or copying and pasting the information into another document. After this activity, you’ll compare this to the exemplar. 

# Part 3: Query the tables and compare performance
## Step 1: Query the table without a partition or cluster
Delete the code in the Editor tab, then copy and paste the following code. Click Run to query avocados—the table without partition or cluster.
SELECT
    year,
    COUNT(*) AS number_avocados,
    SUM(TotalVolume) AS sum_totalVolume,
    SUM(AveragePrice) AS sum_AveragePrice
FROM `mydataset.avocados`
WHERE type = 'organic'
GROUP BY year
ORDER BY year ASC;

When the query has finished running, check the Execution details tab. This explains that the number of records read is the total number of records in the table. In this query, the database processes all records from the table. This is reflected in S00:Input.

![image](https://github.com/user-attachments/assets/735b4ca1-4ae9-439d-9afe-b1fdcf41b173)

In the next steps, take note of the S00 and S01 rows as described in the preceding screenshot. You will need to compare these details to the exemplar.

## Step 2: Query the partitioned table
Delete the code in the Editor tab, then copy and paste the following code. Click Run to query avocados_partitioned—the table that is partitioned by an integer range.

SELECT
    year,
    COUNT(*) AS number_avocados,
    SUM(TotalVolume) as sum_TotalVolume,
    SUM(AveragePrice) as sum_AveragePrice
FROM `mydataset.avocados_partitioned`
WHERE type = 'organic'
GROUP BY year
ORDER BY year ASC;

When the query has finished running, check the Execution details tab and save a screenshot of it. You’ll need to compare these details to the exemplar.

## Step 3: Query the partitioned and clustered table
Delete the code in the Editor tab, then copy and paste the following code. Click Run to query avocados_clustered—the table that is partitioned by an integer range and clustered by type.

SELECT
    year,
    COUNT(*) AS number_avocados,
    SUM(TotalVolume) as sum_TotalVolume,
    SUM(AveragePrice) as sum_AveragePrice
FROM `mydataset.avocados_clustered`
WHERE type = 'organic'
GROUP BY year
ORDER BY year ASC;

When the query has finished running, check the Execution details tab and save a screenshot of it. You will need to compare these details to the exemplar.








