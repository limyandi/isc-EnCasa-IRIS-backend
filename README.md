# Project Title

EnCasa (Logistics Community Project) Built with InterSystems IRIS

## Getting Started

1. To Deploy the project, open `InterSystems Studio` and import both cloned XML files by navigating to `Tools->Import Local`. N.B. Create one namespace for each cloned XML data.
2. Go to IRIS Management Portal and create a new Web Application `System Administration=>Security=>Applications=>Web Applications=>Create New Web Applications`. Name it anything you like, For the enable, choose REST Radio Button and Put in REST.logistics.disp as the dispatch class (keep all of the rest options).
3. 



### Prerequisites

```
1. InterSystems Studio (https://download.intersystems.com/download/login.csp)
2. Populate all NSW Communities with the following POST Request:
{{YOUR_IRIS_INSTANCE_SERVER}}/logistics/communities
```
The Body Request: [communities.json](communities.json)

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

