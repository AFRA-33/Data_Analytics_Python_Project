# Restaurant Data Analysis Project Using Python

## Table of Contents
1. [Project Overview](#project-overview)
2. [Dataset Description](#dataset-description)
3. [Installation and Setup](#installation-and-setup)
4. [Analysis Overview](#analysis-overview)
7. [File Structure](#file-structure)
8. [Contributing](#contributing)


## Project Overview
This project explores a comprehensive dataset of restaurants, focusing on key factors such as price range, availability of online delivery and table booking services, and aggregate ratings. By performing exploratory data analysis (EDA), this project aims to uncover insights into how these factors interact and influence customer satisfaction and restaurant performance.

## Dataset Description
The dataset contains the following columns:

| Column Name              | Description                                         |
|--------------------------|-----------------------------------------------------|
| Restaurant ID            | Unique identifier for each restaurant               |
| Restaurant Name          | Name of the restaurant                               |
| Country Code             | Country where the restaurant is located             |
| City                     | City where the restaurant is located                |
| Address                  | Address of the restaurant                            |
| Locality                 | Locality of the restaurant                           |
| Longitude                | Longitude coordinate of the restaurant               |
| Latitude                 | Latitude coordinate of the restaurant                |
| Cuisines                 | Types of cuisines offered by the restaurant          |
| Average Cost for Two     | Average cost for two people to dine                 |
| Currency                 | Currency used for pricing                           |
| Has Table Booking        | Availability of table booking (1 for Yes, 0 for No) |
| Has Online Delivery      | Availability of online delivery (1 for Yes, 0 for No, NaN for unknown) |
| Price Range              | Restaurant price range (1 to 4)                     |
| Aggregate Rating         | Overall restaurant rating                            |
| Rating Color             | Color associated with the rating                     |
| Rating Text              | Descriptive rating category (e.g., "Good", "Average") |
| Votes                    | Number of votes received by the restaurant           |

## Installation and Setup

### Prerequisites
Make sure you have Python installed along with the following libraries:
```bash
pip install pandas matplotlib seaborn geopandas
```

### Project Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/AFRA-33/Data_Analytics_Python_Project.git
   cd Data_Analytics_Python_Project
   ```

Run the analysis scripts in your preferred environment (e.g., Jupyter Notebook, Python script).

## Analysis Overview

### Top three most common cuisines in the dataset
 We looked at various aspects of the restaurant dataset, including the distribution of cuisines across different restaurants. The analysis revealed that **North Indian** cuisine is the most popular, followed by a combination of **North Indian and Chinese**, and **Fast Food**. This information is crucial for understanding customer preferences in the regions covered by the dataset.

Here are the top three most common cuisines:

```python
# Code to determine the top three cuisines
top_cuisines = df['Cuisines'].value_counts().head(3)
print("The top three cuisines in the dataset are :")
top_cuisines
```

#### Results:

- **North Indian**: 936 restaurants
- **North Indian, Chinese**: 511 restaurants
- **Fast Food**: 354 restaurants


### Percentage of restaurants that serve each of the top cuisines

We analyzed the distribution of different cuisines served by the restaurants in the dataset. The top three most common cuisines served are **North Indian**, **North Indian and Chinese**, and **Fast Food**. Below are the percentages of restaurants that serve these cuisines relative to the total number of restaurants:

```python
# Code to calculate the total number of restaurants
total_restaurants = len(df)

# Code to calculate the percentage of restaurants serving each of the top cuisines
top_cuisines = df['Cuisines'].value_counts().head(3)
top_cuisines_percentage = (top_cuisines / total_restaurants) * 100
top_cuisines_percentage = top_cuisines_percentage.apply(lambda x: f"{x:.2f}%")

# Output the percentages
print("Percentage of restaurants that serve each of the top cuisines are:")
print(top_cuisines_percentage)
```

#### Results:

- **North Indian**: 9.80%
- **North Indian, Chinese**: 5.35%
- **Fast Food**: 3.71%

These percentages provide an overview of the most popular types of cuisines offered by restaurants, which can help businesses make informed decisions about the cuisine offerings in various regions.


### Highest number of restaurants in the dataset
 We identified that **New Delhi** has the highest number of restaurants. This provides valuable insights into regional restaurant density and market saturation. 

```python
# Code to find the city with the highest number of restaurants
top_city = df['City'].value_counts().idxmax()

# Code to find the number of restaurants in the top city
no_restaurants_in_city = df['City'].value_counts().max()

# Output the result
print(f"The city with the highest number of restaurants in the dataset is {top_city} with {no_restaurants_in_city} restaurants.")
```

#### Result:

- **City**: New Delhi
- **Number of Restaurants**: 5,473

This data shows that New Delhi is a significant market for restaurants, offering opportunities for both new and established businesses to tap into a large consumer base.


### Distribution of Aggregate Ratings

We analyzed the distribution of aggregate ratings across restaurants to understand how customers typically rate their dining experiences. The distribution plot below shows how ratings are spread, with the most common rating range between 3.0 and 4.0.

```python
# Code to plot the distribution of aggregate ratings
plt.figure(figsize=(10,6))
sns.histplot(df['Aggregate rating'], bins=10, kde=True, color='skyblue')
plt.title('Distribution of Aggregate Rating')
plt.xlabel('Aggregate Rating')
plt.ylabel('Frequency')
plt.show()

# Code to determine the most common rating range
df['Rating Range'] = pd.cut(df['Aggregate rating'], bins=[0, 1, 2, 3, 4, 5], include_lowest=True)
most_common_rating_range = df['Rating Range'].mode()[0]
print(f"The most common rating range is {most_common_rating_range}")
```

#### Results:

- **Most Common Rating Range**: (3.0, 4.0]

The majority of restaurants fall within the 3.0 to 4.0 rating range, which indicates a trend of moderate customer satisfaction in the dataset.


### Most Common Combinations of Cuisines

We explored the dataset to identify the most common cuisine combinations offered by restaurants. Understanding the cuisine combinations can help determine customer preferences and restaurant offerings. Below are the top five most common combinations of cuisines:

```python
# Code to determine the most common combinations of cuisines
top_cuisines = df['Cuisines'].value_counts().head(5)

# Output the top five cuisine combinations
print("The top most common combinations of cuisines in the dataset are:")
top_cuisines
```

#### Results:

1. **North Indian**: 936 restaurants
2. **North Indian, Chinese**: 511 restaurants
3. **Fast Food**: 354 restaurants
4. **Chinese**: 354 restaurants
5. **North Indian, Mughlai**: 334 restaurants

This insight shows that **North Indian** cuisine is the most popular, with combinations like **North Indian & Chinese** and **North Indian & Mughlai** also being popular choices in the dataset.


### Distribution of Rating Texts and Common Keywords

We explored the rating texts provided by customers to identify trends in feedback. This analysis helps us understand the frequency of positive and negative reviews, as well as customer sentiment.

```python
# Code to analyze the distribution of rating texts
rating_counts = df['Rating text'].value_counts()

# Plotting the distribution of rating texts
plt.figure(figsize=(8,5))
sns.barplot(x=rating_counts.index, y=rating_counts.values, hue=rating_counts.index, palette='viridis', legend=False)
plt.title("Distribution of Rating Texts")
plt.xlabel("Rating Text")
plt.ylabel("Count")
plt.xticks(rotation=45)
plt.show()
```

#### Results:

The rating texts are distributed as follows:

- **Average**: 3,737 reviews
- **Not Rated**: 2,148 reviews
- **Good**: 2,100 reviews
- **Very Good**: 1,079 reviews
- **Excellent**: 301 reviews
- **Poor**: 186 reviews

This analysis shows that most of the ratings fall under the "Average" and "Good" categories, indicating that customers generally have moderate satisfaction with their dining experiences. The least frequent reviews are "Excellent" and "Poor," which reflect extreme sentiments (very positive or very negative).


### Average Length of Reviews and Its Relationship with Ratings

We analyzed the average length of text reviews and explored if there is any relationship between the length of the review and the aggregate rating given by customers. This analysis helps in understanding how detailed the reviews are in relation to customer satisfaction.

```python
# Calculate the length of each review
df['Rating length'] = df['Rating text'].apply(lambda x: len(str(x).split()))

# Calculate the average review length
avg_review_length = df['Rating length'].mean()
print(f"The average review length is: {avg_review_length:.2f} words.")

# Plotting the relationship between review length and aggregate rating
plt.figure(figsize=(10,6))
sns.scatterplot(x='Aggregate rating', y='Rating length', data=df, hue='Rating text', palette='coolwarm', legend=False)
plt.title("Review Length vs Aggregate Rating")
plt.xlabel('Aggregate Rating')
plt.ylabel('Review Length')
plt.show()
```

#### Results:

- **Average Review Length**: 1.34 words

The scatter plot above shows that there is a slight variation in review lengths across different aggregate ratings. However, most of the reviews are quite short, often consisting of just one or two words. This may suggest that customers tend to leave concise feedback, regardless of whether the rating is positive or negative.


### Restaurants with the Highest and Lowest Number of Votes

Identifying restaurants with the most and the least votes helps us understand which restaurants are the most and least popular, according to customer engagement.

```python
# Sorting restaurants by the number of votes
sorted_df = df.sort_values(by='Votes', ascending=False)

# Identifying the restaurant with the highest and lowest number of votes
highest_votes = sorted_df.iloc[0]
lowest_votes = sorted_df.iloc[-1]

print("Restaurant with the highest number of votes:")
print(highest_votes[['Restaurant Name', 'Votes']])

print("\nRestaurant with the lowest number of votes:")
print(lowest_votes[['Restaurant Name', 'Votes']])
```

#### Results:

- **Restaurant with the Highest Number of Votes:**
  - **Name:** Toit
  - **Votes:** 10,934

- **Restaurant with the Lowest Number of Votes:**
  - **Name:** Do Bhai Paneer Wale And Sweets
  - **Votes:** 0

This analysis shows that "Toit" is the most popular restaurant based on customer engagement, while "Do Bhai Paneer Wale And Sweets" had the least engagement in terms of votes.


### Correlation Between the Number of Votes and the Rating of a Restaurant

We analyzed whether there is a relationship between the number of votes a restaurant receives and its rating. This can provide insights into how customer engagement (measured by votes) relates to customer satisfaction (measured by rating).

```python
# Calculate the correlation between votes and rating
correlation = df[['Rating numeric', 'Votes']].corr().iloc[0,1]
print(f"Correlation between the number of votes and the rating of a restaurant is {correlation:.2f}")

# Plot the relationship between votes and rating
plt.figure(figsize=(10,6))
sns.scatterplot(x='Votes', y='Rating numeric', data=df)
plt.title("Votes vs Rating")
plt.xlabel("Number of Votes")
plt.ylabel("Numeric Rating")
plt.show()
```

#### Results:

- **Correlation between Votes and Rating**: 0.40

This positive correlation indicates that there is a moderate relationship between the number of votes and the rating of a restaurant. As the number of votes increases, the rating tends to improve, but the correlation is not very strong, implying other factors also play a role in determining restaurant ratings.



#### Relationship Between Price Range and Availability of Online Delivery and Table Booking

We explored whether higher-priced restaurants are more likely to offer services such as online delivery and table booking. This analysis helps in understanding the service availability across different price ranges.

```python
# Plot the relationship between price range and availability of online delivery and table booking
plt.figure(figsize=(14,6))

# Subplot 1: Online Delivery by Price Range
plt.subplot(1,2,1)
sns.barplot(x='Price range', y='Votes', data=df, hue='Has Online delivery', palette='Set1')
plt.title("Average Online Delivery by Price Range")
plt.xlabel('Price range')
plt.ylabel("Average Availability")

# Subplot 2: Table Booking by Price Range
plt.subplot(1,2,2)
sns.barplot(x='Price range', y='Votes', data=df, hue='Has Table booking', palette='Set1')
plt.title("Average Table Booking by Price Range")
plt.xlabel('Price range')
plt.ylabel("Average Availability")

plt.show()
```

#### Results:

- **Online Delivery**: Higher-priced restaurants tend to offer online delivery more frequently compared to lower-priced ones.
- **Table Booking**: Similarly, restaurants with a higher price range are more likely to offer table booking services.


#### Relationship Between Price Range and Availability of Services

In this section, we aim to determine whether higher-priced restaurants are more likely to offer online delivery and table booking services. This analysis is valuable for understanding how pricing influences service availability.

```python
# Count of restaurants by price range
df['Price range'].value_counts()
```
```plaintext
Price Range
1    4444
2    3113
3    1408
4     586
Name: count, dtype: int64
```

We visualize the relationship using count plots for both services:

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 5))

# For Online Delivery
sns.countplot(x='Price range', hue='Has Online delivery', data=df, ax=axes[0], palette='viridis')
axes[0].set_title('Price Range vs Online Delivery')
axes[0].set_xlabel('Price Range')
axes[0].set_ylabel('Counts')
axes[0].legend(title='Online Delivery', labels=['No', 'Yes'])

# For Table Booking
sns.countplot(x='Price range', hue='Has Table booking', data=df, ax=axes[1], palette='viridis')
axes[1].set_title('Price Range vs Table Booking')
axes[1].set_xlabel('Price Range')
axes[1].set_ylabel('Counts')
axes[1].legend(title='Table Booking', labels=['No', 'Yes'])

plt.tight_layout()
plt.show()
```

#### Results:

- **Price Range vs Online Delivery**: The count plot indicates whether online delivery is more commonly offered by higher-priced restaurants.
- **Price Range vs Table Booking**: Similarly, we observe the relationship between price range and the availability of table booking services.

These visualizations reveal patterns that can help both customers looking for services and restaurant owners in strategizing their offerings based on pricing.


## File Structure
```
restaurant-data-analysis/
│
├── data/                   # Directory for dataset(s)
│   └── restaurants.csv      # Restaurant data file
├── notebooks/               # Jupyter notebooks for analysis
├── scripts/                 # Python scripts for data analysis
├── README.md                # Project documentation (this file)
└── requirements.txt         # List of required libraries and dependencies
```

## Contributing
Contributions are welcome! If you would like to contribute:
1. Fork the repository.
2. Create a new branch.
3. Make your changes and submit a pull request.

