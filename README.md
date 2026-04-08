# Data_Analytics_Python_App_Rating_Project

## Objective: Make a model to predict the app rating, with other information about the app provided.
## Analysis to be done: The problem is to identify the apps that are going to be good for Google to promote. App ratings, which are provided by the customers, is always a great indicator of the goodness of the app. 
The problem reduces to: predict which apps will have high ratings.
Content: Dataset: Google Play Store data (“googleplaystore.csv”)

## Fields in the data –
*	App: Application name
*	Category: Category to which the app belongs 
*	Rating: Overall user rating of the app
*	Reviews: Number of user reviews for the app
*	Size: Size of the app
*	Installs: Number of user downloads/installs for the app
*	Type: Paid or Free
*	Price: Price of the app
*	Content Rating: Age group the app is targeted at - Children / Mature 21+ / Adult
*	Genres: An app can belong to multiple genres (apart from its main category). For example, a musical family game will belong to Music, Game, Family genres.
*	Last Updated: Date when the app was last updated on Play Store
* Current Ver: Current version of the app available on Play Store
*	Android Ver: Minimum required Android version
  
## Library used:
* Numpy
* Pandas
* Matplotlib.pyplot
* Seaborn
* Plotly.express
* Sklearn.model_selection
* Sklearn.linear_model
* Sklearn.mectrics

  
## Steps to perform:
1.	Load the data file using pandas.
 ![step1](https://github.com/user-attachments/assets/31af249a-67d0-4bf9-a866-8b0db8e1ee08)
2.	Check for null values in the data. Get the number of null values for each column.
![Step2](https://github.com/user-attachments/assets/f2f810a8-aa1c-4e40-9742-167a4ab49d22)
3.	Drop records with nulls in any of the columns. 
![Step3](https://github.com/user-attachments/assets/0bf52563-ddf9-4e66-9ed0-389e9931bcd7)
4.	Variables seem to have incorrect type and inconsistent formatting. You need to fix them:
	* Before formating
	![Step4](https://github.com/user-attachments/assets/839b3b7b-9407-4c2e-b4c8-d9c576b3c2c3)

 *	Size column has sizes in Kb as well as Mb. To analyze, you’ll need to convert these to numeric.
    *	Extract the numeric value from the column
    *	Multiply the value by 1,000, if size is mentioned in Mb
![Step41](https://github.com/user-attachments/assets/c586c6e0-2b8e-4451-904f-82729b751b06)
*	Reviews is a numeric field that is loaded as a string field. Convert it to numeric (int/float).
![step42](https://github.com/user-attachments/assets/8771100c-9410-4107-8564-ada5509ec40e)
*	Installs field is currently stored as string and has values like 1,000,000+. 
  * Treat 1,000,000+ as 1,000,000
  *	remove ‘+’, ‘,’ from the field, convert  it to integer
 ![Step43](https://github.com/user-attachments/assets/dc5428ba-773c-45ce-ae77-08cc985d8ddb)
*	Price field is a string and has $ symbol. Remove ‘$’ sign, and convert it to numeric.
![step44](https://github.com/user-attachments/assets/5af5535f-135b-42df-94b6-fbd18620c321)

* After formating
  
 ![Step442](https://github.com/user-attachments/assets/85b55005-129f-47bb-87da-41077b95c062)

 5. Sanity checks:
*	Average rating should be between 1 and 5 as only these values are allowed on the play store. Drop the rows that have a value outside this range.
*	Reviews should not be more than installs as only those who installed can review the app. If there are any such records, drop them.
*	For free apps (type = “Free”), the price should not be >0. Drop any such rows.

![Step5](https://github.com/user-attachments/assets/c797cdb2-963d-4353-87bc-0e5ebc2829a8)

6.Box plot on Price(to check for any high priced app) and Review (to find the range)
![step52](https://github.com/user-attachments/assets/61963721-8c67-4610-9502-445d59d607cc)
![step61](https://github.com/user-attachments/assets/ea4d8cf2-285b-422f-90de-5b30ddfdff80)

7. Histogram for Rating(rating distributed and is it more towards the higher rating) and Size
![step71](https://github.com/user-attachments/assets/12aa8e70-6e55-4c9b-a8a5-423f9fba1abf)

![step72](https://github.com/user-attachments/assets/65726867-9fce-44f3-93b5-3b13a4082a97)

8.  Scatter plots (for numeric features) and box plots (for character features) to assess the relations between rating and the other features.
   * Scatter plot for Rating vs Price. Based on the scatter plot Rating increases with Price
  ![Step81](https://github.com/user-attachments/assets/33dc43d6-8236-424d-b4d6-9ef9dc6309f5)

 * Scatter plot for Rating vs Size. Based on the scatter plot Rating increases with ther app Size
   ![step92](https://github.com/user-attachments/assets/0953a224-7380-45c1-8a29-fec7c11f03ad)

* Scatter plot for Rating and Reviews. Based on the scatter plot more review means better rating.
![step93](https://github.com/user-attachments/assets/1e7529ff-d72b-44d1-a62d-eb28451fb9e3)

 * boxplot for Ratings and Category to find Which genre has the best ratings
![step94](https://github.com/user-attachments/assets/a837788e-c9c1-4eb5-b18e-f7e5ec98f7e9)

9. Train test split  and apply 70-30 split. Separate the dataframes into X_train, y_train, X_test, and y_test. Use linear regression as the technique.
	Report the R2 on the train set

![step10](https://github.com/user-attachments/assets/e5e131c9-573a-43bf-9600-748ba19d6ad9)
![step11](https://github.com/user-attachments/assets/d8077a1a-5808-468f-92ee-4532d76503dd)

Findings:
* Mean Absolute error- On average, predictions are off by about 0.32 rating points, since rating ranges from 1 to 5 this is relatively small error.
* Mean squared error- indicates low to moderate error.
* Rsquare score-  Model explains only 15.56% of the variance in ratings,very low explantory power and most variation on rating is noe captured.
* low r2 indicates features do not strongly influence ratings, they may depend on unobserved factores like UX,quality, user preception and so on.
 ### The model achieved an R² score of 0.1556, indicating that it explains only about 15.56% of the variance in app ratings. Although the MAE is relatively low at 0.3185, suggesting predictions are close to actual values, the low R² highlights that the model fails to capture the underlying factors influencing ratings. This suggests that ratings are influenced by variables not included in the model, and that linear regression may not be sufficient for accurate prediction.
