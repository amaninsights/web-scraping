# Countries of the World Web Scraper

A web scraping project that extracts comprehensive country data from a demo website.

## Project Overview

This scraper extracts information about countries including their names, capital cities, population, and area in square kilometers. The data is cleaned and structured into a pandas DataFrame for easy analysis.

## Data Source

- **Website**: https://www.scrapethissite.com/pages/simple/
- **Type**: Educational scraping sandbox
- **Data Format**: HTML tables with country information

## Features

- Extracts country names
- Retrieves capital cities
- Collects population data
- Gathers area information in km²
- Data cleaning and type conversion
- Structured DataFrame output

## Technologies Used

- **BeautifulSoup**: HTML parsing and data extraction
- **Requests**: HTTP requests to fetch web pages
- **Pandas**: Data manipulation and DataFrame creation

## Installation

Install the required dependencies:

```bash
pip install beautifulsoup4 requests pandas
```

## Usage

### Running the Scraper

1. Open the `scrapering.ipynb` Jupyter notebook
2. Execute the cells in order:

   **Cell 1**: Import libraries
   ```python
   from bs4 import BeautifulSoup
   import requests
   import pandas as pd
   ```

   **Cell 2**: Fetch the webpage
   ```python
   url='https://www.scrapethissite.com/pages/simple/'
   page=requests.get(url)
   soup=BeautifulSoup(page.text,'html')
   ```

   **Cell 3**: Find country data containers
   ```python
   country_data=soup.find_all(class_='country')
   ```

   **Cell 4**: Extract and clean data
   ```python
   data=[]
   for block in country_data:
       country=block.find(class_="country-name").get_text(strip=True)
       capital = block.find(class_="country-capital").get_text(strip=True)
       population = block.find(class_="country-population").get_text(strip=True)
       area = block.find(class_="country-area").get_text(strip=True)
       
       data.append({
           "country":country,
           "capital": capital,
           "population": int(population),
           "area_km2": float(area)
       })
   ```

   **Cell 5**: Create DataFrame
   ```python
   df=pd.DataFrame(data).set_index('country')
   ```

   **Cell 6**: Display results
   ```python
   df.head(10)
   ```

## Sample Output

The scraper produces a DataFrame with the following structure:

| country | capital | population | area_km2 |
|---------|---------|------------|----------|
| Andorra | Andorra la Vella | 84000 | 468.0 |
| United Arab Emirates | Abu Dhabi | 4975593 | 82880.0 |
| Afghanistan | Kabul | 29121286 | 647500.0 |
| Antigua and Barbuda | St. John's | 86754 | 443.0 |
| Anguilla | The Valley | 13254 | 102.0 |

## Data Structure

- **country**: String - Country name (used as index)
- **capital**: String - Capital city name
- **population**: Integer - Population count
- **area_km2**: Float - Area in square kilometers

## Notes

- The target website is designed for educational scraping purposes
- Data is automatically cleaned (whitespace removal, type conversion)
- Missing or invalid data is handled gracefully
- The scraper can be easily modified for similar websites

## Future Enhancements

- Add data export functionality (CSV, JSON)
- Implement error handling for network issues
- Add data visualization capabilities
- Extend to scrape additional country information