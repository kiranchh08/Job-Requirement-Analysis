# Job-Requirement-Analysis
Job Market Skill Demand Analysis using PostgreSQL and Python
Project Overview
The objective of this project is to analyze real-world job market data to identify in-demand technical skills across different job roles, locations, and experience levels. This analysis helps understand hiring trends and skill requirements in the global job market using structured data analytics techniques.

The project follows a complete data analytics pipeline including:
Data Cleaning
Data Transformation
Skill Segmentation
Database Integration
SQL-Based Data Modeling
Analytical Aggregations
Visualization and Insight Generation
PostgreSQL was used for structured data storage and transformation, while Python was used for analytical computation and visualization.

Dataset Description
The analysis was performed using three raw datasets:

Table: raw_job_postings
Contains job-level metadata such as:
job_link
job_title
company
job_location
search_city
search_country
job_level
job_type
first_seen

Table: raw_job_skills
Contains job skill information:
job_link
job_skills

Each job record may contain multiple skills stored as a comma-separated string.

Table: job_skill_demand
Derived table created after cleaning and filtering technical skills from job_skills and computing demand count for each technical skill.

Data Cleaning and Preprocessing
Handling Missing Values

Table: raw_job_postings

Column company contained 11 NULL values
Column job_location contained 19 NULL values
These NULL values were replaced with the label "Unknown" instead of deleting them since the number of missing records was minimal and job location and company name were not critical for skill demand analysis.

Table: raw_job_skills
Column job_skills contained 2085 NULL values
These records were removed as skill analysis was the primary focus of the project. Compared to the total dataset size, 2085 records were negligible.

Duplicate Records:
Duplicate job records were checked across all tables and no duplicates were found.

Skill Extraction and Normalization
Each job posting contained multiple skills stored as a comma-separated string. These were:
Converted to lowercase
Split into individual skill entries
Cleaned by removing special characters
Trimmed to remove whitespace
Standardized to merge similar skill variants

Examples:
"Python Programming" → Python
"Python Developer" → Python
"Structured Query Language" → SQL
"Microsoft Excel" → Excel

This normalization prevented duplicate counting of semantically identical skills.

Technical Skill Filtering

Many non-technical skills such as:
Communication, Leadership, Problem Solving, Teamwork, Analytical Thinking, were present in the dataset.

A predefined list of technical skills was used to filter out soft skills and retain only job-relevant technical competencies such as:

Python
SQL
Excel
Machine Learning
AWS
Azure
Tableau
Power BI
Docker
Kubernetes
React
TensorFlow

This resulted in a curated dataset of technical skills used for further analysis.

Aggregation and Demand Analysis
The demand for each technical skill was computed using COUNT aggregation after exploding multi-skill job entries into separate rows.

Top 50 most in-demand technical skills were extracted and stored in the PostgreSQL table:
job_skill_demand

A database view named:

top_50_skills
was created for optimized querying during visualization.

Data Modeling

A master join view was created by integrating:
raw_job_postings
raw_job_skills
top_50_skills

This combined dataset enabled multi-dimensional analysis involving:

Job Type
Job Level
Geographic Location
Skill Demand
Visualization

Python libraries used:
Pandas
Matplotlib
Seaborn
SQLAlchemy

A Jupyter Notebook was used to generate analytical visualizations including:
Top In-Demand Technical Skills
Skill Demand by Country
Skill Demand by Job Level
Skill Demand by Job Type
Average Number of Skills Required per Job Level
Average Skill Requirement per Job Type
Skill Distribution Across Countries
Job-Level Skill Requirement Distribution
Country-wise Technical Skill Heatmaps
SQL was used for efficient data extraction while Python was used for analytical computation and visualization to minimize memory and storage overhead.

Challenges Faced

Handling multi-skill entries stored in a single column
Normalizing similar technical skill variations
Removing soft skills from job descriptions
Managing large dataset transformations
Resolving ambiguous joins during table integration
Ensuring only technical skills were considered for demand analysis

Key Insights

Data Analysis, Excel, Python, and SQL are among the most in-demand technical skills
Cloud platforms such as AWS and Azure are consistently required
Machine Learning and Deep Learning skills are in growing demand
Frontend technologies like React and Angular show steady hiring trends
Entry-level jobs typically require fewer technical skill combinations compared to mid-level roles

Tools and Technologies Used
PostgreSQL
Python
Pandas
Matplotlib
Seaborn
SQLAlchemy
Jupyter Notebook

License
This project is licensed under the MIT License.

This project is licensed under the MIT License.

