# NeuroWeaves Wireless EEG Firmware

This repository contains the core firmware files used for the custom wireless EEG acquisition module developed for the NeuroWeaves study. The firmware configures the ADS1299 analog front-end, acquires low-amplitude biopotential signals, and streams EEG data wirelessly through Bluetooth Low Energy (BLE) to a handheld device or computer for monitoring and offline analysis.

## Purpose

The firmware was used to support wireless validation experiments in the NeuroWeaves study, including preclinical recordings with the custom wearable acquisition module. The wireless module primarily performs analog-front-end configuration, digitization, BLE packet transmission, and signal-strength/connection monitoring. Signal processing and quantitative analysis were performed offline using MATLAB.

## Included files

- `main.c`  
  Main application firmware. This file initializes the BLE stack, configures advertising and connection parameters, manages ADS1299 acquisition, monitors RSSI, and coordinates wireless data streaming.

- `ads1299-x.c`  
  ADS1299 driver implementation. This file handles SPI communication, ADS1299 register configuration, device initialization, and data acquisition from the analog front-end.

- `ble_eeg.c`  
  BLE EEG service implementation. This file defines BLE characteristics for ADS1299 configuration and EEG data transmission.

## Hardware platform

The firmware was developed for an nRF52-based wireless module integrated with an ADS1299 analog front-end. The ADS1299 was used for multi-channel electrophysiological signal acquisition, and BLE was used for wireless data transmission.

The wireless module was configured for EEG-band recordings and was used with NeuroWeaves electrodes during preclinical validation experiments.

## Key firmware functions

The firmware supports:

- ADS1299 initialization and register configuration
- SPI-based data acquisition from the ADS1299
- BLE advertising and connection management
- BLE EEG data streaming
- Connection-parameter optimization for higher-throughput transmission
- BLE transmit-power configuration
- RSSI monitoring for wireless-link quality assessment
- Packet transmission through custom EEG BLE characteristics

## Sampling and wireless transmission

For the experiments reported in the manuscript, the wireless acquisition system was configured to support EEG recording with sampling parameters selected to preserve physiologically relevant EEG-band activity. Wireless performance, including signal fidelity, RSSI stability, packet-loss rate, and battery operation, is described in the Supplementary Information.

## Build environment

This firmware was developed using the Nordic nRF52 software development environment and Nordic SoftDevice BLE stack. The code depends on Nordic SDK headers and drivers, including BLE stack, GATT, advertising, connection-parameter, GPIO, SPI, timer, and logging modules.

To build the firmware, the following additional project files are required:

- Nordic SDK source and header files
- SoftDevice configuration
- board-specific pin configuration
- `sdk_config.h`
- project makefile or IDE project file
- corresponding header files, including `ads1299-x.h` and `ble_eeg.h`

These dependencies are platform-specific and are not included in this minimal code package.

## Data analysis

This firmware only performs acquisition and wireless transmission. Offline signal processing, including filtering, time-frequency analysis, SNR quantification, and event-related analysis, was performed separately using MATLAB. The analysis code is provided separately through the Code Availability statement in the manuscript.

## Notes

This code package is provided to document the core firmware logic used for the NeuroWeaves wireless acquisition system. It is not intended as a standalone commercial software release. Additional board-specific files, pin maps, SDK dependencies, and build configuration files are required to compile and deploy the firmware on the original hardware.