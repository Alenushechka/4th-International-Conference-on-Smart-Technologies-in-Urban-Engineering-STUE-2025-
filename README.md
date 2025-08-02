#рисунок 3 Potential Ecological Risk Index (PERI) for Soil Samples
import matplotlib.pyplot as plt
import pandas as pd
from matplotlib.patches import Patch

# Дані PERI для проб (розраховані за вашими виміряними концентраціями)
data = {
    "Sample": [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
    "PERI": [152.30, 197.49, 132.49, 219.62, 175.71, 135.32, 99.79, 275.29, 125.36, 130.36, 154.84, 175.10]
}

df = pd.DataFrame(data)

# Градація Hakanson для кольорів
colors = []
for peri in df["PERI"]:
    if peri < 40:
        colors.append("#a1d99b")  # Low
    elif peri < 80:
        colors.append("#41ab5d")  # Moderate
    elif peri < 160:
        colors.append("#fdae6b")  # Considerable
    elif peri < 320:
        colors.append("#e6550d")  # High
    else:
        colors.append("#a50f15")  # Very High

# Побудова графіку
plt.figure(figsize=(12, 7))
bars = plt.bar(df["Sample"], df["PERI"], color=colors, edgecolor='black')

# Значення над стовпцями
for bar in bars:
    yval = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2, yval + 2, round(yval, 1),
             ha='center', va='bottom', fontsize=10)

# Легенда
legend_elements = [
    Patch(facecolor="#a1d99b", label="Low (<40)"),
    Patch(facecolor="#41ab5d", label="Moderate (40–80)"),
    Patch(facecolor="#fdae6b", label="Considerable (80–160)"),
    Patch(facecolor="#e6550d", label="High (160–320)"),
    Patch(facecolor="#a50f15", label="Very High (>320)")
]

plt.legend(handles=legend_elements, title="Hakanson PERI scale", fontsize=10, title_fontsize=12, loc="upper right")

# Оформлення
plt.title("Potential Ecological Risk Index (PERI) for Soil Samples", fontsize=16)
plt.xlabel("Sample Number", fontsize=14)
plt.ylabel("PERI Value", fontsize=14)
plt.xticks(df["Sample"])
plt.ylim(0, max(df["PERI"]) + 50)

plt.tight_layout()
plt.show()
