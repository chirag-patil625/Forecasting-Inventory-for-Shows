# Forecasting Inventory for Shows
Ticket Availability Prediction is a machine learning project aimed at forecasting the remaining capacity of event tickets.

## Problem Statement

Event ticket sales often follow non-traditional patterns due to limited inventory and fixed event dates. This project addresses the challenge of predicting the remaining ticket capacity for upcoming events, considering the maximum capacity and the days left until the event. The solution is designed to forecast ticket availability using a Random Forest Regressor model.


## Solution Overview:
The solution uses machine learning to predict the remaining capacity for an event based on the number of days until the event, total availability, and capacity. The model is trained using the RandomForestRegressor and predictions are scaled for better performance.


## Dataset

The dataset used in this project consists of the following key attributes:

- **show_id**: Unique identifier for the show.
- **timestamp**: Date and time when the availability data was recorded.
- **availability_standard**: Number of standard tickets available.
- **availability_resale**: Number of resale tickets available.
- **capacity**: Maximum capacity for the show.
- **event_date**: Date of the event.
- **venue_id**: Identifier for the venue.
- **event_time_zone**: Time zone of the event.
- **total_availability**: Sum of standard and resale availability.
- **days_until_event**: Days remaining until the event.
- **log_remaining_capacity**: Log-transformed remaining capacity (the target variable).



## Project Workflow

1. Data Preprocessing
Datetime Conversion: The timestamp and event_date columns are converted to datetime objects, ensuring that both are timezone-aware and aligned to the same timezone.

2. Feature Engineering:

3. total_availability is calculated by summing the availability_standard and availability_resale columns.
days_until_event is computed as the difference between event_date and timestamp.
Handling Missing Values: Missing values in key columns such as capacity and total_availability are filled using mean values, ensuring consistency in the data.

4. Log Transformation: To stabilize variance and ensure non-negativity, the remaining capacity (i.e., capacity - total_availability) is transformed using a log function.

5. Scaling Features: Features such as days_until_event, total_availability, and capacity are scaled using MinMaxScaler to standardize them for model training.
#


## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install the required dependencies.
```bash
pip install -r requirements.txt
```

## Project Structure

```
Ticket Availability Prediction/
│
├── app.py                      # Flask web application
├── e0318324-c453-47ed-af34-cc1051e07549.csv    # Dataset
├── rf_model.joblib              # Trained Random Forest model
├── scaler.joblib                # Scaler for feature transformation
├── README.md                    # Project documentation
├── templates/
│   └── index.html               # Web interface (HTML form)
└── static/
    └── css/                     # Static CSS assets for styling
```

## Usage

### Running the Application

1. **Clone the Repository**: Download or clone the project repository to your local machine.
2. **Prepare the Dataset**: Ensure that the dataset (`e0318324-c453-47ed-af34-cc1051e07549.csv`) is placed in the working directory.
3. **Train the Model**: Run the Python script to train the Random Forest model. This will generate two files:
   - `rf_model.joblib` (the trained model)
   - `scaler.joblib` (the fitted scaler)
4. **Start the Flask Web Application**:

   ```bash
   python app.py
   ```

5. **Access the Web Interface**: Open a web browser and navigate to [http://127.0.0.1:5000/](http://127.0.0.1:5000/).
6. **Use the Prediction Form**: Enter the required details in the form (days until event, total availability, and capacity) to get a prediction of the remaining ticket capacity.

### Example Usage

Once the form is filled out with the required data, the application will display the predicted remaining capacity of tickets for the event.

**Example Output**:

```yaml
Predicted Remaining Capacity: 100.45
```

## Model Details

### Data Preprocessing

- **Datetime Conversion**: Convert `timestamp` and `event_date` columns to datetime objects. Ensure both are timezone-aware and aligned to the same timezone.
- **Feature Engineering**: 
  - Compute `total_availability` by summing `availability_standard` and `availability_resale`.
  - Calculate `days_until_event` as the difference between `event_date` and `timestamp`.
- **Missing Values**: Fill missing values for `capacity` and `total_availability` with mean values.
- **Log Transformation**: The remaining capacity (i.e., `capacity - total_availability`) is transformed using a logarithmic function to stabilize variance.
- **Scaling Features**: Features such as `days_until_event`, `total_availability`, and `capacity` are scaled using `MinMaxScaler`.

### Model Development

A Random Forest Regressor model is trained on the following features:

- `days_until_event`
- `total_availability`
- `capacity`

The target variable is the log-transformed remaining capacity.

### Model Evaluation

The performance of the Random Forest model is evaluated using the following metrics:

- Mean Absolute Error (MAE): 0.0003
- Mean Squared Error (MSE): 0.0001
- Root Mean Squared Error (RMSE): 0.0092
- R-squared (R²): 1.0000 (indicating near-perfect performance on the training set)

The trained model and scaler are saved as .joblib files for reuse in the Flask application.

## Flask Application

The Flask application enables users to input event details (days until event, total availability, and capacity) via a web interface and receive predictions for the remaining ticket capacity.

- **Form Input**: Users enter the number of days until the event, total ticket availability, and the event capacity.
- **Prediction**: The app scales the input data, makes predictions using the pre-trained model, and displays the results after reversing the log transformation.

## API Endpoints

- `/`: Renders the form for input.
- `/predict`: Processes the form data and returns the predicted remaining ticket capacity.

## Future Enhancements

- **Incorporate External Data**: Integrate additional features such as event popularity, historical sales trends, and weather data to improve accuracy.
- **Real-Time Predictions**: Implement real-time data streaming to provide up-to-date predictions as the event date approaches.
- **Model Improvement**: Experiment with advanced models such as Gradient Boosting Machines or XGBoost for potentially better performance.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)

