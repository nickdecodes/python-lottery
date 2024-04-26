# API Reference
## Class: IOUtil

The `IOUtil` class provides utility methods for input/output operations.

### Method: get_logger

Returns a configured logger instance.

#### Parameters:
- `log_file` (str, optional): The name of the file to log to. If not provided, logging will be directed to the terminal.

#### Returns:
- `logging.Logger`: A configured logger instance.

#### Description:
This method retrieves or creates a logger instance based on the provided `log_file` argument. If no `log_file` is specified, a default logger named 'default_logger' is used. The method configures the logger with the specified log format and log level. If logging to a file, it uses rotation at midnight and keeps up to 7 backup log files.

If the logger does not already have handlers, the method configures the appropriate handler (either for logging to the terminal or to a file) and sets the formatter and log level for the handler. The configured logger is then returned.

#### Example Usage:
```python
# To obtain a logger logging to a file:
logger = IOUtil.get_logger('app.log')

# To obtain a logger logging to the terminal:
logger = IOUtil.get_logger()
```

### Method: list_to_int

Converts a list of integers to a single integer, with an optional replacement for zeros.

#### Parameters:
- `numbers` (List[int]): A list of integers.
- `zero_replacement` (str, optional): A string to replace zeros with. Defaults to an empty string.
- `**kwargs` (Any): Additional keyword arguments.

#### Returns:
- `int`: A single integer formed by concatenating the list elements.

#### Description:
This method takes a list of integers and concatenates them into a single integer, with an optional replacement for zeros. It validates that the input data is a list and that all elements in the list are integers. Zeros in the list are replaced with the specified `zero_replacement` string. The list elements are then joined and converted to an integer, which is returned.

#### Example Usage:
```python
# Convert a list of integers to a single integer
result = IOUtil.list_to_int([1, 2, 3, 0, 5])

# Convert a list of integers to a single integer with zero replacement
result = IOUtil.list_to_int([1, 0, 3, 0, 5], zero_replacement='X')
```

### Method: int_to_list

Converts an integer to a list of digits, each digit is the remainder of division by a modulus.

#### Parameters:
- `number` (int): The integer to be converted into a list of digits.
- `modulus` (int, optional): The divisor used for the modulo operation on each digit. Defaults to 10.
- `**kwargs` (Any): Additional keyword arguments.

#### Returns:
- `List[int]`: A list of integers, where each integer is a digit of the original number after the modulo operation.

#### Description:
This method takes an integer and converts it into a list of digits, where each digit is the remainder of division by a specified modulus. It validates that the input data is an integer and that the modulus is a positive integer. The integer is converted to a list of digits using the specified modulus, and the resulting list is returned.

#### Example Usage:
```python
# Convert an integer to a list of digits
result = IOUtil.int_to_list(12345)

# Convert an integer to a list of digits with a specified modulus
result = IOUtil.int_to_list(98765, modulus=8)
```

### Method: write_data_to_file

Writes data to a file.

#### Parameters:
- `file_path` (str): Path to the file where data will be written.
- `data` (List[str]): List of data to write to the file.
- `app_log` (Optional[logging.Logger], optional): Optional logger for logging information. Defaults to None.
- `mode` (str, optional): Mode in which the file should be opened. Defaults to 'a+' for append.
- `**kwargs` (Any): Additional keyword arguments.

#### Returns:
- `bool`: Indicates whether the operation was successful (True) or failed (False).

#### Description:
This method writes the provided data to the specified file. If no logger is provided, it uses the default logger obtained from the `get_logger` method. It checks if data is provided and logs a warning if no data is provided. It then attempts to open the file in the specified mode and write each line of data to the file. If an error occurs during the write operation, it logs the exception and returns False.

#### Example Usage:
```python
# Write data to a file
success = IOUtil.write_data_to_file('output.txt', ['Line 1', 'Line 2', 'Line 3'])

# Write data to a file with a specified logger and mode
logger = IOUtil.get_logger('app.log')
```
### Method: read_data_from_file

Reads data from a file and returns a list of non-empty lines.

#### Parameters:
- `file_path` (str): Path to the file to be read.
- `app_log` (Optional[logging.Logger], optional): Optional logger for logging information. Defaults to None.
- `mode` (str, optional): Mode in which the file should be opened. Defaults to 'r' for read only.

#### Returns:
- `Optional[List[str]]`: List of non-empty lines from the file or None if an exception occurs.

#### Description:
This method reads the data from the specified file and returns a list of non-empty lines. If no logger is provided, it uses the default logger obtained from the `get_logger` method. It attempts to open the file in the specified mode and reads each line, stripping any leading and trailing whitespace. It then filters out empty lines and returns the list of non-empty lines. If an error occurs during the read operation, it logs the exception and returns None.

#### Example Usage:
```python
# Read data from a file
data = IOUtil.read_data_from_file('input.txt')

# Read data from a file with a specified logger and mode
logger = IOUtil.get_logger('app.log')
data = IOUtil.read_data_from_file('input.txt', app_log=logger, mode='r')
```

### Method: write_csv_data_to_file

Writes data to a CSV file.

