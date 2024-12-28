# WLED for Waveshare ESP32-S3-Zero

Just a working WLED flash image binary for ESP32-S3-Zero (2M RAM, 4M DIO flash).

If you want to give it a go for yourself, this is roughly the process that got me to a working flash image binary:
```
git clone https://github.com/Aircoookie/WLED.git
cd WLED
npm install
npm run build
~/.platformio/penv/bin/platformio run --environment esp32s3_4M_qspi
# (...or build in VS Code + PlatfomIO for esp32s3_4M_qspi)
cd WLED/.pio/build/esp32s3_4M_qspi
esptool.py --chip=esp32s3 merge_bin --flash_size=4MB --flash_mode=qio --flash_freq=40m --output=flash.bin 0x0 bootloader.bin 0x8000 partitions.bin 0x10000 firmware.bin
esptool.py --chip esp32s3 -p /dev/cu.usbmodem141201 -b 460800 --before=default_reset --after=hard_reset write_flash --flash_mode dio --flash_freq 80m --flash_size detect 0 flash.bin
```
