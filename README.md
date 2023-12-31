# Building a Matter Accessory Device based on Silicon Labs EFR32xG24 Explorer Kit Board (EK2703A) with a Mikro Elektronika UART 1-WIRE CLICK and a Dallas Semiconductor DS18B20 temperature sensor.
### Author: [Olav Tollefsen](https://www.linkedin.com/in/olavtollefsen/)

## Introduction

This article shows how to modify the "Matter - SoC Sensor over Thread" example project with support for a 1-Wire Dallas Semiconductor DS18B20 temperature sensor conneected to a Mikro Elektronika UART 1-WIRE CLICK attached to the Silicon Labs EFR32xG24 Explorer Kit Board (EK2703A).

This article is based on Silicon Labs Gecko SDK version 4.3.2 with Silicon Labs Matter 2.2.0.

<img src="./images/xg24-ek2703a.png" alt="Silicon Labs EFR32xG24 Explorer Kit Board" width="200" height="170"/>

<img src="./images/uart-1-wire-click-thickbox_default-2.jpg" alt="Mikro Elektronika UART 1-WIRE CLICK" width="200" height="170"/>

### What you will need

- A PC running Windows as the development workstation.
- Install Simplicity Studio V5 from Silicon Labs.
- Silicon Labs EFR32xG24 Explorer Kit Board (EK2703A).
- Mikro Elektronika UART 1-WIRE CLICK
- Dallas Semiconductor DS18B20 temperature sensor

This article assumes that you have already installed Simplicity Studio V5 and the Gecko SDK 4.4.0

## Mount the Mikro Elektronika UART 1-WIRE CLICK

When mounting the Mikro Elektronika UART 1-WIRE CLICK on the Silicon Labs EFR32xG24 Explorer Kit Board make sure it's oriented correctly according to this illustration:

![mikroBUS Add-on Board Orientation](./images/mikrobus-board-orientation.png)

## Create the initial project based on the "Matter - SoC Sensor over Thread" example project

Start by creating a new project in Simplicity Studio V5 by selecting the "Matter - SoC Sensor over Thread" example project and click "Create":

![Matter - SoC Sensor over Thread Example Project](./images/matter-sensor-thread-example-project.png)

This is a good starting point as it already implements a fully functional Matter over Thread device.

## Change the default sensor type

When you create the sensor project it defaults to Occupancy Sensor. To switch between
the sensors, uninstall the 'Matter Occupancy Sensor'/current sensor component and install the
respective sensor component to enable it. One sensor component should be enabled for the app to build.

Open the .slcp file in your project and select "SOFTWARE COMPONENTS".

Navigate to "Silicon Labs Matter v2.2.0->Platform->Sensors:

![Sensor Components](./images/platform-sensor-components.png)

Select the "Matter Temperature Sensor" component and click "Install".

When asked click on "Replace Matter Occupancy Sensor with Matter Temperature Sensor":

![Replace Matter Occupancy Sensor](./images/replace-occupancy-sensor-component.png)

Select "Temperature Sensor Support" and click "Install".

## Add USUART support for the Mikro Elektronika UART 1-WIRE CLICK

Open the .slcp file in your project and select "SOFTWARE COMPONENTS".

Locate "Services->IO Stream->Driver->IO Stream: USART", select it and click "Install"

![IO Stream: USART](./images/io_stream_usart_install.png)

Select the name "mikroe" and click Done.

![Instance "mikroe"](./images/create-uart-instance.png)

Select the "mikroe" instance and click "Configure"

![Instance "mikroe"](./images/mikroe-instance-configure.png)

Change the Baud Rate to 9600 and the CTS and RTS to None.

## Turn off C++ "No RTTI" option

In order to use some C++ language features (like dynamic_cast) you may need to turn off the "No RTTI" option.

![Instance "mikroe"](./images/no-rtti.png)
