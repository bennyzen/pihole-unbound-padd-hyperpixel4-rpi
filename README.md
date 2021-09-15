# pihole-unbound-padd-hyperpixel4-rpi
docker-compose stack with [PiHole](https://github.com/pi-hole/pi-hole), Unbound, [PADD](https://github.com/pi-hole/PADD) with Hyperpixel4 display for RaspberryPi

![image](https://user-images.githubusercontent.com/13304/133509651-1ac29500-c368-4ffa-978d-27c9160ee314.png)

## Setup

- Install Raspbian lite
- Make sure you provide a *fixed IP* for this device
- Setup docker and docker-compose
- Install hyperpixel4 display
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
- In PiHole under Settings > DNS set your Upstream DNS Server to `127.0.0.1#5335`
![image](https://user-images.githubusercontent.com/13304/133510101-f7c438c9-c24e-4657-992b-a0f7bc963cdc.png)


## Test DNS performance
After you have successfully setup everything and started the stack, make sure you test the performance of the DNS by doing:
```
./dnsperftest/dnstest.sh
```
