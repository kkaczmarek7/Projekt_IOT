# Czujnik jakości powietrza – Smart Home

Projekt demonstracyjny systemu IoT, który symuluje działanie czujnika jakości powietrza w środowisku inteligentnego domu. Wykorzystuje chmurowe usługi Microsoft Azure do przesyłania, przechowywania i analizy danych. Umożliwia wizualizację pomiarów w Power BI.

---

## Zawartość projektu

- `azure_iot.py` – skrypt symulujący czujnik i wysyłający dane do Azure IoT Hub
- Obsługa danych środowiskowych: temperatura, wilgotnoś.
- Integracja z:
  - **Azure IoT Hub** – do komunikacji z urządzeniem
  - **Azure Cosmos DB** – do trwałego przechowywania danych
  - **Power BI** – do wizualizacji pomiarów

---

## Wymagania

- Python 3.7+
- Konto w Microsoft Azure
- Skonfigurowane:
  - Azure IoT Hub z urządzeniem `simulated-device`
  - Azure Cosmos DB z bazą `iotdata` i kontenerem `sensordata`
  - Routing wiadomości z IoT Hub do Cosmos DB
- Power BI Desktop do wizualiacji danych.



 Krok 1: Utwórz projekt w Pythonie
1.1. Utwórz folder projektu
mkdir AzureIoTSimulator
cd AzureIoTSimulator

1.2. Utwórz plik symulatora
Utwórz plik azure_iot.py z poniższą zawartością:
import time
import random
import json
from azure.iot.device import IoTHubDeviceClient, Message

# Wklej swój connection string tutaj
CONNECTION_STRING = "TU_WKLEJ_CONNECTION_STRING_Z_AZURE_IOT_HUB"

def simulate_sensor_data():
    temperature = round(random.uniform(20.0, 30.0), 2)
    humidity = round(random.uniform(30.0, 60.0), 2)
    return {
        "deviceId": "simulated-device",
        "temperature": temperature,
        "humidity": humidity,
        "timestamp": time.strftime("%Y-%m-%dT%H:%M:%SZ", time.gmtime())
    }

def main():
    print("Łączenie z IoT Hub...")
    client = IoTHubDeviceClient.create_from_connection_string(CONNECTION_STRING)

    try:
        while True:
            data = simulate_sensor_data()
            message = Message(json.dumps(data))
            message.content_encoding = "utf-8"
            message.content_type = "application/json"
            client.send_message(message)
            print(f"Wysłano: {data}")
            time.sleep(15)
    except KeyboardInterrupt:
        print("Zatrzymano symulator")
    finally:
        client.shutdown()

if __name__ == "__main__":
    main()


 Krok 2: Zainstaluj bibliotekę azure-iot-device
Jeśli nie masz jeszcze środowiska, utwórz je:
python -m venv venv
source venv/bin/activate  # Na Windows: venv\Scripts\activate

Zainstaluj bibliotekę:
pip install azure-iot-device


 Krok 3: Skonfiguruj Azure (jak poprzednio)
Upewnij się, że masz:
IoT Hub z urządzeniem simulated-device


Cosmos DB z bazą iotdata i kontenerem sensordata


Routing z IoT Hub do Cosmos DB (routing message → endpoint Cosmos DB)



 Krok 4: Uruchom symulator
W terminalu w folderze projektu:
python azure_iot.py

Powinieneś widzieć w konsoli dane wysyłane co 15 sekund.

 Krok 5: Sprawdź dane w Azure
Wejdź w Cosmos DB → Data Explorer


Otwórz iotdata → sensordata i sprawdź przychodzące dane



 Krok 6: Wizualizacja w Power BI
Otwórz Power BI Desktop → Get Data → Azure Cosmos DB


Wprowadź URI i Primary Key (z zakładki Keys w portalu)


Wybierz bazę iotdata i kontener sensordata


Załaduj dane i twórz wizualizacje (np. wykresy temperatury i wilgotności)
