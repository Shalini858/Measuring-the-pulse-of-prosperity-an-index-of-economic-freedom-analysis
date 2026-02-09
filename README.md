Python
Copy code
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv("economic_freedom.csv")

# Preview data
print(df.head())

# Basic descriptive statistics
print("\nSummary Statistics:")
print(df[['Overall_Score', 'GDP_Per_Capita']].describe())

# Categorize economic freedom levels
def freedom_category(score):
    if score >= 80:
        return "Free"
    elif score >= 70:
        return "Mostly Free"
    elif score >= 60:
        return "Moderately Free"
    elif score >= 50:
        return "Mostly Unfree"
    else:
        return "Repressed"

df['Freedom_Category'] = df['Overall_Score'].apply(freedom_category)

# Count countries in each category
category_counts = df['Freedom_Category'].value_counts()
print("\nFreedom Category Distribution:")
print(category_counts)

# Correlation between freedom and prosperity
correlation = df['Overall_Score'].corr(df['GDP_Per_Capita'])
print(f"\nCorrelation between Economic Freedom and GDP per Capita: {correlation:.3f}")

# Visualization: Freedom vs Prosperity
plt.figure(figsize=(8, 5))
sns.regplot(
    x='Overall_Score',
    y='GDP_Per_Capita',
    data=df,
    scatter_kws={'alpha': 0.6}
)
plt.title("Economic Freedom vs Prosperity")
plt.xlabel("Index of Economic Freedom Score")
plt.ylabel("GDP per Capita")
plt.tight_layout()
plt.show()