#### Parameters:
- `file_path` (str): Path to the file where CSV data will be written.
- `data` (List[List[Any]]): List of rows (where each row is a list) to write to the CSV file.
- `app_log` (Optional[logging.Logger], optional): Optional logger for logging information. Defaults to None, which will create a new logger.
- `mode` (str, optional): Mode in which the file should be opened. Defaults to 'a+' for append.
- `newline` (str, optional): Controls how universal newlines works (it only applies to text mode). Defaults to ''.
- `**kwargs` (Any): Additional keyword arguments.

#### Returns:
- `bool`: Indicates whether the operation was successful (True) or failed (False).

#### Description:
This method writes the provided data to the specified CSV file. If no logger is provided, it uses the default logger obtained from the `get_logger` method. It checks if data is provided and logs a warning if no data is provided. It then attempts to open the file in the specified mode and write the data to the CSV file using the `csv.writer` class. If an error occurs during the write operation, it logs the exception and returns False.

#### Example Usage:
```python
# Write data to a CSV file
success = IOUtil.write_csv_data_to_file('output.csv', [['Name', 'Age'], ['John', 30], ['Alice', 25]])

# Write data to a CSV file with a specified logger and mode
logger = IOUtil.get_logger('app.log')
success = IOUtil.write_csv_data_to_file('output.csv', [['Name', 'Age'], ['John', 30], ['Alice', 25]], app_log=logger, mode='w', delimiter=',')
```

### Method: read_csv_data_from_file

Reads CSV data from a file and returns a list of rows.

#### Parameters:
- `file_path` (str): Path to the CSV file to be read.
- `app_log` (Optional[logging.Logger], optional): Optional logger for logging information. Defaults to a new logger if None.
- `mode` (str, optional): Mode in which the file should be opened. Defaults to 'r' for read only.
- `**kwargs` (Any): Additional keyword arguments.

#### Returns:
- `Optional[List[List[str]]]`: List of rows from the CSV file or None if an exception occurs.

#### Description:
This method reads the CSV data from the specified file and returns a list of rows. If no logger is provided, it uses the default logger obtained from the `get_logger` method. It attempts to open the file in the specified mode and reads the CSV data using the `csv.reader` class. It then returns the list of rows. If an error occurs during the read operation, it logs the exception and returns None.

#### Example Usage:
```python
# Read CSV data from a file
data = IOUtil.read_csv_data_from_file('input.csv')

# Read CSV data from a file with a specified logger and mode
logger = IOUtil.get_logger('app.log')
data = IOUtil.read_csv_data_from_file('input.csv', app_log=logger, mode='r', delimiter=',')
```

### Method: write_json_data_to_file

Writes data to a JSON file.

#### Parameters:
- `file_path` (str): Name of the JSON file.
- `data` (Any): Data to write (usually a dict or a list).
- `app_log` (Optional[logging.Logger], optional): Optional logger for logging information. Defaults to a new logger if None.
- `mode` (str, optional): Mode in which the file should be opened. Defaults to 'w' for write (overwriting).
- `**kwargs` (Any): Additional keyword arguments.

#### Returns:
- `bool`: Indicates whether the operation was successful (True) or failed (False).

#### Description:
This method writes the provided data to the specified JSON file. If no logger is provided, it uses the default logger obtained from the `get_logger` method. It then attempts to open the file in the specified mode and write the data to the JSON file using the `json.dump` method. If an error occurs during the write operation, it logs the exception and returns False.

#### Example Usage:
```python
# Write data to a JSON file
success = IOUtil.write_json_data_to_file('output.json', {'name': 'John', 'age': 30})

# Write data to a JSON file with a specified logger and mode
logger = IOUtil.get_logger('app.log')
success = IOUtil.write_json_data_to_file('output.json', {'name': 'John', 'age': 30}, app_log=logger, mode='a', separators=(',', ':'))
```

### Method: read_json_data_from_file

Reads data from a JSON file.

#### Parameters:
- `file_path` (str): Name of the JSON file.
- `app_log` (Optional[logging.Logger], optional): Optional logger for logging information. Defaults to a new logger if None.
- `mode` (str, optional): Mode in which the file should be opened. Defaults to 'r' for read.
- `**kwargs` (Any): Additional keyword arguments.

#### Returns:
- `Optional[Any]`: Data read from the JSON file or None if an exception occurs.

#### Description:
This method reads the data from the specified JSON file and returns it. If no logger is provided, it uses the default logger obtained from the `get_logger` method. It attempts to open the file in the specified mode and reads the data from the JSON file using the `json.load` method. It then returns the data read from the file. If an error occurs during the read operation, it logs the exception and returns None.

#### Example Usage:
```python
# Read data from a JSON file
data = IOUtil.read_json_data_from_file('input.json')

# Read data from a JSON file with a specified logger and mode
logger = IOUtil.get_logger('app.log')
data = IOUtil.read_json_data_from_file('input.json', app_log=logger, mode='r', encoding='utf-8')
```

## Class: ModelUtil

The `ModelUtil` class provides utility methods for handling and analyzing numerical data.

### Method: exponential_moving_average_next_value

Calculate the Exponential Moving Average (EMA) of a given numeric sequence.

#### Parameters:
- `numeric_sequence` (List[int]): A list or sequence of numbers for which the EMA is to be calculated.
- `param span:` The number of periods over which to calculate the EMA. Default is 5.

