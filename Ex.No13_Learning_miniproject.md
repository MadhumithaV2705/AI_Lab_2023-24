# Ex.No: 10 Learning – Use Supervised Learning  
### DATE: 25.10.2025                                                                           
### REGISTER NUMBER : 212223060145

### AIM: 
To write a program to train a classifier for predicting the content type (Movie/TV Show) of Netflix titles using Supervised Learning.

###  Algorithm:
# Random Forest Classifier
1. Handle categorical features using label encoding
2. Split data into training and testing sets
3. Train Random Forest classifier
4. Predict content type and evaluate accuracy

### Program:
```
from google.colab import files
uploaded = files.upload()

import pandas as pd
df = pd.read_csv("netflix_titles.csv")
df.head()

df.info()
df.isnull().sum()
df.describe()

import matplotlib.pyplot as plt
import seaborn as sns
# 1. Distribution of Movies vs TV Shows
plt.figure(figsize=(6,4))
sns.countplot(x='type', data=df, palette='Set2')
plt.title('Distribution of Content Types')
plt.show()

# 2. Top 10 Countries with Most Content
top_countries = df['country'].value_counts().head(10)
plt.figure(figsize=(8,6))
sns.barplot(x=top_countries.index, y=top_countries.values, palette='Blues_d')
plt.xticks(rotation=45)
plt.title('Top 10 Countries with Most Content')
plt.show()

# 3. Top Genres
df['genre'] = df['listed_in'].str.split(',').str[0]  # take first listed genre
top_genres = df['genre'].value_counts().head(10)
plt.figure(figsize=(8,6))
sns.barplot(x=top_genres.index, y=top_genres.values, palette='magma')
plt.xticks(rotation=45)
plt.title('Top 10 Genres with Most Content')
plt.show()

plt.figure(figsize=(10,5))
sns.histplot(df['release_year'], bins=30, kde=False, color='skyblue')
plt.title('Content Released per Year')
plt.show()

plt.figure(figsize=(10,6))
sns.countplot(y='rating', data=df, order=df['rating'].value_counts().index)
plt.title('Distribution of Content Ratings')
plt.show()

from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import LabelEncoder
from sklearn.metrics import classification_report, accuracy_score
df['country'] = df['country'].fillna('Unknown')
le_country = LabelEncoder()
df['country_enc'] = le_country.fit_transform(df['country'])
X = df[['release_year', 'country_enc']]
y = df['type'].map({'Movie':0, 'TV Show':1})  # encode target
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
print("Accuracy:", accuracy_score(y_test, y_pred))
print("\nClassification Report:\n", classification_report(y_test, y_pred))
```

### Output:


### Result:
Thus, the system was trained successfully on the Netflix dataset, and the prediction of content type (Movie/TV Show) was carried out with good accuracy.
