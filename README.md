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