#### Returns:
- `int`: The EMA value as an integer.

#### Description:
This method calculates the Exponential Moving Average (EMA) of the provided numeric sequence. EMA is a type of moving average that places a greater weight and significance on the most recent data points, making it more responsive to new information compared to a simple moving average (SMA). The method uses the pandas library to convert the numeric sequence into a Series object and then calculates the EMA using the `ewm` method with specified parameters such as 'span' and 'min_periods'. The last value of the EMA series is returned as an integer.

#### Example Usage:
```python
# Calculate the EMA of a numeric sequence
ema_value = ModelUtil.exponential_moving_average_next_value([10, 15, 20, 25, 30])
print(f"The EMA value is: {ema_value}")
```

### Method: linear_regression_next_value_by_index

Predicts the next value in a sequence using linear regression.

#### Parameters:
- `numeric_sequence` (List[int]): A list or sequence of numbers to model.

#### Returns:
- `int`: The predicted next value in the sequence as an integer.

#### Description:
This method uses linear regression to predict the next value in a given sequence of numbers. Linear regression involves fitting a line to the data points in such a way that the distance between the data points and the line is minimized. The method converts the numeric sequence into a numpy array and reshapes it for use with the scikit-learn library. It then creates a LinearRegression model, fits it to the data, and predicts the next value in the sequence using the fitted model. The predicted value is returned as an integer.

#### Example Usage:
```python
# Predict the next value in a sequence using linear regression
next_value = ModelUtil.linear_regression_next_value_by_index([10, 15, 20, 25, 30])
print(f"The predicted next value is: {next_value}")
```

### Method: multivariate_polynomial_regression_next_value

Predicts the next value in a numeric sequence using multivariate polynomial regression.

#### Parameters:

- `numeric_sequence` (List[int]): A list or sequence of numbers to model.
- `rolling_size (int):` The number of elements in each rolling window.
- `degrees (int):` The degree of the polynomial regression. Defaults to 3.

#### Returns:

- `float:` The predicted next value in the sequence.

#### Description:

This method applies a polynomial regression model to a numeric sequence to predict the next value. It utilizes a rolling window approach to create datasets, scales the features, and fits a polynomial regression model to make the prediction.

#### Example Usage:

```python
# Predict the next value in a sequence using harmonic regression
next_value = ModelUtil.multivariate_polynomial_regression_next_value([10, 15, 20, 25, 30], rolling_size=3, degrees=2)
print(f"The predicted next value is: {next_value}")
```

### Method: harmonic_regression_next_value_by_index

Predicts the next value in a sequence using harmonic regression.

#### Parameters:
- `numeric_sequence` (List[int]): A list or sequence of numbers to model.
- `frequency` (float, optional): The frequency of the periodic component to model. Defaults to 1.0.

#### Returns:
- `int`: The predicted next value in the sequence as an integer.

#### Description:
This method predicts the next value in a given sequence of numbers by fitting a harmonic model to the sequence using sine and cosine components. Harmonic regression involves capturing periodic patterns in the data by fitting a model with sine and cosine components. The method converts the numeric sequence into a numpy array and creates sine and cosine features based on the time array and given frequency. It then creates a LinearRegression model, fits it to the data with harmonic features, and predicts the next value in the sequence using the fitted model. The predicted value is returned as an integer.

#### Example Usage:
```python
# Predict the next value in a sequence using harmonic regression
next_value = ModelUtil.harmonic_regression_next_value_by_index([10, 15, 20, 25, 30], frequency=0.5)
print(f"The predicted next value is: {next_value}")
```

### Method: random_forest_regressor_next_value

Predicts the next value in a numeric sequence using a Random Forest Regressor model.

#### Parameters:
- `numeric_sequence (List[int]):` The list of integers representing the sequence.
- `rolling_size (int):` The number of elements in each rolling window.
- `warm_start (bool):` Whether to reuse the solution of the previous call to fit and add more estimators to the ensemble.
- `random_state (int):` Controls both the randomness of the bootstrapping of the samples used when building trees
                                    (if `bootstrap=True`) and the sampling of the features to consider when looking for the best split at each node.
-  `param_distributions (Optional[Dict]):` The distribution of parameters to try in randomized search.
                                                    eg: {
                                                        'n_estimators': stats.randint(100, 500),
                                                        'max_depth': [None, ] + [i for i in range(10, 100)],
                                                        'max_features': ['sqrt', 'log2'],
                                                        'min_samples_split': stats.randint(2, 80),
                                                        'min_samples_leaf': stats.randint(1, 40)
                                                    }
- `param_overrides (Optional[Dict]):` Additional parameters for the RandomizedSearchCV.
                                                    eg: {
                                                        'n_iter': 100,
                                                        'cv': 3,
                                                        'scoring': 'neg_mean_squared_error',
                                                        'verbose': 0,
                                                        'random_state': 12,
                                                        'n_jobs': -1
                                                    }

#### Returns:
- `float:` The predicted next value in the sequence.

#### Description:
This method uses a Random Forest Regressor to predict the next value in a sequence based on the values in a rolling window. The sequence is first transformed into a dataset suitable for regression by creating overlapping windows of specified size.

