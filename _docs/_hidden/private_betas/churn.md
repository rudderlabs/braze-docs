---
nav_title: Predictive Churn
title: Predictive Churn
description: "This tutorial page covers the benefits of Predictive Churn, why you should be using it, and how to get it set up."
hidden: true
---

# Predictive Churn
> Customer Churn, also known as customer turnover or client loss, is one of the most important metrics for growing businesses to consider. Having the right tools to address churn is crucial in minimizing loss and maximizing customer retention. To get a jump on these potentially churning users, Braze offers Predictive Churn, providing a proactive approach toward minimizing future churn.

![Churn Overview][3]

With Predictive Churn, you can define what churn means for your business ([Churn Definition](#step-2-define-churn)) as well as the users you'd like to prevent from churning ([Prediction Audience](#step-3-choose-the-users-you-want-to-keep-from-churning)). When you build the Prediction, Braze will train a machine learning model to predict churn by comparing the behaviors of users in the historical Prediction Audience who did or did not churn according to your definition. 

Once the Prediction model is built and done training, users that currently fit the definition of the Prediction Audience will be assigned a Churn Risk Score between 0 and 100 denoting how likely they are to Churn according to your definition. The higher the score, the more likely a user is to churn. 

Updating the risk scores of the Prediction Audience can be done with a [frequency you choose](#step-4-choose-the-update-frequency-for-churn-predictions). This way, you can reach out to users who are at risk of Churning before they actually do and prevent it from happening in the first place.

## Step 1: Create a New Prediction
On the left navigation bar of the Braze dashboard, choose the Predictions page.  A Prediction is one instance of a trained machine learning model and all the parameters and data it uses. On this page, you will see a list of current active Predictions along with some basic info about them. Here you can rename, archive, and create new Predictions. Archived predictions are inactive and do not update user scores. 

To create a new Prediction, choose “Create Prediction” in the upper right corner, and select a new “Churn Prediction.”

{% alert note %}
There is a limit of 3 concurrently active Churn Predictions.
{% endalert %}

On the Edit page, give your new Prediction a unique name.

## Step 2: Define Churn
In the Churn Definition panel, use the provided filters to define what churn means for your business. In other words, what does a user have to do in what time frame for you to consider them churned? Remember, you don’t need to explain what behaviors might precede churn-- only what makes a user a churned user. This should also generally be a description of what behavior a user does or doesn't do to churn as opposed to an attribute a user has.     For example, you might consider users who haven’t opened your app in 7 days to be churned. 

To implement this example, enter 7 days in the time window at the top of the panel.

![Churn 1][1]

Then, use the available filters to select which behaviors in that time frame constitute churn. For this case, select "do not" and "start a session". You can combine other filters with "and" and "or" as you see fit to create the definition you need. Uninstalling, making or not making purchases, or performing or not performing particular custom events are other filters you can include.

Interested in some potential churn definitions to consider? You’ll find some inspiration at the [bottom of this page](#sample-definitions).

## Step 3: Choose the Users you Want to Keep from Churning
Although you can try to prevent churn as defined above in your entire population of users, the model will likely perform better if you narrow down the group of users you want to prevent from churning with some criteria. Think about the specific users who mean the most to you that you’d like to retain and define them here. For example, you might want to retain users who first used the app more than a month ago or have ever made a purchase. 

{% alert note %}
The Prediction Audience cannot exceed 40 million users.
{% endalert %}

For filters that begin with “Last...” like Last Used App and Last Made Purchase, the time window to look back for these filters cannot exceed 30 days minus the number of days of the window specified in the Churn Definition. For example, if your Churn definition has a window of 14 days, the time window for the “Last...” filters cannot exceed 30 - 14 = 16 days.

For a sample list of Prediction Audience definitions, check out the [bottom of the page](#sample-definitions)! 

## Step 4: Choose the Update Frequency for Churn Predictions

The machine learning model created when you complete this page will be used on a schedule you select here to generate fresh scores of users’ probability to churn. Please select the maximum frequency of updates that you’ll find useful. For example, if you’re going to send a weekly promotion to prevent users from churning, set the update frequency to Weekly on the day and time of your choosing.

![Churn 2][2]

## Step 5: Build Prediction
Verify that the details you’ve provided are correct, and choose “Build Prediction.” You can also save your changes in draft form by selecting “Save As Draft” to return to this page and build the model later. Once you click Build Prediction, the process that generates the model will begin. This could take between 30 minutes to a few hours, depending on data volumes. For this Prediction, you will see a page explaining that training is in progress for the duration of the model building process.

Once it’s done, the page will switch to the Analytics view automatically, and you will also get an e-mail informing you that the Prediction and results are ready. In the event of an error, the page will return to the Editing mode with an explanation of what went wrong.

The Prediction will be rebuilt ("retrained") again every two weeks automatically to keep it updated on the most recent data available. Note that this is a separate process from when users' Churn Risk Scores, the output of the Prediction, are produced. The latter is determined by the update frequency you chose in Step 4.

# Performance & Targeting

![Churn Targeting][4]


## Prediction Quality
In order to measure the accuracy of your model, the Prediction Quality metric will show you how effective this particular machine learning model appears to be when tested on historical data. Braze pulls data according to the groups you specified in the model creation page. The model is trained on one data set (the “training” set) and then tested on a new, separate data set (the “test” set). 

Our measure of Prediction Quality is [Lift Quality](https://dl.acm.org/doi/10.1145/380995.381018). You are probably familiar with "lift", which often measures the increase, as a ratio or percentage, of some successful outcome like a conversion. In this case, the successful outcome is correctly identifying a user who would have churned. Lift Quality is the average lift the Prediction provides across all possible audience sizes for messaging the test set. This approach measures how much better than random guessing the model is. With this measure, 0% means the model is no better than randomly guessing about who will churn, and 100% indicates perfect knowledge of who will churn.

Here’s what we recommend for various different ranges of Prediction Quality:

| Prediction Quality Range (%) | Recommendation |
| ---------------------- | -------------- |
| 60 - 100 | Excellent. Top tier accuracy. Changing the audience definitions is unlikely to provide additional benefit. |
| 40 - 60 | Good. This model will produce accurate predictions, but trying different audience settings may achieve even better results. |
| 20 - 40| Fair. This model can provide accuracy and value, but consider trying different audience definitions to see if they increase performance. |
| 0 - 20 | Poor. We recommend you change your audience definitions and try again. |
{: .reset-td-br-1 .reset-td-br-2}

The Prediction will be trained again every two weeks to keep it updated on the most recent user behavior patterns. This is also when the Prediction Quality metric will be updated. The last time this occurred for a Prediction will be displayed on the Predictions list page as well as on an individual Prediction's analytics page.


>Prediction Quality Details <br><br> Example: If 20% of your users usually churn on average, and you pick a random subset of 20% of your users and label them as churned at random (whether they truly are or not), you’d expect to correctly identify only 20% of the actual churners. That's random guessing. If the model were to only do that well, the lift would be 1 for this case.<br> If the model, on the other hand, allowed you to message 20% of the users and, in doing so capture all the “true” churners and no one else, the lift would be 100% / 20% = 5. If you chart this ratio for every proportion of the likeliest churners you could message, you get the [Lift Curve](https://towardsdatascience.com/the-lift-curve-unveiled-998851147871). <br><br>Another way to think of Lift Quality (and also Prediciton Quality) is how far along the way between random guessing (0%) and perfection (100%) the Prediction's lift curve is at identifying churners on the test set. For the original paper on Lift Quality see [here](https://dl.acm.org/doi/10.1145/380995.381018).

## Churn Score and Category

Users in the Prediction Audience will be assigned a Churn Score between 0 and 100. The higher the score, the greater the likelihood of Churn. Users with Churn Scores between 0 and 50 will be labeled in the Low Churn Risk category. Users with scores between 50 and 75, and 75 and 100 will be labeled as the Medium and High Churn Risk categories, respectively. The scores and the corresponding categories will be updated according to the schedule you chose in the model creation page. The number of users with Churn Scores in each of 20 equally sized buckets is displayed in the chart at the top of the page. This can help you determine what the churn risk looks like across the population according to this Prediction.

## Targeting Users

The Prediction analytics page lets you decide what users you should target based on their Churn Risk Score or Category. As soon as the Prediction is done training and this page is populated, you can jump to simply using [Filters](#filters) in Segments or Campaigns to begin using the outputs of the model. But, if you want help deciding who to target and why, this page can help based on the historical accuracy of the model and your own business goals. 

The distribution of the scores for the entire Prediction Audience is displayed at the top of the page in a chart that you can view, by category, or by score. Users in bins further to the right have higher scores and are more likely to churn. Users in bins further to the left are less likely to churn. The slider beneath the chart will allow you to select a swath of users and estimate what the results would be of targeting users in the selected range of Churn Risk Score or Category.

As you move the slider, the bar in the left half of the lower panel will inform you how many users out of the entire Prediction Audience would be targeted.

### Estimated Results

![Estimated Results][6]

In the right half of the panel beneath the chart, we show estimates of the expected accuracy of targeting this swath of the Prediction Audience. Based on data about users in the Prediction Audience in the past, and the apparent accuracy for the model for discriminating between churning and non-churning users on that past data, these progress bars estimate for a future potential message using the audience highlighted with the slider:

1. An estimate of how many actual churners will be correctly targeted

Of course, we don't know the future perfectly, so we don't know precisely which users from the Prediction Audience will churn in the future. But the Prediction is a reliable inference. Based on past performance, this progress bar indicates how many of the total "actual" or "true" churners expected in the Prediction Audience (based on prior churn rates) will be targeted with the current targeting selection. We would expect this number of users to churn if you do not target them with any extra or unusual messaging. 

2. An estimate of how many users who wouldn't have actually churned will be incorrectly targeted

All machine learning models make errors. There may be users in your selection who have a high Churn Risk Score but do not end up churning. They would not churn even if you take no action. They will be targeted anyway, so this is an error or "false positive." The full width of this second progress bar represents the expected number of users who will not churn, and the red portion is those who will be incorrectly targeted using the current slider position.

Using this information, we encourage you to decide how many of the churners you want to capture, and what the cost of a false positive error is for your business. If you are sending out a valuable promo, you may want to keep non-churners targeted to a minimum while getting as many expected true churners as the model will allow. Or, if you're less sensitive to false positives and users receive extra messaging, you can message more of the audience to capture more expected churners and ignore the likely errors.

### Filters {#filters}

Once you've decided what range of Churn Risk Score or Category you want to target, you can use the "Create Segment" or "Create Campaign" buttons below the targeting sentences to create a new segment or campaign that filters for users with the Churn Risk Score or Category selected with the slider.

![Churn Filters][5]

You can also use filters in campaigns or segments to target the users according to that threshold. You can filter for users by Churn Score or Churn Category in Campaigns, Canvas, and Segments, just like you use any other filter in Braze.

## Churn Correlation Table

This analysis displays any user attributes or behaviors that are correlated with user churn in the historical Prediction Audience. The tables are split into left and right for more and less likely to churn, respectively. For each row, the ratio by which the users with the behavior or attribute in the left column are more or less likely to churn is displayed in the right column. This number is the ratio of churn likelihood of users with this behavior or attribute divided by the likelihood to churn off the entire Prediction Audience.

This table is updated only when the Prediction retrains and not when user Churn Risk Scores are updated.

## Archived Predictions

Archived Predictions will cease updating user scores. Any archived Prediction that is unarchived will continue updating user scores on its predetermined schedule. Archived Predictions are never deleted and remain in the list.

## What To Do Next? {#what-do-next}

Now that you’ve identified and selected the group of users at risk of churn that you feel require some incentives or a new messaging series to keep ‘em active and engaged, what do you do? Do you just add them proactively to your current passive user series? Or do you build out a brand new series of Canvases and Campaigns? Here are a few ideas to consider:

- Target your predicted medium-to-high-risk users with a special discount, free merchandise (physical gift or digital credits), exclusive content, or early access to a new experience (product, app feature, level).
- You could drop these users into a daily Canvas for a week, delivering messages on the channel they prefer most, do a concentrated blast for three days, reaching customers on every channel, from email to Facebook, or Send a message from a real person, asking for brand feedback or offering a pro tip.
- Maybe you just need a new, fun way to reiterate the value of your brand, and all the ways these customers have found value in yours before. This could look like a persona-specific weekly newsletter, a series of real stories from real users about your brand, or some other content marketing play.

Keep in mind that you can message different levels of at-risk users differently! So the highest-risk customers could get higher discounts than the medium-risk customers, while the lowest-risk customers simply get new kinds of messaging or content but no larger incentive. You can also layer other filters into these segments, to further qualify who gets what offers, messages, etc.

### Sample Churn and Prediction Audience Definitions {#sample-definitions}

- “Within 7 days, did custom event ‘Subscription Cancellation’”
- “Within 14 days, did custom event ‘Trial Expired’”
- “Within 1 day did uninstall.” 
- “Within 14 days did not Make a Purchase.” 

For the Churn definitions we outlined above, there might be some corresponding Prediction Audience definitions:
- Started subscription more than 2 weeks ago OR Started subscription less than two weeks ago. You might want to create 2 predictions in this case and then message new subscribers differently than longer-term subscribers. You could also define this as “First Made Purchase more than 30 days ago.”
- For uninstallers, you might focus on customers who have purchased something in the recent past or used the app very recently.
- For those at risk of not purchasing as a definition of churn, you may want to focus on customers who have been browsing or searching or engaging with your app more recently. Perhaps the right discount intervention will prevent this more engaged group from churning.

[1]: {% image_buster /assets/img/churn/churn1.png %}
[2]: {% image_buster /assets/img/churn/churn2.png %}
[3]: {% image_buster /assets/img/churn/churn_overview.png %}
[4]: {% image_buster /assets/img/churn/churnTargeting.gif %}
[5]: {% image_buster /assets/img/churn/churnFilters.png %}
[6]: {% image_buster /assets/img/churn/churnEstimatedResults.png %}

