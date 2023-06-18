# Enhanced_Recovery_After_Surgery

Enhanced Recovery After Surgery
Enhanced Recovery After Surgery (ERAS) is a set of protocols used in the management of surgical patients before, during, and after an operation. 
While the specific components of ERAS implemented depend on the type of surgery, there are a few general principles:

Before surgery: pre-surgery counseling, meetings with the surgical team, use of epidural for pain management.
During surgery: shorter inclusions, laparoscopic approaches when possible, conservative opioid pain management.
After surgery: encouraging movement soon after surgery, quick transition to oral pain medications, resumption of normal food/fluid intake.
Prior studies have demonstrated that the use of ERAS programs is associated with increased patient satisfaction, improved use of hospital resources, decreased complications, 
and decreased morbidity and mortality.

Imagine that a hospital system is interested in making the ERAS protocol standard practice for all surgeries at all of its hospitals. One of the hospitals in the system, 
Hospital B, has been using ERAS since the beginning of 2015. Another hospital, Hospital A, does not use it.

The hospital’s administrators commission a study to determine whether the use of ERAS at Hospital B led to a decrease in length of stay (LOS). 
To assess the effectiveness of ERAS, the hospital administrators decide to compare Hospital B to Hospital A. 
The average length of stay at Hospital B and Hospital A was calculated for each of the years between 2010 and 2019.

In this project, we’ll use the Difference in Differences (DID) method to evaluate whether implementation of the ERAS protocol led to a reduction in the average hospital length of stay (LOS).


# Data Exploration

1.
Let’s start by loading the dataset. We’ve provided a file named eras_df.csv in the workspace. Load this file into a dataframe named eras.

2.
Take a look at the head of the dataframe eras. Familiarize yourself with the following variables in the dataset:

year: indicates the year of the surgery.
hospital: indicates where each surgery was performed (Hospital A, Hospital B).
los: hospital length of stay (LOS) in days.

3.
The next step is to plot the data. Filter to just Hospital B and make a line graph to display the change in average hospital LOS over time for Hospital B. 
Add a vertical dashed line to indicate the point in time when Hospital B implemented the ERAS protocol for surgeries.

# Checking for Parallel Trends

4.
Great job so far! We can definitely see a change from 2014 to 2015, but we can’t tell how much is due to using the ERAS system. Let’s plot the data again with Hospital A as a potential control group.

Generate another line graph but this time plot data for both Hospital A and Hospital B with a vertical dashed line at the year 2014.

Do the trends in LOS at each hospital appear similar up to the year 2014? Do you think that the assumption of parallel trends is met?


# Calculating the ATT with Means

5.
Now that we have verified that the parallel trends assumption has been met up to the year 2015, we can continue with calculating the ATT. 
First, let’s create a new dataset called eras2 that uses just the observations from 2014 and 2015. Print eras2 to see the means before and after treatment for both hospitals.

6.
Now take the difference in average LOS from 2014 to 2015 for each hospital. Call this difference Adiff for Hospital A and Bdiff for Hospital B.


7.
Now let’s calculate the difference in differences using Adiff and Bdiff from the previous task.


# Calculating the ATT with Regression

8.
We’ve successfully calculated the ATT manually, but let’s see if we can accomplish the same task with regression. Before we begin modeling, create two indicator variables:

treat: a treatment group indicator that is 1 for the treated group and 0 for the control group.
time: a time indicator variable that is 1 for the year 2015 and 0 for 2014.

9.
Fit a linear regression model predicting LOS from treatment group, time, and an interaction term between treatment group and time. Save the model object as hospital_model. 
Print the results of the model.


10.
So how should we interpret the results of the regression model we just fit?

(Intercept): the average LOS for a patient at Hospital A (control group) in 2014 was about 4.46 days.
treat: Prior to implementation of ERAS at Hospital B, the average LOS for patients at Hospital B was about 0.44 days shorter than for patients at Hospital A.
time: The LOS for patients at Hospital A was on average 0.76 days shorter in 2015 than in 2014.
treat:time: The change in LOS for patients at Hospital B was an additional 0.80 days fewer than the change in LOS of patients at Hospital A between 2014 and 2015.
But which regression coefficient represents the ATT (the causal estimand)? Print only the coefficient that corresponds with the ATT. Does this align with the ATT you calculated manually?


# Conclusion

11.
Great job! Using both manual methods and regression, you found that the average treatment effect among the treated (ATT) for the ERAS protocol is -0.75. 
This means that use of the ERAS protocol led to a 0.75 day (or 18 hour) reduction in average hospital length of stay compared to the expected LOS had Hospital B NOT used ERAS. 
Not too shabby!
