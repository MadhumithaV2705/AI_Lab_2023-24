# Ex.No: 13 Machine Learning  
### DATE: 25.10.2025                                                                           
### REGISTER NUMBER : 212223060145

### Aim: 
To write a program to train a classifier for predicting the content type (Movie/TV Show) of Netflix titles using Supervised Learning.

###  Algorithm:
### Random Forest Classifier
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
<img width="549" height="393" alt="image" src="https://github.com/user-attachments/assets/920e1548-a715-4307-b77f-68e37488544d" />
<img width="684" height="622" alt="image" src="https://github.com/user-attachments/assets/f70d07d7-bd8a-4b25-816f-1bd17a38355f" />
<img width="693" height="667" alt="image" src="https://github.com/user-attachments/assets/608e6327-963a-4bcb-bbb3-62cccd508aff" />
<img width="859" height="470" alt="image" src="https://github.com/user-attachments/assets/842eada3-0f81-493c-845f-d3c55ea111d2" />
<img width="884" height="547" alt="image" src="https://github.com/user-attachments/assets/8aba3682-c16d-4672-bce9-4b84b09e1fac" />
<img width="662" height="267" alt="image" src="https://github.com/user-attachments/assets/9247dd8f-88f6-42c8-9567-f210e26f743d" />

### Result:
Thus, the system was trained successfully on the Netflix dataset, and the prediction of content type (Movie/TV Show) was carried out with good accuracy.
