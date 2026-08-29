name: Build ESP8266 Binary

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Arduino CLI
        uses: arduino/setup-arduino-cli@v2

      - name: Install ESP8266 Core and Libraries
        run: |
          arduino-cli core update-index --additional-urls https://arduino.esp8266.com/stable/package_esp8266com_index.json
          arduino-cli core install esp8266:esp8266 --additional-urls https://arduino.esp8266.com/stable/package_esp8266com_index.json
          arduino-cli lib install "Adafruit GFX Library"
          arduino-cli lib install "Adafruit SSD1306"

      - name: Compile Sketch
        run: |
          mkdir -p build
          arduino-cli compile --fqbn esp8266:esp8266:nodemcuv2 --output-dir ./build .

      - name: Upload Binary
        uses: actions/upload-artifact@v4
        with:
          name: ZeroTwin-build
          path: build/*.bin
