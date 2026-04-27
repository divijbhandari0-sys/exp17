Name - Divij Bhandari
Aim: To study and implement Basic Charts and Visual Encoding using Python.

THEORY

Introduction to Data Visualization
Data visualization is the graphical representation of data and information using visual elements such as lines, bars, scatter points, and histograms. By transforming raw numbers into visual form, patterns, trends, correlations, and outliers become immediately apparent in ways that tables of numbers cannot convey. Visualization is an essential step in both exploratory data analysis (EDA — understanding the data) and in communication (presenting findings to an audience).

Python provides two primary libraries for data visualization:

Matplotlib: The foundational, low-level plotting library for Python. It provides complete programmatic control over every element of a figure — axes, labels, colors, line styles, markers, and layout. It is built around the pyplot sub-module and can produce static, animated, and interactive figures.

Seaborn: A statistical data visualization library built on top of Matplotlib. It provides a higher-level interface that produces polished, statistically informative plots with significantly less code. It integrates natively with Pandas DataFrames.

Both libraries are imported with standard aliases: import matplotlib.pyplot as plt import seaborn as sns import pandas as pd

Dataset Creation
Create a 5-row DataFrame. The relationship between Study_Hours and Marks is used to demonstrate how scatter plots reveal correlations. The Days column serves as the x-axis for line and bar charts, acting as a categorical time axis.

Basic Line Chart — plt.plot()
A line chart connects data points with straight line segments, showing how a value changes across categories or time. It is the standard chart type for trend visualization.

Function and parameter breakdown:

plt.plot(x, y): The core Matplotlib plotting command. x and y are the data for the horizontal and vertical axes respectively. They can be Pandas Series, NumPy arrays, or Python lists.
marker='*': Places a star-shaped marker at each data point. Other marker options include 'o' (circle), 's' (square), '^' (triangle up), 'D' (diamond), '+' (plus), and '' (empty string — no marker, just the line).
plt.title('Pranav'): Adds a title string at the top of the plot.
plt.xlabel('Days'): Labels the x-axis.
plt.ylabel('Study Hours'): Labels the y-axis.
plt.show(): Renders and displays the completed figure. Without this call, the figure is buffered but not rendered to the screen (in script mode; Jupyter/Colab auto-displays).
A second variant with color specified: plt.plot(df['Days'], df['Study_Hours'], marker='*', color='black') plt.title('Pranav') plt.xlabel('Days') plt.ylabel('Study Hours') plt.show()

The color parameter sets the line and marker color. Accepted values include named colors ('black', 'red', 'blue', 'green'), short codes ('k', 'r', 'b', 'g'), and hex codes like '#FF5733'.

A variant with no markers: plt.plot(df['Days'], df['Study_Hours'], marker='') plt.title('Pranav') plt.xlabel('Days') plt.ylabel('Study Hours') plt.show()

Setting marker='' produces a clean line with no markers at data points, useful when the data is dense and markers would create visual clutter.

The same chart structure was applied to the Student-Dataset: plt.plot(df['Gender'], df['Department'], marker='') plt.plot(df['Gender'], df['CGPA'], marker='', color='black')

Advanced Multi-Line Chart — plt.figure() and plt.legend()
Multiple data series can be plotted on the same axes by calling plt.plot() multiple times before plt.show(). A legend distinguishes the series.

Function and parameter breakdown:

plt.figure(figsize=(7, 4)): Creates a new figure with specified dimensions in inches (width=7, height=4). Without this call, Matplotlib uses the default figure size. This is important for controlling the aspect ratio and output image resolution.
marker='o': Circle marker at each data point.
marker='s': Square marker at each data point.
label='Study Hours': Assigns a text label to this line for use in the legend.
label='Marks': Assigns a text label to the second line.
plt.legend(): Displays a legend box in the figure, automatically populated with the label strings defined in each plt.plot() call. Matplotlib places the legend in the "best" position by default to minimize overlap with the data.
Bar Chart — plt.bar()
A bar chart represents discrete categorical data with rectangular bars whose heights are proportional to the values they represent. It is used to compare quantities across categories.

Function and parameter breakdown:

plt.bar(x, height): x is the categorical labels for each bar; height is the numerical value for each bar's height.
color='green': Sets the fill color of all bars. Each bar can have a different color by passing a list: color=['red','blue','green','orange','purple'].
The same structure was applied to the Student-Dataset: plt.bar(df['Gender'], df['CGPA'], color='green') plt.bar(df['Department'], df['CGPA'], color='red')

