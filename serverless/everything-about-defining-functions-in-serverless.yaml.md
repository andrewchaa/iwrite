# Everything about defining functions in serverless.yaml

Under `functions` section, you define your lambda functions. 

### Simple function that simply has http event.

```yaml
functions:
  listAnnouncements:
    handler: KeidApis.Apis::KeidApis.Apis.Controllers.AnnouncementsController::List
    package:
      artifact: bin/Release/netcoreapp3.1/package.zip
    events:
      - http:
          path: announcements
          method: get

```

I used `Controller` convention as I'm used to ASP.NET core structure. 

The `handler`'s format is `[Assembly Name]::[Full Name of the Class]::[Method Name]` 

| Valule | Description |
| :--- | :--- |
| KeidApis.Apis | the name of the assembly |
| KeidApis.Apis.Controllers.AnnouncementsController | the full class name |
| List | the method name |



### HTTP uri with request parameters

You can define request parameters, so that the function can parse a part of the uri and use it as parameter.

```yaml
  updateWarranty:
    handler: Navien.Installers.Lambdas::Navien.Installers.Lambdas.Functions.RegistrationsController::WarrantyPut
    package:
      artifact: bin/release/netcoreapp2.1/deploy-package.zip

    events:
      - http:
          path: /registrations/{serialNumber}/warranty
          method: put
          reqeust:
            parameters:
              path:
                serialNumber: true
          cors: true
          private: true

```
