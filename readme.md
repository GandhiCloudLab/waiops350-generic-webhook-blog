# Generic Webhook Probe to push Events in Watson AIOps AI Manager

This article explains about Installing and using the Generic Webhook Probe in IBM Watson AIOps AI Manager 3.5.0, to push events.

Installation scripts are available here [files](./files).

## 1. Update Properties

#### Update entitlement Keys

Update the below properties in `files/00-config.sh` file .

```
export ENTITLEMENT_KEY=eyJhbG...........................e4Zog

export WEBHOOK_PASSWORD=......
```

## 2. Install AI-Manager

#### 2.1. Login to OCP Cluster

Login to OCP cluster where AI-Manager is installed using  `oc login` command .

#### 2.2. Run the install script

Goto the `files` folder and Run the install script as like below.

```
cd files
sh 10-install.sh
```

- It would take around 5 minutes to complete the istallation. 
- The same script can be run again and again if the install stopped for any reason.

#### 2.3. Output
 
The installation would be completed and the output could be like this.

```
PROBE_WEBHOOK_URL=https://mywebhook-mb-webhook-cp4waiops.aaaaaaaa/probe/generic
```

You can use this link to push alerts.

## 3. Pusing Events

A Sample event is available here [files/data/my-event.json](./files/data/my-event.json).

#### 3.1. Run the script

Goto the `files` folder and Run the below script as like below.

```
sh 20-push-event.sh
```

#### 3.2. View Results

The Alert should have been created and can be seen in the WAIOPS console.

![webhook](./images/01-alert.png)

The Story could have been created like these.

![webhook](./images/02-story.png)
![webhook](./images/03-story-details.png)

#### 3.3. Event Data

The below fields are important.

```
      "SERIAL": 10001,
      "EventId": "bookinfo-ratings-down",
      "Node": "bookinfo-ratings",
      "Severity": 4,
      "Summary": "Ratings service is down and not reachable",
      "NetcoolEventAction": "insert",
      "Type": 1,

```

- The value 1 in the field `Type` represents issue/probelm.


## 4. Clearing Events

A Sample event is available here [files/data/my-event-clear.json](./files/data/my-event-clear.json).

#### 4.1. Run the script

Goto the `files` folder and Run the below script as like below.

```
sh 30-clear-event.sh
```

#### 4.2. View Results

The status of Alert and story should have been like the below in the WAIOPS console.

![webhook](./images/04-alert-clear.png)
![webhook](./images/06-story-clear.png)


#### 4.3. Event Data

The below fields are important for clearing.

```
      "NetcoolEventAction": "update",
      "Type": 2,
```

- The value 2 in the field `Type` represents resolution/clear.


## Reference

The script is based out of the following IBM documentations.

https://www.ibm.com/docs/en/cloud-paks/cloud-pak-watson-aiops/3.5.0?topic=integration-probe-sevone-npm-ai-manager

https://www.ibm.com/docs/en/cloud-paks/cloud-pak-watson-aiops/3.5.0?topic=reference-normalized-alert-mapping-rules
