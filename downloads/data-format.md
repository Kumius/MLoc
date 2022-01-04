# Data format (encrypted)

We publish the scanning results of malls in this dataset. The collectors use their smartphones to scan the features (e.g. BLE signals), and the logs are saved in the trace files. The path to each trace file is as follows.

```Shell
# The path to each trace file.
./site-id/floor/path_data_files/path-id.txt
# For example:
./5d2709bb03f801723c32852c/F1/path_data_files/5dca1cffe518c500069ebafc.txt
```

In each trace file, there are two parts of data: **meta data** and **scanned data**. The metadata contains the basic information of the collection (e.g., the site ID), and the scanned data refers to the fingerprint features we collect by smartphones. Please note that due to privacy considerations, we may delete (or change) some information in the public dataset.

### Meta Data

Each line of the meta data starts with ‘#’, and the meaning of each line is as follows. (Some data might be removed for privacy considerations.)

- startTime: the time stamp of when the collector started to scan the fingerprint.
- SiteID: the ID of the building.
    - FloorId: the ID of the floor.
- type: sensor information.
    - name: sensor name.
    - version: sensor version.
    - vendor: the vendor of the sensor.
    - resolution: the resolution of the sensor.
    - power: the power consumption of the sensor.
    - maximumRange: the measuring range of the sensor.
- VersionName: the version name of the collecting application.
    - VersionCode: the version ID of the collecting application.
- endTime: the time stamp of when the collector completed the fingerprint scan. (It usually appears in the end of the file).

### Scanned Data

Each line of the scanned data starts with a timestamp, and follows by the scanning result. The details are as follows.

- TYPE_ACCELEROMETER: the acceleration ($m/s^2$) in (x, y, z) direction, and the 4th value refers to the accuracy level of the accelerometer. Note that gravity is included in the acceleration.
- TYPE_ACCELEROMETER_UNCALIBRATED: the uncalibrated acceleration ($m/s^2$) in (x, y, z) direction, the correpsonding deviations in (x, y, z) direction, and the accuracy level.
- TYPE_BEACON: the information of the beacon, including the uuid, major_id, minor_id, transmission strength, received signal strength, estimated distance, Mac address, lastseen (pseudo data).
- TYPE_GYROSCOPE: the angular velocity ($rad/s$) in (x, y, z) direction, and the 4th value refers to the accuracy level of the gyroscope.
- TYPE_GYROSCOPE_UNCALIBRATED: the uncalibrated angular velocity ($rad/s$) in (x, y, z) direction, the correpsonding deviations in (x, y, z) direction, and the 4th value refers to the accuracy level of the gyroscope.
- TYPE_ROTATION_VECTOR: its format is the same to TYPE_GYROSCOPE, but the rotation is calculated based on sensor fusion.
- TYPE_MAGNETIC_FIELD: the magnetic field ($\mu T$) in (x, y, z) direction, and the 4th value refers to the accuracy level of the magnetometer.
- TYPE_MAGNETIC_FIELD_UNCALIBRATED: the uncalibrated magnetic field in (x, y, z) direction, the correpsonding deviations in (x, y, z) direction, and the 4th value refers to the accuracy level of the magnetometer.
- TYPE_WAYPOINT: the current position (x, y, z) of the collector (there might be deviations). Note that this can be regarded as the ground truth of the user’s position.
- TYPE_WIFI: The information of the WiFi, including the ssid, bssid, signal strength, frequency range, lastseen (pseudo data).