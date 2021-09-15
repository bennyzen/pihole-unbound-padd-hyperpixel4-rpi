# pihole-unbound-padd-hyperpixel4-rpi
docker-compose stack with PiHole, Unbound, PADD with Hyperpixel4 display for RaspberryPi

- Install Raspbian lite
- Setup docker and docker-compose
- Install hyperpixel4 display
- Add these lines to your `~/.bashrc`
```bash
# Run PADD
# If we’re on the PiTFT screen (ssh is xterm)
if [ "$TERM" == "linux" ] ; then
  while :
  do
    docker exec -it pihole bash /padd/padd.sh
    sleep 1
  done
fi
```
- Pull this repo
- Start the stack with `docker-compose up -d`
