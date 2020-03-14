# Prometheus &amp; Grafana on a Raspberry Pi
Using docker-compose to run Prometheus &amp; Grafana on a Raspberry Pi

## Install Docker & docker-compose

Instructions from [dev.to](https://dev.to/rohansawant/installing-docker-and-docker-compose-on-the-raspberry-pi-in-5-simple-steps-3mgl)

* Install docker `curl -sSL https://get.docker.com | sh`
* Add permissions for user pi to run docker commands `sudo usermod -aG docker pi`
* Install docker-compose `sudo pip3 install docker-compose`

## Run Prometheus & Grafana

* Build and run `docker-compose up --build`
* Or run in the background `docker-compose up -d`
* Prometheus should now be running at `http://raspberrypi.local:9090`
* Grafana should now be running at `http://raspberrypi.local:3000`

### Credit
Thanks to [finestructure](https://github.com/finestructure/blogpost-prometheus) for the base.

