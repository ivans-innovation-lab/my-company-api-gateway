
This service requires 

- 'my-company-configuration-backingservice' (on staging and production)
- 'my-company-registry-backingservice' (on staging and production)
- 'rabbit-stage / rabbit-prod'

You can create it manually on PWS, or by running script:

```
cf api https://api.run.pivotal.io
cf auth EMAIL PASSWORD

cf target -o idugalic -s Stage
cf create-user-provided-service my-company-configuration-backingservice -p '{"uri":"https://stage-my-company-configuration-backingservice.cfapps.io"}'
cf create-user-provided-service my-company-registry-backingservice -p '{"uri":"https://stage-my-company-registry-backingservice.cfapps.io"}'
cf create-service cloudamqp lemur rabbit-stage


cf t -s Prod
cf create-user-provided-service my-company-configuration-backingservice -p '{"uri":"https://prod-my-company-configuration-backingservice.cfapps.io"}'
cf create-user-provided-service my-company-registry-backingservice -p '{"uri":"https://prod-my-company-registry-backingservice.cfapps.io"}'
cf create-service cloudamqp lemur rabbit-prod


```