#### Example Usage:
```python
# Predict the next value in a sequence using a Random Forest Regressor
next_value = ModelUtil.random_forest_regressor_next_value([10, 15, 20, 25, 30], rolling_size=3)
print(f"The predicted next value is: {next_value}")
```

### Method: random_forest_regressor_next_value_by_index

Predicts the next value in a sequence using a Random Forest Regressor.

#### Parameters:
- `numeric_sequence` (List[int]): A list or sequence of numbers to model.

#### Returns:
- `int`: The predicted next value in the sequence as an integer.

#### Description:
This method predicts the next value in a given sequence of numbers using a Random Forest Regressor, which is an ensemble machine learning model that uses multiple decision trees to make predictions. It is particularly useful for regression tasks on complex datasets because it can capture non-linear relationships between variables. The method converts the numeric sequence into a numpy array and creates a RandomForestRegressor model, fits it to the data, and predicts the next value in the sequence using the fitted model. The predicted value is returned as an integer.

#### Example Usage:
```python
# Predict the next value in a sequence using a Random Forest Regressor
next_value = ModelUtil.random_forest_regressor([10, 15, 20, 25, 30])
print(f"The predicted next value is: {next_value}")
```


### Method: relative_strength_index

Calculate the Relative Strength Index (RSI) for a given list of prices.

#### Parameters:
- `numeric_sequence` (List[int]): A list of prices for a particular stock or asset.
- `period` (int, optional): The period over which to calculate the RSI, typically 14. Defaults to 10.

#### Returns:
- `int`: The calculated RSI value.

#### Description:
This method calculates the Relative Strength Index (RSI), which is a momentum oscillator that measures the speed and change of price movements. It oscillates between zero and 100. Traditionally, RSI is considered overbought when above 70 and oversold when below 30. The method calculates the RSI value based on the given list of prices and the specified period. It calculates the differences between consecutive prices, separates the positive gains and negative losses, calculates the average gain and average loss, and then uses these values to calculate the RSI.

#### Example Usage:
```python
# Calculate the RSI for a list of prices
rsi_value = ModelUtil.relative_strength_index([50, 55, 60, 57, 62, 58, 63, 65, 70, 68, 72, 75], period=14)
print(f"The calculated RSI value is: {rsi_value}")
```

### Method: seasonal_autoregressive_integrated_moving_average_next_value

Fit a Seasonal Autoregressive Integrated Moving Average (SARIMA) model to the provided time series data and predict the next value in the series.

#### Parameters:
- `numeric_sequence` (List[int]): A list of numerical values representing a time series.

#### Returns:
- `int`: The next integer value predicted by the SARIMA model.

#### Description:
This method fits a Seasonal Autoregressive Integrated Moving Average (SARIMA) model to the provided time series data and predicts the next value in the series. SARIMA models are used to forecast future points in a time series and are capable of modeling complex seasonal patterns by incorporating both non-seasonal (ARIMA) and seasonal elements. The method converts the data to a numpy array for time series analysis, automatically discovers the optimal order for the SARIMA model, fits the SARIMA model to the time series data, and predicts the next value in the time series. The predicted value is returned as an integer.

#### Example Usage:
```python
# Fit a SARIMA model to the time series data and predict the next value
next_predicted_value = ModelUtil.seasonal_autoregressive_integrated_moving_average([100, 110, 120, 115, 125, 130, 135])
print(f"The next predicted value is: {next_predicted_value}")
```

## Class: SpiderUtil

The `SpiderUtil` class provides methods for crawling data from a specified URL.

### Constructor: __init__

Initialize the `SpiderUtil` object with a URL.

#### Parameters:
- `url` (str, optional): The URL to fetch the data from. Defaults to 'https://www.lottery.gov.cn/kj/kjlb.html?dlt'.

#### Description:
This constructor initializes the `SpiderUtil` object with a URL. If the URL is not provided, it defaults to a specific URL for fetching data. The URL can be specified as a keyword argument when creating an instance of `SpiderUtil`.

#### Example Usage:
```python
# Initialize a SpiderUtil object with a custom URL
spider = SpiderUtil(url='https://example.com/data')
```

### Method: spider_chrome_driver

Initialize a Chrome WebDriver with headless option and navigate to the URL.

#### Returns:
- `webdriver.Chrome`: An instance of Chrome WebDriver.

#### Description:
This method initializes a Chrome WebDriver with the headless option enabled and navigates to the URL specified in the `SpiderUtil` object. It returns an instance of the Chrome WebDriver that can be used for web crawling and data extraction.

#### Example Usage:
```python
# Initialize a SpiderUtil object with a custom URL
spider = SpiderUtil(url='https://example.com/data')
# Initialize a Chrome WebDriver and navigate to the URL
driver = spider.spider_chrome_driver()
# Use the driver to interact with the web page
```

### Abstract Method: spider_recent_data

Fetch the recent data from the web page.

#### Returns:
- `List[List[str]]`: A list of lists containing recent data entries.

#### Description:
This abstract method is responsible for fetching the recent data from the web page. It initializes a Chrome WebDriver, navigates to the specified URL, retrieves the recent data from the page, and returns it as a list of lists containing the data entries.

