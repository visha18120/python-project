# python-project
The IPL Data Analysis Python Project involves analyzing Indian Premier League cricket data to uncover insights about teams, players, and match performance. The dataset includes match results, player statistics, scores, venues, and more. Using Python, the project performs data cleaning
matches.csv
The Indian Premier League (IPL) is one of the most popular and competitive T20 cricket leagues in the world, attracting top players from across the globe and generating massive fan engagement, sponsorships, and data. With over a decade of matches, the IPL has created a large volume of data related to player performances, team strategies, match outcomes, and more.

This project, IPL Data Analysis using Python, aims to explore and analyze historical IPL data using data science techniques to derive meaningful insights. By leveraging Python's powerful data analysis libraries such as Pandas, NumPy, Matplotlib, and Seaborn, we will uncover trends and patterns that are not immediately obvious from raw statistics.

The project uses two main datasets:

matches.csv: Contains match-level information such as date, venue, participating teams, toss winner, match winner, and more.

deliveries.csv: Contains ball-by-ball data from every match, including information about runs scored, batsmen, bowlers, dismissals, and extras.

Through this analysis, we seek to answer key questions such as:

Which teams and players have been most successful?

How does the toss decision influence match outcomes?

What are the scoring trends across seasons and venues?

Which players have dominated in terms of runs and wickets?

Are there any patterns in dismissals or match-winning strategies?

This project combines descriptive statistics, data cleaning, visualizations, and exploratory data analysis (EDA) to present a clear picture of IPL dynamics. The final result will be a collection of insights and charts that tell the story of the IPL from a data-driven perspective, providing value for fans, analysts, and cricket strategists alike.

By the end of this project, we will have a solid understanding of how data science can be applied in sports analytics, particularly cricket, and how to extract actionable insights from real-world datasets.

pip install pandas matplotlib seaborn
# Import necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Set visual style
sns.set(style="whitegrid")

# Load the dataset
df = pd.read_csv("matches.csv")

# Display the first few rows
print("Data Preview:")
display(df.head())

# -------------------------
# BASIC DATA OVERVIEW
# -------------------------
print("\nBasic Information:")
print(df.info())

print("\nSummary Statistics:")
print(df.describe())

print("\nMissing Values:")
print(df.isnull().sum())

# -------------------------
# ANALYSIS 1: Number of Matches by Season
# -------------------------
season_matches = df['season'].value_counts().sort_index()
plt.figure(figsize=(10,5))
sns.barplot(x=season_matches.index, y=season_matches.values, palette="Blues_d")
plt.title("Total Matches Played per Season")
plt.xlabel("Season")
plt.ylabel("Number of Matches")
plt.show()

# -------------------------
# ANALYSIS 2: Most Successful Teams
# -------------------------
team_wins = df['winner'].value_counts()
plt.figure(figsize=(10,6))
sns.barplot(y=team_wins.index, x=team_wins.values, palette="viridis")
plt.title("Most Successful Teams in IPL History")
plt.xlabel("Wins")
plt.ylabel("Team")
plt.show()

# -------------------------
# ANALYSIS 3: Most Player of the Match Awards
# -------------------------
top_players = df['player_of_match'].value_counts().head(10)
plt.figure(figsize=(10,5))
sns.barplot(x=top_players.values, y=top_players.index, palette="Set2")
plt.title("Top 10 Players with Most 'Player of the Match' Awards")
plt.xlabel("Number of Awards")
plt.ylabel("Player")
plt.show()

# -------------------------
# ANALYSIS 4: Toss Decision Impact
# -------------------------
toss_decisions = df['toss_decision'].value_counts()
plt.figure(figsize=(6,4))
toss_decisions.plot(kind="pie", autopct="%1.1f%%", colors=["#66b3ff", "#99ff99"])
plt.title("Toss Decisions: Bat or Field?")
plt.ylabel("")
plt.show()

# -------------------------
# ANALYSIS 5: Toss Winner vs Match Winner
# -------------------------
df['toss_match_win'] = df['toss_winner'] == df['winner']
toss_match_win_rate = df['toss_match_win'].value_counts(normalize=True)[True] * 100
print(f"\nPercentage of times toss winner also won the match: {toss_match_win_rate:.2f}%")

# -------------------------
# ANALYSIS 6: Venue Analysis
# -------------------------
venue_counts = df['venue'].value_counts().head(10)
plt.figure(figsize=(10,5))
sns.barplot(x=venue_counts.values, y=venue_counts.index, palette="coolwarm")
plt.title("Top 10 Venues with Most Matches")
plt.xlabel("Number of Matches")
plt.ylabel("Venue")
plt.show()

# -------------------------
# ANALYSIS 7: Season Winners
# -------------------------
season_winners = df.drop_duplicates('season', keep='last')[['season', 'winner']]
print("\nSeason Winners:
