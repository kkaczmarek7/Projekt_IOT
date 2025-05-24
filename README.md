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