#### Example Usage:
```python
# Initialize a SpiderUtil object with a custom URL
spider = SpiderUtil(url='https://example.com/data')
# Fetch recent data from the web page
recent_data = spider.spider_recent_data()
print(recent_data)
```

### Abstract Method: spider_latest_data

Fetch the latest single data entry.

#### Returns:
- `Optional[List[str]]`: A list containing the latest data entry, or None if there is no data.

#### Description:
This abstract method is responsible for fetching the latest single data entry from the web page. It calls the `spider_recent_data` method to retrieve the recent data and returns the first entry from the recent data as a list, or None if there is no data available.

#### Example Usage:
```python
# Initialize a SpiderUtil object with a custom URL
spider = SpiderUtil(url='https://example.com/data')
# Fetch the latest single data entry from the web page
latest_data = spider.spider_latest_data()
if latest_data:
    print(latest_data)
else:
    print("No data available.")
```

### Abstract Method: spider_full_data

Load the full set of data from the source.

#### Returns:
- `List[List[str]]`: A list of lists containing all data entries.

#### Description:
This method is responsible for loading the full set of data from the source. Subclasses should provide their own implementation to fetch and return the complete data set from the source.

#### Example Usage:
```python
# Initialize a SpiderUtil object with a custom URL
spider = SpiderUtil(url='https://example.com/data')
# Load the full set of data from the source
full_data = spider.spider_full_data()
print(full_data)
```

## Class: CalculateUtil

The `CalculateUtil` class provides methods for computing features based on single or multiple data points.

### Class Method: generate_datasets_with_rolling_size

Generates sequential test and validation datasets from a list of integers. It optionally adjusts test datasets by removing extreme values.

#### Parameters:

- `data (List[int]):` The input data list from which datasets are generated.
- `rolling_size (int):` The number of elements in each test set. Defaults to 5.
- `adjust (bool):` Whether to remove the maximum and minimum values from each test set. Defaults to False.

#### Returns:

- `Tuple[List[List[int]], List[int]]:` A tuple containing two lists:
       - The first list contains the test sets, possibly adjusted.
       -  list contains the single-element validation sets.

#### Description:

The function iterates over the data to create overlapping test sets of a specified size. Each test set is  followed by a validation set which is the next single element in the list. If the 'adjust' flag is True,  the maximum and minimum values are removed from each test set.

#### Example Usage:

```python
# Calculate the counts of numbers within predefined zones
number_combination = [10, 15, 20, 25, 30]
zone_ranges = [(0, 15), (16, 25), (26, 35)]
zone_counts = CalculateUtil.calculate_zone_ratio(number_combination, zone_ranges)
print(zone_counts)
```

### Class Method: calculate_zone_ratio

Calculate the counts of numbers within predefined zones for a given sequence of numbers.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of numbers from which the method will count how many numbers fall into each zone.
- `zone_ranges` (List[Tuple[int, int]]): A list of tuples where each tuple contains two numbers representing the start and end of a zone range, defining the zones for categorizing the numbers.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `Tuple[int, ...]`: A tuple containing the count of numbers that fall within each specified zone.

#### Description:
This class method determines the distribution of the numbers in the input sequence across specified zones. It calculates the counts of numbers within predefined zones based on the provided number combination and zone ranges. Each zone is defined by a range, and the method counts how many numbers fall into each zone. The counts are returned as a tuple, with each element representing the count for a respective zone.

#### Example Usage:
```python
# Calculate the counts of numbers within predefined zones
number_combination = [10, 15, 20, 25, 30]
zone_ranges = [(0, 15), (16, 25), (26, 35)]
zone_counts = CalculateUtil.calculate_zone_ratio(number_combination, zone_ranges)
print(zone_counts)
```

### Class Method: calculate_big_small_ratio

Calculate the counts of numbers within predefined size ranges for a sequence of numbers.

#### Parameters:
- `number_combinations` (Iterable[int]): An iterable of numbers from which the method will count how many numbers fall into each size range.
- `big_small_ranges` (List[Tuple[int, int]]): A list of tuples where each tuple contains two numbers representing the start and end of a range, defining the size ranges for categorizing the numbers.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `Tuple[int, ...]`: A tuple containing the count of numbers that fall within each specified range or 'zone'.

#### Description:
This class method assesses how many numbers from the input sequence fall within each of the specified size ranges. Each range represents a 'zone', which could correspond to a concept like 'big' or 'small' numbers. It calculates the counts of numbers within predefined size ranges based on the provided number combinations and size ranges. The counts are returned as a tuple, with each element representing the count for a respective range or 'zone'.

#### Example Usage:
```python
# Calculate the counts of numbers within predefined size ranges
number_combinations = [10, 15, 20, 25, 30]
size_ranges = [(0, 15), (16, 25), (26, 35)]
size_counts = CalculateUtil.calculate_big_small_ratio(number_combinations, size_ranges)
print(size_counts)
```

### Class Method: calculate_road_012_ratio

Calculate the count of numbers within predefined zones (referred to as 'roads') for a given sequence of numbers.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of numbers from which the method will count how many numbers fall into each 'road' as defined by the ranges.
- `road_012_ranges` (List[tuple[int, ...]]): A list of range objects or sequences defining the 'roads'. Each element in this list corresponds to a different 'road', and the numbers in 'number_combination' are checked against these ranges to determine their counts.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `Tuple[int, ...]`: A tuple containing the count of numbers in each 'road'.

