#importing libraries
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

#reading a csv file using pandas
data = pd.read_csv('C:/Users/FUJITSU/Downloads/day_wise2.csv')


#checking if the data is imported with success
print(data.head(10))
print (data.info)

#defining function for line graph accepting dataset as parameter
def line_plot(data):

#Extracting data to variables
    Confirmed = data['Confirmed']
    deaths = data['Deaths']
    recovered = data['Recovered']
    active = data['Active']
    day=data['Day']

#plotting data on line graph using pyplot
    plt.plot(day, Confirmed, label='Confirmed cases')
    plt.plot(day, deaths, label='Deaths')
    plt.plot(day, recovered, label='Recovered')
    plt.plot(day, active, label='Active cases')
    

    # Display the graph
    # Add labels,title and legend
    plt.xlabel('Cases day wise')
    plt.ylabel('Values')
    plt.legend()
    plt.title('Line graph of values of confirmed cases over time')
    # Show the chart 
    plt.show()





#defining function for Pie chart accepting dataset as parameter
def pie_plot(data):
    
    # Define the categories for the pie chart
    categories = ['Deaths', 'Recovered', 'Active']
    
    # Extracting the values for day 100
    second_value_column1 = data.loc[100, 'Deaths']
    second_value_column2 = data.loc[100, 'Recovered']
    second_value_column3 = data.loc[100, 'Active']

    # Create a list 'plotted' to store the extracted values
    plotted = [second_value_column1, second_value_column2, second_value_column3]

    # Create a new figure for the pie chart with a specified size
    plt.figure(figsize=(6, 6))

    # Create a pie chart using the 'plotted' values with labels and percentage formatting
    plt.pie(plotted, labels=categories, autopct='%1.1f%%')

    # Set a title for the pie chart
    plt.title('Pie Chart of Confirmed Cases of a particular day')

    # Display the pie chart
    plt.show()




#defining function for Bar chart accepting dataset as parameter
def bar_chart(data):

    # Create an array 'x' with values representing the x-axis positions for each bar
    x = np.arange(len(data['Date']))

    # Define the width of each bar
    width = 0.2

    # Create a grouped bar chart for Confirmed, Deaths, and Recovered cases
    # Each set of bars is shifted by 'width' to create a grouped effect
    plt.bar(x - width, data['Confirmed'], width, label='Confirmed', color='blue')
    plt.bar(x, data['Deaths'], width, label='Deaths', color='red')
    plt.bar(x + width, data['Recovered'], width, label='Recovered', color='yellow')

    # Add labels and a title to the chart
    plt.xlabel('Date')  # Label for the x-axis
    plt.ylabel('Counts')  # Label for the y-axis
    plt.title('COVID-19 Cases Over Time')  # Title for the chart

    # Customize the x-axis ticks to display every 17th value and rotate them for better readability
    plt.xticks(range(0, 188, 17), data['Date'].iloc[::17], rotation=90)

    # Add a legend to differentiate the bars by label
    plt.legend()

    # Display the bar chart
    plt.show()



# Call the functions with the data
line_plot(data)  # Create and display a line plot
pie_plot(data)   # Create and display a pie chart
bar_chart(data)  # Create and display a grouped bar chart