Bar Chart with Value Labels — plt.text() and b.get_height()
A more informative variant of the bar chart displays the exact numerical value above each bar, making precise comparisons easier.

Detailed explanation:

bar = plt.bar(...): plt.bar() returns a BarContainer object, which is an iterable of Rectangle patch objects, one per bar. Assigning it to bar enables iteration.
for b in bar: Iterates over each Rectangle (bar) in the container.
b.get_height(): Returns the height (numerical value) of the current bar.
b.get_x(): Returns the x-coordinate of the left edge of the bar.
b.get_width(): Returns the width of the bar.
b.get_x() + b.get_width() / 2: Computes the x-coordinate of the bar's center, ensuring the text is horizontally centered above the bar.
plt.text(x, y, s, ha, va): Places the text string s at coordinates (x, y).
ha='center': Horizontal alignment — centers the text at the x position.
va='bottom': Vertical alignment — places the bottom of the text at y (just above the bar top).
s=f'{height}': The text content, formatted using an f-string to display the numeric height value.
plt.grid(axis='y'): Adds horizontal gridlines (along the y-axis). This makes it easier to read bar heights by visual alignment to the gridlines. Setting axis='x' adds vertical gridlines; axis='both' adds both.
Histogram — plt.hist()
A histogram displays the frequency distribution of a single continuous numerical variable by dividing its range into equal-width intervals (bins) and counting how many values fall in each bin. Unlike a bar chart (discrete categories), a histogram's bars are adjacent with no gaps, reflecting the continuous nature of the data.

Parameter breakdown:

bins=3: Divides the range of the data into 3 equal-width intervals. A small number of bins produces a coarser, more summarized view. More bins reveal more detail.
edgecolor='black': Draws a black border around each bar, separating adjacent bins and improving readability.
alpha=0.30: Sets the bar transparency (0.0 = fully transparent, 1.0 = fully opaque). At 0.30, the bars are mostly transparent, allowing background gridlines to show through.
Histogram with Mean Overlay — plt.axvline() and np.mean()
A more informative histogram overlays statistical reference lines for the mean and (optionally) the median, allowing visual assessment of distribution skewness.

Function and parameter breakdown:

np.mean(Marks): Computes the arithmetic mean of the list. Returns 72.0 for this data.
plt.axvline(x, color, linestyle, linewidth, label): Draws a vertical line spanning the full height of the axes at x-coordinate x.
linestyle='--': Dashed line. Other options: '-' (solid), ':' (dotted), '-.' (dash-dot).
linewidth=2: Sets the thickness of the line in points.
label='Mean': Assigns a legend label to this line.
plt.grid(axis='y', linestyle='--', alpha=0.5): Adds semi-transparent dashed horizontal gridlines for easier reading of frequencies.
print(mean_value): Prints the computed mean (72.0) to the console.
Scatter Plot — plt.scatter()
A scatter plot displays individual data points as dots on a two-dimensional plane, with one variable on the x-axis and another on the y-axis. It is the primary chart for exploring the correlation between two numerical variables.

plt.scatter(x, y) plots one dot per data point at the coordinates (x[i], y[i]). A positive correlation between Study_Hours and Marks (more study hours → higher marks) would appear as a upward-sloping cluster of dots. No correlation would appear as a random cloud.

Conditional Scatter Plot — Color Encoding with List Comprehension
Visual encoding adds a third variable to a 2D scatter plot by mapping it to the color of each point. This is done by creating a list of colors based on a condition.

df['Result'] = [...]: Adds a new 'Result' column to the DataFrame (Pass/Fail labels).
colors = ['red' if result == 'Fail' else 'green' for result in df['Result']]: A list comprehension that generates a color string for each row. Rows where Result is 'Fail' get 'red'; rows where Result is 'Pass' get 'green'.
c=colors: The c parameter of plt.scatter() accepts a list of color values, applying them point-by-point. This encodes the categorical Result variable as color.
This technique is called visual encoding — using a visual property (color, size, shape) to represent a data attribute. It allows a third variable (Pass/Fail) to be visible on a plot that already uses x and y for two other variables.

Seaborn Line Chart — sns.lineplot()
Seaborn's lineplot() produces a line chart from a DataFrame using column name arguments, avoiding the need to manually extract Series values.

