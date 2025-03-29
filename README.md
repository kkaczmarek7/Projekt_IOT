# Inteligentny Czujnik Jakości Powietrza dla Smart Home

## Opis projektu

Projekt polega na stworzeniu inteligentnego czujnika jakości powietrza, który monitoruje poziom zanieczyszczeń (PM2.5, PM10), temperaturę i wilgotność w pomieszczeniu. Dane są przesyłane do chmury (Azure), gdzie są przechowywane, analizowane, a użytkownik otrzymuje powiadomienia oraz ma dostęp do historii pomiarów.

## Architektura

Projekt składa się z kilku głównych komponentów:

- **Urządzenie IoT (ESP32/Raspberry Pi)** – zbiera dane z czujników jakości powietrza.
- **Chmura (Azure IoT Hub, Azure Blob Storage, Azure Functions)** – odbiera dane, przechowuje je i analizuje.
- **Backend (REST API)** – pozwala na komunikację z chmurą i użytkownikami.
- **Frontend (opcjonalnie)** – pozwala użytkownikowi na monitorowanie jakości powietrza w czasie rzeczywistym.

## Technologie

- **Azure**: IoT Hub, Blob Storage, Functions
- **Python**: Do tworzenia symulatora urządzenia IoT
- **FastAPI/Node.js**: Backend API
- **MQTT/HTTP**: Protokół komunikacji między urządzeniem a chmurą
- **React.js/Vue.js** (opcjonalnie): Frontend do wizualizacji danych




