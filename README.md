## Preparation and install software

1. Install nodejs 'https://nodejs.org/en/download/'
2. Install mountebank 'npm install -g mountebank'

## Start mountebank

You can start mountebank by command 'mb' but this is empty of mountebank.

If you already have config file of imposter so you can use the below command to start mountebank with your config.
```bash
mb --configfile ./imposters.ejs --allowInjection --loglevel debug
```
or you can run by use script.
```bash
./start_mb_local.sh
```

## Test request mountebank with Postman

Import share link of Postman then test request it.

Postman share link

`https://www.getpostman.com/collections/c26a7f62b8f063a4c29c`
