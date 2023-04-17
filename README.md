# Analysis of E-commerce with SQL

## Project/Goals
- Create a **postgresql database** of *ecommerce* data with **pgadmin4**
- Develop insights on ecommerce data using **postgresql queries**
- Document project parts with **markdown files**
- Keep track of changes to project files with **git and gitHub**

## Process
### 1. [Clean data](cleaning_data.md)
### 2. [Answer provided questions](starting_with_questions.md)
### 3. [Answer novel questions](starting_with_data.md)
### 4. [Validate answers](QA.md)

## Results
- The top selling products are Nest brand products, making up four of the top 5.
- Over 90% of sales revenue comes from the United States.
- Exploration into correlations between webpage interaction and product orders/revenue can be made with the assumption that each row in *all_sessions* logs an interaction with a product.

## Challenges 
Not having a dictionary to explain the data was the largest hurdle in drawing conclusions, and the biggest challenge to validation.

## Future Goals
Without a dictionary the *ecommerce* data is unreliable. Moving forward it would be best to restructure the data collection process to provide clearer logs with more concise metrics.
