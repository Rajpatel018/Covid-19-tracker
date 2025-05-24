# Covid-19-tracker
The COVID-19 Tracker API is a Python-based web application designed to fetch, process, and display real-time data about COVID-19 cases globally and by country. It leverages publicly available APIs to provide up-to-date statistics, helping users monitor the spread of the virus effectively.


import requests

def get_global_data():
    url = "https://disease.sh/v3/covid-19/all"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        print("\n🌍 Global COVID-19 Stats:")
        display_data(data)
    else:
        print("Error: Could not fetch global data.")

def get_country_data(country):
    url = f"https://disease.sh/v3/covid-19/countries/{country}"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        print(f"\n📍 COVID-19 Stats for {data['country']}:")
        display_data(data)
    else:
        print(f"Error: Could not fetch data for '{country}'. Check the country name.")

def display_data(data):
    print(f" Total Cases   : {data['cases']:,}")
    print(f" Recovered     : {data['recovered']:,}")
    print(f" Deaths        : {data['deaths']:,}")
    print(f" Last Updated  : {data['updated']} (Unix timestamp)\n")

def main():
    print("===== COVID-19 Tracker API using Python =====")
    while True:
        print("\n1. Global Stats")
        print("2. Country Stats")
        print("3. Exit")
        choice = input("Enter your choice (1/2/3): ")

        if choice == "1":
            get_global_data()
        elif choice == "2":
            country = input("Enter country name (e.g., India): ")
            get_country_data(country)
        elif choice == "3":
            print("Exiting COVID-19 Tracker. Stay Safe!")
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
