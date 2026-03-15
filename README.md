## README for Initial Modeling of Cost Projection & Timeline Projection

## REQUIREMENTS:
Install required packages:

pip install pandas scikit-learn

What I've done so far has mainly consisted of combining the two datasets through merging with queue data on project ID. 
The two datasets: 
1. GI_Interactive_Queue: provides project attributes such as capacity, fuel type, queue timing, and etc.

2. gi_master_extracted_data: contains upgrade cost information stored in a JSON structure.

# Data Cleaning

1. Split project_ids into individual rows for projects with multiple IDs. 
2. Parse the project_cost_map_json (apparently needed to transforms strings into actual dictionary objects)
3. Extracts project-level upgrade costs from the JSON structure.


# The Cost modeling is done through a linear regression model with basic labeling engineering:

The target variable: cost (extracted from the cost map)
The input feature: Summer MW (Only included one feature so far to ensure that the model is working)

The linear regression model is done with scikit-learn:
  Cost = Intercept + (Coefficient × Summer MW)

  The model outputs:
  Regression intercept
  Cost coefficient per MW
  Example cost prediction for a hypothetical project

The example: a prediction for a 100 MW project, estimating the expected upgrade cost using the trained model.

# Timeline Prediction modeling

Goal: Trying to calculate the median timeline since the average is too skewed. 

Input feature: in_service_timeline 

There is a function to parse strings like "24-48 months" from the datasets, the script converts them into numeric values by:
  removing the word "months."
  splitting the lower and upper bounds
  Taking the average of the range

And then calculate the median. Currently, the baseline model (example) doesn't matter since it will all just come out to be the median as the initial result. 