#### Description:
This class method determines how many numbers from the input fall within each of the specified ranges, where each range represents a 'road', which is a segment of the overall data set. It calculates the count of numbers within predefined zones for a given sequence of numbers based on the provided number combination and 'road' ranges. The counts are returned as a tuple, with each element representing the count for a respective 'road'.

#### Example Usage:
```python
# Calculate the count of numbers within predefined 'road' zones
number_combination = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
road_ranges = [(0, 3), (4, 6), (7, 9)]
road_counts = CalculateUtil.calculate_road_012_ratio(number_combination, road_ranges)
print(road_counts)
```

### Class Method: calculate_odd_even_ratio

Calculate the ratio of odd to even numbers within a given sequence of numbers.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of integers from which the method will count the number of odd and even numbers.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `Tuple[int, int]`: A tuple containing two elements; the first is the count of odd numbers and the second is the count of even numbers in the number_combination.

#### Description:
This method is designed to be called on the class itself rather than on an instance of the class. It can be used to analyze a collection of numbers (number_combination) and determine the count of odd and even numbers. It calculates the count of odd and even numbers within a given sequence of numbers based on the provided number combination. The counts are returned as a tuple, with the first element representing the count of odd numbers and the second element representing the count of even numbers.

#### Example Usage:
```python
# Calculate the ratio of odd to even numbers within a given sequence
number_combination = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
odd_even_counts = CalculateUtil.calculate_odd_even_ratio(number_combination)
print(odd_even_counts)
```

### Class Method: calculate_prime_composite_ratio

Calculate the ratio of prime to composite numbers in a sequence of numbers provided in the `number_combination`.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of numerical values from which the method will determine the count of prime (including 1) and composite numbers.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `Tuple[int, int]`: A tuple containing two elements; the first is the count of prime numbers (including 1) and the second is the count of composite numbers in the `number_combination`.

#### Description:
This method calculates the ratio of prime to composite numbers in a sequence of numbers provided in the `number_combination`. It determines which numbers are prime (including 1) and which are composite, and computes their counts. The counts are returned as a tuple, with the first element representing the count of prime numbers (including 1) and the second element representing the count of composite numbers.

#### Example Usage:
```python
# Calculate the ratio of prime to composite numbers within a given sequence
number_combination = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
prime_composite_counts = CalculateUtil.calculate_prime_composite_ratio(number_combination)
print(prime_composite_counts)
```

### Class Method: calculate_span

Calculate the span of a sequence of numbers provided in the `number_combination`. The span is defined as the difference between the maximum and minimum values in the set of numbers.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of numerical values from which the method will find the maximum and minimum values and calculate the difference (span) between them.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `int`: The span of the numbers in the `number_combination` as an integer. If the input contains floating point numbers, the span is cast to an integer before being returned.

#### Description:
This method calculates the span of a sequence of numbers provided in the `number_combination`. It finds the maximum and minimum values in the collection and calculates the difference (span) between them. The span is then returned as an integer. If the input contains floating-point numbers, the span is cast to an integer before being returned.

#### Example Usage:
```python
# Calculate the span of a sequence of numbers
number_combination = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
span = CalculateUtil.calculate_span(number_combination)
print(span)
```

### Class Method: calculate_sum_total

Calculate the total sum of a sequence of numbers provided in the `number_combination`. This method aggregates all the numerical values in the list or tuple passed as an argument and returns their sum.

#### Parameters:
- `number_combination` (Iterable[Union[int, float]]): An iterable of numerical values from which the method will calculate the sum of the values.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `Union[int, float]`: The sum total of the numbers in the `number_combination` as an integer or float, depending on the input values.

#### Description:
This method calculates the total sum of a sequence of numbers provided in the `number_combination`. It aggregates all the numerical values in the list or tuple and returns their sum. The sum total is returned as an integer or float, depending on the input values.

#### Example Usage:
```python
# Calculate the sum total of a sequence of numbers
number_combination = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
total_sum = CalculateUtil.calculate_sum_total(number_combination)
print(total_sum)
```

### Class Method: calculate_sum_tail

Calculate the last digit (tail) of the sum of a given number combination. The tail is the unit's place of the sum, which can be useful for certain types of numerical analysis or pattern recognition.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of numerical values from which the method will calculate the sum and return the last digit (tail) of the sum.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `int`: The last digit of the sum of the `number_combination` as an integer.

#### Description:
This method calculates the last digit (tail) of the sum of a given number combination. It takes a list or tuple of numerical values, calculates the sum of these numbers, and returns the last digit of this sum. The last digit is returned as an integer.

#### Example Usage:
```python
# Calculate the last digit of the sum of a sequence of numbers
number_combination = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
sum_tail = CalculateUtil.calculate_sum_tail(number_combination)
print(sum_tail)
```

### Class Method: calculate_weekday

Calculate the weekday number from a date string.

#### Parameters:
- `date` (str): A date string.
- `date_format` (str): The format of the date string. Defaults to '%Y-%m-%d'.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `int`: The weekday number where 1 represents Monday and 7 represents Sunday.

