#

## Deploy Your Multi-Target Application (MTA)
```
https://developers.sap.com/tutorials/btp-app-cap-mta-deployment..html
```

### Generate MTA deployment descriptor (mta.yaml)

```bash
cds add mta
```

## Exclude CSV files from deployment

```yaml
build-parameters:
  before-all:
   - builder: custom
     commands:
      - npm install --production
      - npx -p @sap/cds-dk cds build --production
      - npx rimraf gen/db/src/gen/data
```

## Add Authorization and Trust Management service (XSUAA)
      
```yaml
modules:
      - name: cpapp-srv
      ...
      requires:
        - name: cpapp-db
        - name: cpapp-uaa
resources:
   ...
 - name: cpapp-uaa
   type: org.cloudfoundry.managed-service
   parameters:
     service: xsuaa
     service-plan: application
     path: ./xs-security.json
     config:
       xsappname: cpapp-${space}    #  name + space dependency
       tenant-mode: dedicated
       role-collections:
         - name: 'RiskManager-${space}'
           description: Manage Risks
           role-template-references:
             - $XSAPPNAME.RiskManager
         - name: 'RiskViewer-${space}'
           description: View Risks
           role-template-references:
             - $XSAPPNAME.RiskViewer

```      

## Build, deploy, and test mtar file

Build the MTA module from your project root folder:
```bash
mbt build -t ./
```

Deploy the module to your current Cloud Foundry space:
```bash
cf deploy cpapp_1.0.0.mtar
```