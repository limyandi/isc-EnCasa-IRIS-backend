# Project Title

EnCasa (Logistics Community Project) Built with InterSystems IRIS

### Prerequisites

```
1. InterSystems Studio (https://download.intersystems.com/download/login.csp)
```

## Getting Started

1. To Deploy the project, open `InterSystems Studio` and import both cloned XML files by navigating to `Tools->Import Local`. N.B. Create one namespace for each cloned XML data.
2. Go to IRIS Management Portal and create a new Web Application `System Administration=>Security=>Applications=>Web Applications=>Create New Web Applications`. Call it '/logistics' (choose the namespace that you used to import 'EnCasa-Dev.xml' file), and for the enable section, choose REST Radio Button and Put in REST.Logistics.disp as the dispatch class (keep all of the rest options).
3. Create another web application, call it '/fileserver', (choose the namespace that you used to import the 'EnCasa-FileServer.xml' file), and for the enable section, choose REST Radio Button and Put in Fileserver.Broker as the dispatch class (keep all of the rest options).
4. Populate all the new Communities with the following POST Request:
{{YOUR_IRIS_INSTANCE_SERVER}}/logistics/communities
The Body Request: [communities.json](communities.json)

OPTIONAL:
To Use the Email Utility, you will have to go to IRIS management portal and set up the credentials.


5. Once you are in Management Portal, navigate to `Interoperability=>Configure=>Production`. Or, if nothing exists, navigate to `Interoperability=>List=>Productions` and choose Logistics.CommunityLogisticsProject and open it. 
6. You should see the SendEmailNotification below Operations section, click that, and go to settings. 
7. Enable the settings, and then fill in:
```
SMTP Server: smtp.gmail.com
SMTP Port: 465
Credentials: {Create your own Credentials with your GMAIL account} (Navigate to "Interoperability=>Configure=>Credentials")
```
8. Create a SSL Configuration, name it anything. (Go back to Management Portal Homepage, Navigate to `System Administration=>Security=>SSL/TLS Configurations`. Test it (on the top left corner beside cancel button), putting in:
```
Server Host Name: smtp.gmail.com
Server Port: 465
```


### Testing

1. Using InterSystems IRIS, populate several of the possible entities.
```
do ##class(DAO.Populate).Populate()
```

2. Play with all of the data from several entities with these possible route

```
Register New User: POST: {{YOUR_IRIS_INSTANCE_SERVER}}/logistics/register with this sample payload:
{
    "email": "limoztry@gmail.com",
    "password": "Haha1221",
    "name": "limyandi",
    "appNotification": true,
    "emailNotification": true,
    "smsNotification": false,
    "phoneNumber": "2213412213",
    "communities": [
        9,7,2
    ]
}
Get Delivery by ID: GET: {{YOUR_IRIS_INSTANCE_SERVER}}/logistics/delivery/5
Create Delivery: POST: {{YOUR_IRIS_INSTANCE_SERVER}}/logistics/delivery with this sample payload:
{
    "date": "2019-09-24",
    "time": "22:32:41Z",
    "customerId": 2,
    "pickupAddress": "212 George St",
    "status": false,
    "timeTo": "23:08:48Z",
    "deliveryAddress": "242 Kent St"
}

Add Job as a Driver: POST: {{YOUR_IRIS_INSTANCE_SERVER}}/logistics/job with this sample payload:
{
    "pickupId":1, 
    "driverId": 3,
    "ETA": "2019-09-18T14:15:04Z"
}
```

## Acknowledgments

1. https://github.com/intersystems-ru/Cache-FileServer

