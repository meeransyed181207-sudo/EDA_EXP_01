**#Experiment 1: EDA in IPL Dataset**
**Aim:**
To perform Exploratory Data Analysis (EDA) on the IPL matches dataset and derive insights about matches per season, winning teams, toss decisions, and top venues.

**Algorithm / Procedure:**

**1.Import Libraries**
  Import pandas for data handling.
  Import matplotlib and seaborn for visualization.
**2.Load Dataset**
  Use pd.read_csv() to load the IPL matches dataset.
  Check dataset shape using .shape.
  View first 5 rows using .head().
**3.Matches per Season (Univariate Analysis)**
  Group data by season and count matches.
  Plot a bar chart to visualize growth/decline in matches.
**4.Top Winning Teams (Univariate Analysis)**
  Use value_counts() on the winner column.
  Plot top 5 winning teams in a bar chart.
**5.Toss Decisions (Univariate Analysis)**
  Count toss decision preferences (bat vs field).
  Plot results using a bar chart.
**6.Top Venues (Univariate Analysis)**
  Count matches per venue.
  Display top 5 venues with a horizontal bar chart.
**7.Draw Insights**
  Observe patterns in toss decisions.
  Identify teams with consistent winning trends.
  
  **Program**
  ```
import pandas as pd
import matplotlib.pyplot as plt

matches = pd.read_csv("matches.csv")

print("A. Understanding the Dataset")

print("Rows and Columns:", matches.shape)
print(matches.head())
print(matches.columns)
print(matches.dtypes)
print("Unique IDs:", matches["id"].nunique())
print("Total Rows:", len(matches))

print("\nB. Data Quality and Cleaning")

print(matches.isnull().sum())
print("Duplicate Rows:", matches.duplicated().sum())

matches = matches.drop_duplicates()

matches["winner"] = matches["winner"].fillna("No Result")
matches["player_of_match"] = matches["player_of_match"].fillna("Unknown")

if "method" in matches.columns:
    matches["method"] = matches["method"].fillna("Normal")

matches["result_margin"] = matches["result_margin"].fillna(0)

print(matches.isnull().sum())

print("\nC. Matches per Season")

season_matches = matches.groupby("season")["id"].count()

print(season_matches)
print("Season with Highest Matches:", season_matches.idxmax())
print("Number of Matches:", season_matches.max())

season_matches.plot(kind="bar", figsize=(10,5))
plt.title("Matches per Season")
plt.xlabel("Season")
plt.ylabel("Matches")
plt.show()

print("\nD. Top Winning Teams")

wins = matches["winner"].value_counts()
print(wins)

top5 = wins.head(5)
print(top5)

top5.plot(kind="bar", figsize=(8,5), color="green")
plt.title("Top 5 Winning Teams")
plt.xlabel("Team")
plt.ylabel("Wins")
plt.show()

print("\nE. Chennai Super Kings Wins")

csk = matches[matches["winner"] == "Chennai Super Kings"]
print(csk)
print("Total Wins:", len(csk))

print("\nF. Toss Decision Analysis")

toss = matches["toss_decision"].value_counts()
print(toss)

toss.plot(kind="bar", color=["orange","blue"])
plt.title("Toss Decision")
plt.xlabel("Decision")
plt.ylabel("Count")
plt.show()

print("\nG. Pivot Analysis")

pivot = pd.crosstab(matches["season"], matches["toss_decision"])
print(pivot)

pivot.plot(kind="bar", figsize=(10,5))
plt.title("Season-wise Toss Decision")
plt.xlabel("Season")
plt.ylabel("Count")
plt.show()

print("\nH. Venue Analysis")

venue = matches["venue"].value_counts()
print(venue)

top5_venue = venue.head(5)
print(top5_venue)

top5_venue.plot(kind="bar", figsize=(10,5), color="purple")
plt.title("Top 5 Venues")
plt.xlabel("Venue")
plt.ylabel("Matches")
plt.show()

print("\nI. Winning Margin Analysis")

print("Largest Winning Margin:", matches["result_margin"].max())

largest = matches[matches["result_margin"] == matches["result_margin"].max()]
print(largest)

top10 = matches.sort_values(by="result_margin", ascending=False).head(10)
print(top10[["season","team1","team2","winner","result_margin"]])

print("\nJ. Match Result Analysis")

def win_type(result):
    if result == "runs":
        return "Won by Runs"
    elif result == "wickets":
        return "Won by Wickets"
    elif result == "tie":
        return "Tie"
    else:
        return "No Result"

matches["win_type"] = matches["result"].apply(win_type)

print(matches["win_type"].unique())

result_count = matches["win_type"].value_counts()
print(result_count)

result_count.plot(kind="bar", figsize=(7,5), color=["skyblue","lightgreen","orange","red"])
plt.title("Match Result Types")
plt.xlabel("Result Type")
plt.ylabel("Matches")
plt.show()

print("\nK. Basic Data Transformation")

matches["date"] = pd.to_datetime(matches["date"])

matches["year"] = matches["date"].dt.year

print(matches[["date","year"]].head())

print(matches[["result","win_type"]].head())

matches.to_csv("matches_cleaned.csv", index=False)

print("\nCleaned dataset saved successfully.")
```

  **Output**
  <img width="1920" height="1080" alt="Screenshot (58)" src="https://github.com/user-attachments/assets/dd1e871d-5ef3-4a90-9a1e-c82585ed57c4" />
<img width="1920" height="1080" alt="Screenshot (59)" src="https://github.com/user-attachments/assets/d9d2d6ab-fe69-469a-9608-0ea36d33f180" />
<img width="1920" height="1080" alt="Screenshot (60)" src="https://github.com/user-attachments/assets/2f799444-841b-458e-a23e-56d210ba389e" />
<img width="1920" height="1080" alt="Screenshot (61)" src="https://github.com/user-attachments/assets/3decd572-57d8-466e-a66b-fa3c027a1b1a" />
<img width="1920" height="1080" alt="Screenshot (62)" src="https://github.com/user-attachments/assets/3ef41fb8-1a80-43c0-8a5f-3293d9ab697f" />


 ** Result**
  This experiment is executed successfully



Highlight the stadiums hosting maximum matches.
