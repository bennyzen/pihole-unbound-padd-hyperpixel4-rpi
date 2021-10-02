# pihole-unbound-padd-hyperpixel4-rpi
docker-compose stack with [PiHole](https://github.com/pi-hole/pi-hole), [Unbound](https://github.com/NLnetLabs/unbound), [PADD](https://github.com/pi-hole/PADD) with [Hyperpixel4](https://github.com/pimoroni/hyperpixel4) display for RaspberryPi

![image](https://user-images.githubusercontent.com/13304/133509651-1ac29500-c368-4ffa-978d-27c9160ee314.png)

## Setup

- Install Raspbian lite 32bit (64bit does not yet support hyperpixel. see https://github.com/pimoroni/hyperpixel4/issues/117)
- Make sure you provide a *fixed IP* for this device
- Setup docker and docker-compose
- Install bc and dig with `sudo apt install bc dnsutils`
- Install hyperpixel4 display (use https://github.com/pimoroni/hyperpixel4)
- Add these lines to your `~/.bashrc` 
```bash
# Run PADD
if [ "$TERM" == "linux" ] ; then
  while :
  do
    docker exec -it pihole bash /padd/padd.sh
    sleep 1
  done
fi
```
- Pull this repo
- Edit values in `docker-compose.yml`
- Start the stack with `docker-compose up -d`
- In PiHole under Settings > DNS set your Upstream DNS Server to `127.0.0.1#5335` and enable DNSSec
![image](https://user-images.githubusercontent.com/13304/133510101-f7c438c9-c24e-4657-992b-a0f7bc963cdc.png)

## Enable auto-login
To directly display your PiHole stats after each reboot, use `raspi-config` under `System Options -> Boot / Auto Login` and enable `Console Autologin`. A reboot is required.

## Adjust the font-size to fill the screen
The default terminal font was too small to fill the entire screen. You can change the font-size doing:
```bash
sudo dpkg-reconfigure console-setup
```
Now hit Enter two times and then on the font-selection screen select a font that is big enough for your eyes. PADD will adapt the amount of information that is shown automatically. The bigger the font, the lesser info is shown.

## Set as DNS
Depending on your network setup, you can now instruct your router to tell all clients to use PiHole as DNS. Or you can just configure the clients manually by entering its IP as DNS. 

## Test DNS performance
After you have successfully setup everything and started the stack, make sure you test the performance of the DNS by doing:
```
./dnsperftest/dnstest.sh
```
