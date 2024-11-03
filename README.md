# Getting Started

Welcome to your new project.

It contains these folders and files, following our recommended project layout:

File or Folder | Purpose
---------|----------
`app/` | content for UI frontends goes here
`db/` | your domain models and data go here
`srv/` | your service models and code go here
`package.json` | project metadata and configuration
`readme.md` | this getting started guide


## Next Steps

- Open a new terminal and run `cds watch`
- (in VS Code simply choose _**Terminal** > Run Task > cds watch_)
- Start adding content, for example, a [db/schema.cds](db/schema.cds).


## Learn More

Learn more at https://cap.cloud.sap/docs/get-started/.

##
cds build --production
cds watch

## Fiori Appliciation Info

In case the Application Info - incidents tab is closed:

Invoke the Command Palette - View → Command Palette or Command + Shift + P for macOS / Ctrl + Shift + P for Windows.

Choose Fiori: Open Application Info.

### Configure the SAP Authorization and Trust Management service

```
https://developers.sap.com/tutorials/prep-for-prod.html
```

```bash
cds add xsuaa --for production
```

{
  "name": "incident-management",
  "dependencies": {
      ...
      "@sap/xssec": "^x"
  },
  ...
  "cds": {
    "requires": {
      ...
      "[production]": {
        "db": "hana",
        "auth": "xsuaa"
      }
    ...
    }
  }
}

xs-security.json 

```json
"role-templates": [
    {
      "name": "support",
      "description": "generated",
      "scope-references": [
        "$XSAPPNAME.support"
      ],
      "attribute-references": []
    },
    {
      "name": "admin",
      "description": "generated",
      "scope-references": [
        "$XSAPPNAME.admin"
      ],
      "attribute-references": []
    }
  ]
  ```