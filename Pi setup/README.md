# PiRacer
### Hardware Setup:
- [PiRacer Standard](https://www.waveshare.com/piracer-ai-kit.htm)
- [Raspberry pi 4 Model B](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/)
- [Raspbian OS Lite 64bit](https://downloads.raspberrypi.org/raspios_lite_arm64/images/) (2023-05-03 release)
- [2-Channel Isolated CAN FD Expansion HAT](https://www.waveshare.com/2-ch-can-fd-hat.htm)
- [7.9inch Capacitive Touch Screen](https://www.waveshare.com/7.9inch-hdmi-lcd.htm) (optional)

### Raspberry Pi Configuration:
Run `raspi-config` in terminal
- Wifi
- SSH

### Install Dependencies:
- **python3**
	```
	sudo apt update
	sudo apt install \
		python3 \
		python3-dev \
		python3-setuptools \
		python3-venv
	```
- **piracer-py**
	#### Install following packages
	```
	sudo apt install \
		gcc \
		v4l-utils \
		i2c-tools \
		raspi-config \
		libopencv-dev
	```
	#### Setup periphery
	> Use **raspi-config** tool to enable the following peripherals:
	> i2c: Interface Options > I2C
	> camera: Interface Options > Camera 
	> Afterwards, reboot
	> ```
	> sudo reboot
	> ````

	#### Install piracer-py package
	```
	mkdir my_piracer
	cd my_piracer
	```
	> From here, virtual environment installation is recommneded.
	> ```
	> #Create virtual environment
	> python -m venv {your_venv_name}
	>
	> #Activate virtual environment
	> source {your_venv_name}/bin/activate
	> ```

	```
	pip install piracer-py
	```
	#### Example
	```
	import time
	from piracer.vehicles import PiRacerPro

	if __name__ == '__main__':

	    piracer = PiRacerPro()
	    # piracer = PiRacerStandard()

	    # Forward
	    piracer.set_throttle_percent(0.2)
	    time.sleep(2.0)

	    # Brake
	    piracer.set_throttle_percent(-1.0)
	    time.sleep(0.5)
	    piracer.set_throttle_percent(0.0)
	    time.sleep(0.1)

	    # Backward
	    piracer.set_throttle_percent(-0.3)
	    time.sleep(2.0)

	    # Stop
	    piracer.set_throttle_percent(0.0)

	    # Steering left
	    piracer.set_steering_percent(1.0)
	    time.sleep(1.0)

	    # Steering right
	    piracer.set_steering_percent(-1.0)
	    time.sleep(1.0)

	    # Steering neutral
	    piracer.set_steering_percent(0.0)
	```
