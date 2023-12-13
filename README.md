# Data_wrangling_OneCampus_Academy
This is how I have preprocessed my data to get valuable insights.


Challenge! 
 The Muskets Football team is preparing for the next games season and have asked you to help clean 
and preprocess their data and hopefully help predict number of hits by each player 
TASK: 
1. Conduct a full range cleaning of the data. Provide explanations and justifications for any actions 
you take. 
2. Preprocess the cleaned data from task 1 above and transform it into a well behaved data. 
3. Select input features for an outcome feature of HITS. 
Sub Tasks 
1. Extract the player names from the PlayerUrl column and create a new column name Player 
Name from the extracts 
2. Create a new column titled Player Status from the CONTRACT column with 3 labels ; 
a. 'Active' If the player has an active contract 
b. 'Free', if the player is free 
c. 'On Loan' if the player is on loan 
3. Unpack the POSITIONS column into as many columns as there are positions and assign Boolean 
values in the columns for each player as appropriate. Name the columns the play position 
4. Weight and Height, W/F, SM and IR Columns: convert to integers 
5. Value, Wage and Release Clause columns: convert to Float 
6. Inspect the HITS column and ensure its float 
7. Create 5 new categorical columns for the Height, Weight, Release Clause, Value and Wage into 
which you convert the respective values into clusters/labels as follows 
a. Height: Bucket intervals of 10 years 
b. Weight: Bucket intervals of 10 kg 
c. Wage: bucket intervals of 50K 
d. Value: bucket intervals of 50M 
e. Release Clause: bucket intervals of 50M


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Muskets Football Team Data Cleaning and Preprocessing</title>
</head>
<body>

<h1>Muskets Football Team Data Cleaning and Preprocessing</h1>

<p>The Muskets Football team is preparing for the next games season and have asked for assistance in cleaning and preprocessing their player data to predict the number of hits by each player.</p>

<h2>Task 1: Data Cleaning</h2>

<h3>1. Extract Player Names</h3>
<pre><code>df['Player Name'] = df['PlayerUrl'].str.extract(r'/([^/]+)$');</code></pre>

<h3>2. Create Player Status Column</h3>
<pre><code>df['Player Status'] = df['CONTRACT'].apply(lambda x: 'Active' if 'active' in x.lower() else ('Free' if 'free' in x.lower() else 'On Loan'));</code></pre>

<h3>3. Unpack Positions Column</h3>
<pre><code>positions = df['POSITIONS'].str.get_dummies(',')
df = pd.concat([df, positions], axis=1);</code></pre>

<h3>4. Convert Columns to Integers or Floats</h3>
<pre><code>df[['Weight', 'Height', 'W/F', 'SM', 'IR']] = df[['Weight', 'Height', 'W/F', 'SM', 'IR']].astype(int)
df[['Value', 'Wage', 'Release Clause']] = df[['Value', 'Wage', 'Release Clause']].astype(float)
df['HITS'] = df['HITS'].astype(float);</code></pre>

<h2>Task 2: Data Preprocessing</h2>

<h3>1. Categorize Columns into Clusters/Labels</h3>
<pre><code>df['Height Category'] = pd.cut(df['Height'], bins=range(140, 211, 10), labels=range(140, 210, 10))
df['Weight Category'] = pd.cut(df['Weight'], bins=range(50, 111, 10), labels=range(50, 110, 10))
df['Wage Category'] = pd.cut(df['Wage'], bins=range(0, 500, 50), labels=range(0, 450, 50))
df['Value Category'] = pd.cut(df['Value'], bins=range(0, 500, 50), labels=range(0, 450, 50))
df['Release Clause Category'] = pd.cut(df['Release Clause'], bins=range(0, 500, 50), labels=range(0, 450, 50));</code></pre>

</body>
</html>
