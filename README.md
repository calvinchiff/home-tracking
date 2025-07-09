# Smart Water Level Monitor

Smart Water Level Monitor is a fullstack embedded & IoT project that measures the water level in a tank using an ultrasonic sensor and displays the data locally and remotely.
The receiver also displays weather, and is designed to support other features in the house in the future.

The system is split into 4 components:

- A low-power **STM32 sensor node** with an ultrasonic sensor and an antenna, powered by battery. It transmits the water level once per hour.
- A **STM32 receiver node** with reception antenna and an e-ink display. It forwards data to a local Raspberry Pi via Wifi using WizFi360 module.
- A **Python API backend** running on the Raspberry Pi, storing incoming data in a SQL database.
- A **React frontend** served on the local network to visualize current and historical water levels.

---

## Project Structure

/
├── sensor/ # STM32 sensor code (C++) – ultrasonic & radio TX
├── receiver/ # STM32 receiver code (C++) – radio RX, e-ink, Raspberry link
├── api/ # Python backend (FastAPI/Flask) + SQL database
├── frontend/ # React frontend interface
├── docker-compose.yml # Container orchestration for local deployment
├── .github/workflows/ # CI/CD pipeline with GitHub Actions
└── README.md # Project overview

---

# Sensor

> Code for the STM32 sensor node measuring water level and sending data periodically.

- Language: C/C++
- Modules: Ultrasonic sensor (HC-SR04), CC1101 915MHz module
- Power: Battery-powered, low-power sleep between transmissions

---

# Receiver

> STM32-based receiver with display and Raspberry Pi link.

- Language: C/C++
- Modules: e-ink display, CC1101 915MHz module, WizFi360
- Displays and Sends received data to Raspberry over Wi-Fi using HTTP requests
- Displays weather and other houses data in the future

---

# API

> Lightweight Python server running on Raspberry Pi, storing and exposing water level data.

- Stack: Python (FastAPI + SQLModel + PostgreSQL)
- Features: REST API for storing and retrieving sensor data

---

# Frontend

> Web interface accessible from the local network to monitor water levels.

- Stack: React, Tailwind CSS
- Features: Real-time level display, historical graph

---

# Deployment

The full system is containerized using Docker and deployed locally on a Raspberry Pi.  
A GitHub Actions workflow builds and pushes the backend and frontend images,  
while **Watchtower** ensures automatic updates by monitoring the container registry.

---

# License

MIT
