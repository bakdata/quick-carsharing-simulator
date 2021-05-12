# Quick Carsharing Simulator

The simulator is based on [OSRM](http://project-osrm.org/). In the first step, we generate the data and write it to
files:

```shell
cd ./simulator
mkdir ./data
python -m car_sharing_simulator.vehicles_generator
python -m car_sharing_simulator.status_generator
```

There should be two files named `vehicles.json` and `status.jsonl` in the `./data/` directory. Start with
ingesting all vehicles:

```
curl -X POST --url <QUICK-HOST-ADDRESS>/ingest/vehicle \
    --header 'content-type: application/json' \
    --header 'X-API-Key:<API-KEY>' \
    --data "@./data/vehicles.json"
```

Ingestion of new status events can be started with `python -m car_sharing_simulator.status_generator`. The script
expects the following environment variables:

| Name               | Example                     | Required          |
|--------------------|-----------------------------|-------------------|
| QUICK_API_KEY      | W9tK8edVnXXa1gMyFVVh        | Yes               |         
| QUICK_HOST         | https://demo.d9p.io/ingest  | Yes               |
| QUICK_STATUS_TOPIC | status                      | Yes               |
| QUICK_NUM_UPDATES  | 200                         | No (default: 200) |




