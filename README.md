docker-compose for heatsheet
============================

This is a docker-compose project for [HeatSheet](https://github.com/orangecoding/heatsheet) from orangecoding

> An overview for your Tado data.
> 
> Tado thermostats are an easy and comfortable way to turn any heater into a smart-heater. We're using them throughout our apartment to not worry about heating.
> 
> However as good as the hardware is, the software (still) lacks the ability to export data and show them on a yearly basis (or showing bigger time-windows than just a single day).
> 
> HeatSheet is changing this. It uses (unofficial) Tado API's, to get the data out of your account and displays them either as a chart or table view. Depending on the chosen granularity, you can analyse your heating behaviour much better, therefor safe money and maybe.. just maybe save the 🌍 by adapting your heating behaviours.

## Installation

1. Clone this project
2. cp `env` to `.env`
3. Edit `.env` to fit your needs
5. If you do't want to use InfluxDB comment out the service in `docker-compose.yml`and set `INFLUXDB_ENABLED=false`
5. `docker-compose build`
5. `docker-compose pull`
4. `docker-compose up -d`

If you need to change the heatSheet settings in `.env` or `docker-compose.yml` you first have to remove the `config.json` from `volumes/app` or you have to edit this file directly. Same with influxDB configuration.

## Upgrade from local installation

Stop containers and copy `db.json` to `volumes/app/config/` and restart

## Use InfluxDB at a later stage

If you did not use InfluxDB at the start but you want to use it at a later stage after db.json already has data, follow this guide:

1. create the config in `.env` (i.e. set `INFLUXDB_ENABLED=true` and generate the other settings)
2. `rm volumes/app/config/config.json` or change the settings there
3. probably best also to remove `volumes/influxdb`
4. `docker-compose up -d`
5. `docker-compose exec app node influxMigration.js`