#### Description:
This method takes a date string and its format, and calculates the weekday number. The weekday number is returned, where 1 represents Monday and 7 represents Sunday.

#### Example Usage:
```python
# Calculate the weekday number from a date string
date_string = '2024-02-08'
weekday_number = CalculateUtil.calculate_weekday(date_string)
print(weekday_number)
```

### Class Method: calculate_ac

Compute the complexity of a given number combination. Complexity is defined as the number of distinct absolute differences between each pair of numbers in the combination, excluding the number of elements minus one.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of numerical values for which the complexity will be calculated.
- `kwargs` (Any): Additional keyword arguments that may be used for future extensions of the method.

#### Returns:
- `int`: An integer representing the complexity of the number combination.

#### Description:
This method computes the complexity of a given number combination. Complexity is defined as the number of distinct absolute differences between each pair of numbers in the combination, excluding the number of elements minus one. The complexity value is returned as an integer.

#### Example Usage:
```python
# Compute the complexity of a number combination
number_combination = [1, 3, 6, 10]
complexity = CalculateUtil.calculate_ac(number_combination)
print(complexity)
```

### Class Method: calculate_consecutive_numbers

Calculate the sequences of consecutive numbers in a given iterable of integers.

#### Parameters:
- `number_combination` (Iterable[int]): An iterable of integers to compute consecutive numbers from.
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `List[List[int]]`: A list of lists, each containing a sequence of consecutive numbers.

#### Description:
This method calculates the sequences of consecutive numbers in a given iterable of integers. It takes an iterable of integers and returns a list of lists, where each inner list contains a sequence of consecutive numbers.

#### Example Usage:
```python
# Calculate consecutive numbers from an iterable of integers
number_combination = [1, 2, 3, 5, 6, 7, 10, 11, 12]
consecutive_sequences = CalculateUtil.calculate_consecutive_numbers(number_combination)
print(consecutive_sequences)
```

### Class Method: calculate_repeated_numbers

Calculate the numbers that appear in all given iterables of integers (intersection).

#### Parameters:
- `number_combinations` (Iterable[Iterable[int]]): An iterable of iterables of integers to find common numbers.
- `window` (int): The number of recent periods to process. Defaults to 2.
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `List[int]`: A list containing the numbers that are common in all given iterables.

#### Description:
This method calculates the numbers that appear in all given iterables of integers, effectively finding the intersection of the sets. It takes an iterable of iterables of integers and returns a list containing the numbers that are common in all given iterables within the specified window.

#### Example Usage:
```python
# Calculate common numbers from multiple iterables of integers
number_combinations = [[1, 2, 3, 4], [2, 3, 4, 5], [3, 4, 5, 6]]
common_numbers = CalculateUtil.calculate_repeated_numbers(number_combinations, window=3)
print(common_numbers)
```

### Class Method: calculate_edge_numbers

Calculate 'edge numbers' which are present in consecutive iterables where each number from the first iterable is either one less or one more than the numbers in the following iterable.

#### Parameters:
- `number_combinations` (Iterable[Iterable[int]]): An iterable of iterables of integers to find 'edge numbers'.
- `window` (int): The number of recent periods to process. Defaults to 2.
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `List[int]`: A list containing the 'edge numbers'.

#### Description:
This method calculates 'edge numbers' which are present in consecutive iterables, where each number from the first iterable is either one less or one more than the numbers in the following iterable. It takes an iterable of iterables of integers and returns a list containing the 'edge numbers' within the specified window.

#### Example Usage:
```python
# Calculate 'edge numbers' from consecutive iterables of integers
number_combinations = [[1, 2, 3], [2, 3, 4], [5, 6, 7]]
edge_numbers = CalculateUtil.calculate_edge_numbers(number_combinations, window=3)
print(edge_numbers)
```

### Class Method: calculate_cold_hot_numbers

Calculate and return 'cold numbers' and 'hot numbers' from a series of number combinations.
'Cold numbers' are those that did not appear in the last 5 iterations,
and 'hot numbers' are those that appeared at least once in the last 5 iterations.

#### Parameters:
- `number_combinations` (Iterable[Iterable[int]]): An iterable of iterables of integers to analyze numbers.
- `all_numbers` (Iterable[int]): An iterable of all possible numbers that could appear.
- `window` (int): The number of recent periods to process. Defaults to 5.
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `Tuple[List[int], List[int]]`: A tuple containing two lists - the first with 'cold numbers' and the second with 'hot numbers'.

#### Description:
This method calculates and returns 'cold numbers' and 'hot numbers' from a series of number combinations. 'Cold numbers' are those that did not appear in the last 5 iterations, and 'hot numbers' are those that appeared at least once in the last 5 iterations. It takes an iterable of iterables of integers and an iterable of all possible numbers, and returns a tuple containing the 'cold numbers' and 'hot numbers' within the specified window.

#### Example Usage:
```python
# Calculate 'cold numbers' and 'hot numbers' from a series of number combinations
number_combinations = [[1, 2, 3], [4, 5, 6], [2, 3, 4], [7, 8, 9], [1, 2, 3]]
all_numbers = range(1, 10)
cold_numbers, hot_numbers = CalculateUtil.calculate_cold_hot_numbers(number_combinations, all_numbers, window=5)
print("Cold numbers:", cold_numbers)
print("Hot numbers:", hot_numbers)
```

