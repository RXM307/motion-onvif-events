# motion-onvif-events

A JS CLI tool that attempts to bridge the gap between your ONVIF camera's motion detection and Zoneminder.

Forked from [zmonvif-events](https://github.com/nickw444/zmonvif-events) to add Docker support.

## Why?
In a typical Zoneminder installation the server will do video processing to determine which frames have motion. Unfortunately this task is quite CPU intensive. 

Fortunately some ONVIF cameras have built in motion detection features, which notify subscribers when an event occurs. 

This tool connects to an ONVIF camera and subscribes to these messages. When the motion state changes, it uses Zoneminder's API to arm the selected monitor

## Install

```bash
npm install -g zmonvif-events
```

## Usage

```bash
zmonvif-events --help
usage: zmonvif-events [-h] -z ZM_BASE_URL -i ZM_MONITOR_ID -c HOSTNAME
                         [-u USERNAME] [-p PASSWORD]

Optional arguments:
  -h, --help            Show this help message and exit.
  -z ZM_BASE_URL, --zm-base-url ZM_BASE_URL
                        Base URL for the Zoneminder instance (with trailing
                        slash)
  -i ZM_MONITOR_ID, --zm-monitor-id ZM_MONITOR_ID
                        The ID of the monitor in Zoneminder
  -c HOSTNAME, --hostname HOSTNAME
                        hostname/IP of the ONVIF camera
  -u USERNAME, --username USERNAME
                        username for the ONVIF camera
  -p PASSWORD, --password PASSWORD
                        password for the ONVIF camera
```

**Example**

```bash
zmonvif-events \
      --zm-base-url http://my-zoneminder-instance.com/zm/ \
      --zm-monitor-id 1 \
      --hostname 192.168.1.55 \
      --username supersecretusername \
      --password dontshareme
```
```
[camera 1]: Started
[camera 1]: CellMotionDetector: Motion Detected: true
[9/1/2019, 5:33:39 PM] Setting camera 1 to state true
[camera 1]: CellMotionDetector: Motion Detected: false
[9/1/2019, 5:33:40 PM] Setting camera 1 to state false
[camera 1]: CellMotionDetector: Motion Detected: true
[9/1/2019, 5:33:42 PM] Setting camera 1 to state true
[camera 1]: CellMotionDetector: Motion Detected: false
```

## Docker

Environment variables
* `ZM_BASE_URL` - Base URL for the Motion instance (with trailing slash)
* `ZM_MONITOR_ID` - The ID of the camera in Motion
* `HOSTNAME` - hostname/IP of the ONVIF camera
* `USERNAME` - username for the ONVIF camera
* `PASSWORD` - password for the ONVIF camera
