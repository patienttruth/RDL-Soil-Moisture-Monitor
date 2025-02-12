After a fellow student asked the question about monitoring soil moisture @ various depths near a construction site I had an idea. Perhaps it can be done with some IOT (Internet of Things) sensors and Open Source Software. 

After a little research I came up with a system that should work for around $100-$250 depending on your exact needs. I found the Ecowitt WH51L soil moisture sensor with a 1 meter cord which broadcasts a signal on the 915 MHz frequency that can be picked up by a RTL-SDR. A SDR is a "software defined radio", a USB interface to monitor radio communications. The WH51L sensor probe is rated to IP 68 and the device housing to IP66, so they don't need protection, but could be installed on a stake and/or under a 5 gallon bucket.

Ecowitt sells a "gateway" which can upload the data to the cloud, however it requires internet access which may not be available in the field. This gateway is likely the easiest way to start collecting data, and assuming there is internet available, would be the most "turnkey reliable".

Alternatively, you could set up a Raspberry Pi (or similar) along with a RTL-SDR with the RTL 433 software. The software would be programmed to collect the data and dump it into a spreadsheet which would be collected periodically. This approach takes some initial setup by someone who can navigate Linux, and until it is tested in a given configuration could not be considered "reliable".

The Pi and SDR would be housed somewhere within radio distance (100m in open areas) of the sensor/s and powered by an extension cord and/or battery backup.

While I haven't tested this configuration and don't guarantee it will work at all, I do use a RTL-SDR to monitor a home weather station and it has been reliable.

Sensor: 
- [Ecowitt WH51L Wireless Soil Moisture Meter with 1M PVC Wire – Soil Sen](https://shop.ecowitt.com/collections/soil-sensor/products/wh51l) - $50
	- Manual - [osswww.ecowitt.net/uploads/20240112/WH51L Manual.pdf](https://osswww.ecowitt.net/uploads/20240112/WH51L%20Manual.pdf)

Data Recording Options:
- Tied to Ecowitt Cloud - [GW1200 IOT Wi-Fi Gateway with Built-in Temperature/Humidity/Barometric](https://shop.ecowitt.com/products/gw1200?pr_prod_strat=pinned&pr_rec_id=615068c78&pr_rec_pid=8170601414818&pr_ref_pid=8102864191650&pr_seq=uniform) - $32
- Self Hosted / Doesn't require internet, however requires some skill / troubleshooting to initially setup.
	- Hardware
		- Radio Interface ~$20-40 [About RTL-SDR](https://www.rtl-sdr.com/about-rtl-sdr/)
			- Need external antenna & USB Extension cord if not present in kit
		- Raspberry Pi ~ $30-100 depending on model
		- Battery Backup?
	- Software - Free and Open Source
		- [GitHub - merbanan/rtl\_433: Program to decode radio transmissions from devices on the ISM bands (and other frequencies)](https://github.com/merbanan/rtl_433)
			- RTL 433 connects to the USB device and decodes the transmissions it receives.
			- RTL 433 can output to a CSV for recording and analysis
			- Note - RTL 433 appears to support the "Ecowitt WH51L", based on its explicit support of the "Ecowitt WH51" which is a shallow depth version. There is a small chance there would be an issue.
	- Related Guides
		- [Low-Cost 433Mhz Sensor Network with rtl\_433 on Raspberry Pi :: apalrd's adventures](https://www.apalrd.net/posts/2021/rtl433/)
		- [RTL\_433: Output to terminal & write to file : r/RTLSDR](https://www.reddit.com/r/RTLSDR/comments/kb9luh/rtl_433_output_to_terminal_write_to_file/)