x='Day': The column name to use as the x-axis (passed as a string).
y='Sales': The column name to use as the y-axis.
data=df: The DataFrame containing the data. Seaborn reads the specified columns directly from this DataFrame.
plt (without plt.show()): In Colab/Jupyter, referencing plt triggers inline display.
Seaborn's lineplot also automatically aggregates multiple y-values at the same x position and displays a confidence interval band, which is not available in Matplotlib's basic plot().

Applied to the Student-Dataset: sns.lineplot(x='Gender', y='Attendance_Percentage', data=df)

Seaborn Bar Chart — sns.barplot()
Seaborn's barplot() displays the mean of y for each category in x, and automatically adds error bars representing a 95% confidence interval. This makes it more statistically informative than Matplotlib's plt.bar(), which simply plots the raw value without any uncertainty estimate.

palette='viridis' (optional): Applies a Seaborn/Matplotlib color palette to the bars. Other options include 'Set1', 'Blues', 'husl', and many more.
Applied to the Student-Dataset: sns.barplot(x='Department', y='Placement_Status', data=df)

Seaborn Histogram — sns.histplot()
sns.histplot() is Seaborn's histogram function. Unlike Matplotlib's plt.hist(), Seaborn's version integrates with DataFrames and supports an optional Kernel Density Estimate (KDE) overlay via kde=True: sns.histplot(df['Sales'], bins=5, kde=True)

The KDE curve is a smoothed, continuous approximation of the underlying distribution, making it easier to identify the distribution shape (normal, skewed, bimodal, etc.) compared to a jagged histogram alone.

Applied to the Student-Dataset: sns.histplot(df['CGPA'], bins=5)

Seaborn Scatter Plot — sns.scatterplot()

sns.scatterplot(x='Sales', y='Profit', data=df) plt.title('Pranav') plt

Seaborn's scatterplot() function takes column name strings and a DataFrame, making it more readable than plt.scatter() with explicit Series extraction. It also supports the hue parameter for automatic color-based categorical encoding: sns.scatterplot(x='Sales', y='Profit', data=df, hue='Category')

When hue='Category' is specified, Seaborn automatically assigns a distinct color to each unique value of the Category column and generates a legend, eliminating the need to manually create a color list as in Matplotlib's conditional scatter plot approach.

Applied to the Student-Dataset: sns.scatterplot(x='Gender', y='CGPA', data=df)

Loading a CSV Dataset for Chart Application

df = pd.read_csv('/content/Student-Dataset.csv') df

All chart types demonstrated on manually created data were subsequently re-applied to the Student-Dataset to practice using visualization on real loaded data. This reinforced that Matplotlib and Seaborn work identically regardless of whether the DataFrame was created manually or loaded from a file.

Comparison of Matplotlib vs. Seaborn Commands
Chart Type	Matplotlib Command	Seaborn Command
Line Chart	plt.plot(x, y, marker=, color=)	sns.lineplot(x=, y=, data=)
Bar Chart	plt.bar(x, height, color=)	sns.barplot(x=, y=, data=)
Histogram	plt.hist(data, bins=, edgecolor=)	sns.histplot(data, bins=, kde=)
Scatter Plot	plt.scatter(x, y, c=colors)	sns.scatterplot(x=, y=, hue=)
Matplotlib offers more granular control (custom markers, colors, annotations via plt.text(), reference lines via plt.axvline(), grid via plt.grid()). Seaborn offers built-in statistical features (confidence intervals, KDE, automatic hue encoding) and requires less code for standard statistical plots.

Summary of plt.* Utility Functions Used
plt.title(str): Adds a title above the chart.
plt.xlabel(str): Labels the horizontal axis.
plt.ylabel(str): Labels the vertical axis.
plt.show(): Renders and displays the current figure.
plt.figure(figsize=(w,h)):Creates a new figure with specified width and height in inches.
plt.legend(): Displays the legend using label= values from plot commands.
plt.axvline(x, ...): Draws a full-height vertical reference line at x-coordinate x.
plt.grid(axis=, ...): Adds gridlines to the specified axis ('x', 'y', or 'both').
plt.text(x, y, s, ha, va):Places text string s at position (x, y) with specified horizontal (ha) and vertical (va) alignment.
CONCLUSION

Basic Charts and Visual Encoding using Python's Matplotlib and Seaborn libraries were successfully studied and implemented.
