# <bindingName> Binding

This binding is for monitoring MPPT Solarcharger from Victron Energy VRM API.

To install vrmlogger look at [this howto](https://github.com/victronenergy/venus/wiki/raspberrypi-install-venus-packages).

## Supported Things

- [VictronEnergyVRM SolarCharger](https://www.victronenergy.com/solar-charge-controllers) (Thing type `sc`)

Only tested with BlueSolar MPPT 100/30

## Discovery

Auto-Discovery has not implemented yet.


## Thing Configuration

The easiest way to configure a Thing (VictronEnergyVRM SolarCharger - `sc`) is via PaperUi. But it is also possible via Thing-File (see below).

| Configuration Parameter | Required | Default | Description                                         |
|-------------------------|----------|---------|-----------------------------------------------------|
| username                | X        |         | Your VRM Username                                   |
| password                | X        |         | Your VRM Password                                   |
| installation-id         | X        |         | ID of your Installation in VRM                      |
| instance-id             | X        | 288     | ID of the Instance in VRM                           |

You can find your Installation-Id if you are logged in to VRM [Portal](https://vrm.victronenergy.com/) in the URL. Click on your Installation. The URL should look like [https://vrm.victronenergy.com/installation/###ID###/dashboard](https://vrm.victronenergy.com/installation/###ID###/dashboard) Between /installation/ and /dashboard should be your ID.

The correct Instance-ID you see also in [Portal](https://vrm.victronenergy.com/) at Menu "Advanced" behind the title in [###ID###] for example "Solar Charger Summary [288]"

## Channels

| Channel  | Item Type | Description                                    |
|----------|-----------|------------------------------------------------|
| ScV      | Number    | Solarcharger Battery Voltage                   |
| ScS      | String    | Solarcharger Charge state                      |
| YT       | Number    | Solarcharger Yield Today                       |
| YY       | Number    | Solarcharger Yield Yesterday                   |
| ScW      | Number    | Solarcharger Battery Watts                     |

## Full Example

### victronenergyvrm.things:

```
Thing victronenergyvrm:sc:myvrmsc [username="yourvrm@email.de", password="securepasswd", installation-id=12345, instance-id=288]
```

### victronenergyvrm.items:

```
Number ScV "Solarcharger Battery Voltage [%.2f V]" {channel="victronenergyvrm:sc:myvrmsc:ScV"}
String ScS "Solarcharger Charge State" {channel="victronenergyvrm:sc:myvrmsc:ScS"}
Number YT "Solarcharger Yield Today [%.2f KWh]" {channel="victronenergyvrm:sc:myvrmsc:YT"}
Number YY "Solarcharger Yield Yesterday [%.2f KWh]" {channel="victronenergyvrm:sc:myvrmsc:YY"}
Number ScW "Solarcharger Power [%d W]" {channel="victronenergyvrm:sc:myvrmsc:ScW"}
```

## Example Installation in my Camper

I'm using this binding to monitor data of my CamperVan Solar Installation which I described [here](http://thejollyjumper.de/2018/10/18/elektrik/)
