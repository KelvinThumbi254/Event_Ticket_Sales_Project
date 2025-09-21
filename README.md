# Introduction
This report provides comprehensive documentation of the Tkinter GUI application designed to assist users in predicting event ticket sales using the Prophet library. The application offers functionalities to display events and perform predictions through a user-friendly interface.
## Description
The Tkinter GUI application, named PredictionApp, is developed to facilitate event ticket sales prediction using the Prophet library. It allows users to display a list of events and perform sales predictions based on historical data. The application is designed with a user-friendly interface that includes buttons, labels, entry fields, and a scrolled text widget for output display.
## Features:
1.	Display a list of events.
2.	Perform predictions on ticket sales.
3.	User input fields for specifying the date range for predictions.
4.	Display prediction results in a scrollable text area.
b) Code Structure Description and Code Snippets
## Overall Structure:
The application is encapsulated within the PredictionApp class. The main components include methods for setting up the UI, displaying events, showing prediction fields, and performing predictions. Below is a detailed breakdown of the code structure:
## 1. Initialization and Window Setup:
The __init__ method initializes the main window, sets its properties, and calls methods to center the window and set up the UI components.
python
Copy code
import tkinter as tk
from tkinter import messagebox, scrolledtext
from datetime import datetime
from prophet import Prophet
import pandas as pd
import matplotlib.pyplot as plt
import os

class PredictionApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Group 3 Prediction App")
        self.center_window(840, 750)
        self.root.resizable(True, True)
        self.current_directory = os.path.dirname(os.path.abspath(__file__))
        self.selected_df = None
        self.setup_ui()
## 2. Centering the Window:
The center_window method calculates the position to center the window on the screen.
python
Copy code
def center_window(self, width, height):
    screen_width = self.root.winfo_screenwidth()
    screen_height = self.root.winfo_screenheight()
    x = (screen_width // 2) - (width // 2)
    y = (screen_height // 2) - (height // 2)
    self.root.geometry(f'{width}x{height}+{x}+{y}')
## 3. Setting Up the UI:
The setup_ui method creates and positions the UI components including labels, buttons, and entry fields.
python
Copy code
def setup_ui(self):
    tk.Label(self.root, text="Welcome to the Prediction App, how can we assist you today?", font=("Helvetica", 16)).grid(row=0, column=0, columnspan=2, pady=10)
    
    tk.Button(self.root, text="1. Display list of Events Present", command=self.display_events, width=30).grid(row=1, column=0, columnspan=2, pady=10)
    self.predict_button = tk.Button(self.root, text="2. Do a Prediction", command=self.show_prediction_fields, state="disabled", width=30)
    self.predict_button.grid(row=2, column=0, columnspan=2, pady=10)
    
    self.start_date_label = tk.Label(self.root, text="Enter the first day for ticket sales (YYYY-MM-DD):", anchor='e')
    self.start_date_entry = tk.Entry(self.root, width=30)
    self.stop_date_label = tk.Label(self.root, text="Enter the last date of the event (YYYY-MM-DD):", anchor='e')
    self.stop_date_entry = tk.Entry(self.root, width=30)
    
    self.do_prediction_button = tk.Button(self.root, text="Predict", command=self.perform_prediction, width=30)
    
    self.output_display = scrolledtext.ScrolledText(self.root, wrap=tk.WORD, width=80, height=20)
## 4. Displaying Events:
The display_events method retrieves and displays a list of events. (Note: The implementation specifics are assumed based on typical functionality.)
python
Copy code
def display_events(self):
    # This method should retrieve events from a dataset and display them
    events = "List of events...\n"  # Placeholder for actual event data retrieval
    self.output_display.grid(row=6, column=0, columnspan=2, pady=10)
    self.output_display.insert(tk.END, events)
    self.predict_button.config(state="normal")
## 5. Showing Prediction Fields:
The show_prediction_fields method displays the entry fields and prediction button.
python
Copy code
def show_prediction_fields(self):
    self.start_date_label.grid(row=3, column=0, sticky='e')
    self.start_date_entry.grid(row=3, column=1)
    self.stop_date_label.grid(row=4, column=0, sticky='e')
    self.stop_date_entry.grid(row=4, column=1)
    self.do_prediction_button.grid(row=5, column=0, columnspan=2, pady=10)
## 6. Performing Prediction:
The perform_prediction method executes the prediction using the Prophet library and displays the results.
python
Copy code
def perform_prediction(self):
    start_date = self.start_date_entry.get()
    stop_date = self.stop_date_entry.get()
    
    # Example data loading and preprocessing (actual implementation will vary)
    df = pd.read_csv(os.path.join(self.current_directory, 'data.csv'))
    df['ds'] = pd.to_datetime(df['date'])
    df['y'] = df['sales']
    
    model = Prophet()
    model.fit(df)
    
    future = model.make_future_dataframe(periods=(pd.to_datetime(stop_date) - pd.to_datetime(start_date)).days)
    forecast = model.predict(future)
    
    plt.figure(figsize=(10, 6))
    model.plot(forecast)
    plt.title('Ticket Sales Prediction')
    plt.xlabel('Date')
    plt.ylabel('Sales')
    plt.grid(True)
    plt.show()
    
    self.output_display.grid(row=6, column=0, columnspan=2, pady=10)
    self.output_display.insert(tk.END, str(forecast.tail()))
c) Execution
To execute the application, follow these steps:
1.	Ensure that all dependencies are installed. You can install them using pip:
sh
Copy code
pip install tkinter pandas matplotlib prophet
2.	Save the complete code into a Python file, e.g., prediction_app.py.
3.	Ensure that you have a dataset named data.csv in the same directory as the Python file. This dataset should have at least two columns: date and sales.
4.	Run the Python script:
sh
Copy code
python prediction_app.py
5.	The application window will open. Follow these steps to use the application:
o	Click the "Display list of Events Present" button to load and display events.
o	Click the "Do a Prediction" button to enable the prediction fields.
o	Enter the start date and stop date for the prediction in the format YYYY-MM-DD.
o	Click the "Predict" button to perform the prediction and view the results.
## Conclusion
This Tkinter GUI application provides a user-friendly interface for event prediction using the Prophet library. It offers functionalities to display events and perform predictions, making it a valuable tool for event managers and planners.
The encapsulation of the application within the PredictionApp class ensures modularity and ease of maintenance. The detailed setup of GUI components and the use of various libraries highlight the comprehensive design and functionality of the application.