### Class Method: calculate_omitted_numbers

Update and return the omission values for each number in all_numbers.

#### Parameters:
- `number_combinations` (Iterable[Iterable[int]]): A list of lists of integers representing past number draws.
- `all_numbers` (Iterable[int]): A list of all possible numbers that could appear.
- `window` (int): The number of recent periods to process. Defaults to 10.
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `Dict[int, int]`: A dictionary with numbers as keys and their omission values as values.

#### Description:
This method updates and returns the omission values for each number in all_numbers. It takes a list of lists of integers representing past number draws and a list of all possible numbers, and returns a dictionary with numbers as keys and their omission values as values within the specified window.

#### Example Usage:
```python
# Update and return the omission values for each number in all_numbers
number_combinations = [[1, 2, 3], [4, 5, 6], [2, 3, 4], [7, 8, 9], [1, 2, 3], [4, 5, 6], [7, 8, 9], [1, 2, 3], [4, 5, 6], [7, 8, 9]]
all_numbers = range(1, 10)
omission_values = CalculateUtil.calculate_omitted_numbers(number_combinations, all_numbers, window=10)
print("Omission values:", omission_values)
```

### Static Method: calculate_standard_deviation_welford

Calculates the standard deviation of a numeric sequence using Welford's method.

#### Parameters:

- `numeric_sequence (List[Union[int, float]]):` The sequence of numbers (integers or floats) for which the standard deviation is to be calculated.
- `decay_factor (Union[int, float]):` The decay factor for weighting recent values more heavily. Defaults to 0.95.

#### Returns:

- `float:` The standard deviation of the sequence. Returns 0 if the sequence contains fewer than two elements.

#### Description:

This method is an online algorithm designed to compute the standard deviation of a sequence of numbers iteratively, which can be useful for large datasets where all data cannot be loaded into memory at once.

#### Example Usage:

```python
# Update and return the omission values for each number in all_numbers
number_combinations = [1, 2, 3, 4, 5, 6]
sd = self.calculate_standard_deviation_welford(number_combinations)
```

### Abstract Method: calculate_winning_amount

Calculate the winning amount based on matching combinations.

#### Parameters:
- `winning_number_combination` (List[int]): Winning number combination.
- `purchase_number_combinations` (List[List[int]]): Purchase number combinations.
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `Tuple[float, int]`: A tuple containing the total winning amount and the count of winning combinations.

#### Description:
This abstract method calculates the winning amount based on matching combinations. It takes a winning number combination and a list of purchase number combinations, and returns a tuple containing the total winning amount and the count of winning combinations.

#### Example Usage:
```python
# Calculate the winning amount based on matching combinations
winning_number_combination = [1, 2, 3, 4, 5]
purchase_number_combinations = [[1, 2, 3, 4, 5], [6, 7, 8, 9, 10], [1, 2, 3, 11, 12]]
total_winning_amount, count_of_winning_combinations = CustomCalculator.calculate_winning_amount(winning_number_combination, purchase_number_combinations)
print("Total winning amount:", total_winning_amount)
print("Count of winning combinations:", count_of_winning_combinations)
```

## Class: AnalyzeUtil

Analyze based on multiple data.

### Abstract Method: analyze_same_period_numbers

Analyze same period number in the last period.

#### Parameters:
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `None`

#### Description:
This abstract method analyzes the same period number in the last period. It does not return any value.

#### Example Usage:
```python
# Analyze same period number in the last period
analyze_util = AnalyzeUtilImplementation()
analyze_util.analyze_same_period_numbers()
```

### Abstract Method: analyze_same_weekday_numbers

Analyze same weekday number in the last period.

#### Parameters:
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `None`

#### Description:
This abstract method analyzes the same weekday number in the last period. It does not return any value.

### Abstract Method: analyze_repeated_numbers

Analyze the number that appeared twice in the last two periods.

#### Parameters:
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `None`

#### Description:
This abstract method analyzes the numbers that appeared twice in the last two periods. It does not return any value.

### Abstract Method: analyze_edge_numbers

Analyze adjacent numbers, plus or minus 1 with the winning number issued in the previous period.

#### Parameters:
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `None`

#### Description:
This abstract method analyzes adjacent numbers, plus or minus 1 with the winning number issued in the previous period. It does not return any value.

### Abstract Method: analyze_cold_hot_numbers

Analyze numbers that have appeared in the last period and numbers that have not appeared in the last period.

#### Parameters:
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `None`

#### Description:
This abstract method analyzes numbers that have appeared in the last period and numbers that have not appeared in the last period. It does not return any value.

### Abstract Method: analyze_omitted_numbers

Analyze the omission statistics for numbers.

#### Parameters:
- `kwargs` (Any): Additional keyword arguments.

#### Returns:
- `None`

#### Description:
This abstract method analyzes the omission statistics for numbers. It covers various aspects such as the number of periods since the previous opening to the current period, average omission, maximum missed value, current omission, previous period omission, theoretical number, and desired probability. It does not return any value.





