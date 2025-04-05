# Home Automation Setup

This repository contains my home automation configuration using:
- Home Assistant
- Frigate (with NVIDIA GPU acceleration)
- Zigbee2MQTT
- PhotoPrism
- InfluxDB

## Hardware Requirements
- NVIDIA RTX 4090 GPU
- Zigbee USB Stick
- IP Cameras (RTSP capable)

## Software Requirements
- Docker
- Docker Compose
- NVIDIA Container Runtime
- CUDA Drivers

## Installation

1. Clone this repository:
```bash
git clone https://github.com/physiii/automation.git
cd automation
```

2. Create necessary directories:
```bash
mkdir -p frigate/config
mkdir -p homeassistant/config
mkdir -p zigbee2mqtt/data
mkdir -p photoprism/storage
mkdir -p influxdb/data
mkdir -p influxdb/config
```

3. Start the services:
```bash
docker-compose up -d
```

## Configuration

### Frigate
- Using CPU-based object detection for stability
- Configured for 5 cameras at 640x360 resolution
- Detection optimized for person, car, and truck objects

### Home Assistant
- Integration with Frigate for camera feeds and object detection
- Zigbee device control through Zigbee2MQTT
- Data logging to InfluxDB

### PhotoPrism
- Photo management system
- Configured to scan specific directories for photos

## Maintenance

To update all containers:
```bash
docker-compose pull
docker-compose up -d
```

To view logs:
```bash
docker-compose logs -f [service_name]
```

## License
MIT License 