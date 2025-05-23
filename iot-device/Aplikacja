import time
import random
import json
from azure.iot.device import IoTHubDeviceClient, Message

# Wklej swój connection string tutaj
CONNECTION_STRING = "HostName=myiothubbb.azure-devices.net;DeviceId=simulated-device;SharedAccessKey=HdypidSiW7bWCxHuwrSEz0kYFByDlquSFPPo3PFqQtk="

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
