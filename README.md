# <img src="https://github.com/jaymodi98/Sync-Ends/blob/master/images/bot.png" height="42" width="42"/> Sync Ends

## End development overheads

Software Engineering Project for CSC 510

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
![GitHub](https://img.shields.io/badge/language-python-blue.svg)
![GitHub contributors](https://img.shields.io/github/contributors/jaymodi98/Sync-Ends)
[![Build Status](https://travis-ci.com/jaymodi98/Sync-Ends.svg?branch=master)](https://travis-ci.com/jaymodi98/Sync-Ends)
<br>
![GitHub closed issues](https://img.shields.io/github/issues-closed-raw/jaymodi98/Sync-Ends)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/jaymodi98/Sync-Ends)
[![codecov](https://codecov.io/gh/jaymodi98/Sync-Ends/branch/master/graph/badge.svg?token=DP2AWTXOXL)](undefined)<br>
[![DOI](https://zenodo.org/badge/300105279.svg)](https://zenodo.org/badge/latestdoi/300105279)
![YouTube Video Views](https://img.shields.io/youtube/views/1Pd3Enj13m8?style=social)

Sync Ends is an automated bridge to sync service owners and service consumers. Every team has a single Postman collection that they use to test their APIs and share it across in their documentations. The backend team has to register their service on our application and we take care of the rest. Everytime there is a change in the way the API is called, we parse the changes and inform the API consumers. This way all the team members are informed about the changes and know exactly what to edit in their codebase. The Slack framework lets you concentrate on the **core** functionality you want to build without worrying about integration overheads.

[![Watch the video](https://github.com/jaymodi98/Sync-Ends/blob/master/images/screenshotpromo.png)](https://www.youtube.com/watch?v=1Pd3Enj13m8)

# Architecture Diagram
<img src="https://github.com/jaymodi98/Sync-Ends/blob/master/images/architecture.PNG" height="500" width="800"/>

## Features
|Feature|Description  |
|--|--|
|1-step service execution |```Simple 1-step CLI execution for Sync Ends service```|
|API Change Notification  |```Get notifications about changes made to the API in Postman along with detailed diff of changes```|
|Track Postman collection | ```Ability to track a Postman collection and get notifications```|
|Slack Bot Subscription   |``` Set frequency of notifications as well as customize Slack channel for updates``` |

## Patterns in the code

- We are using Composite and Layer pattern in the code. The Parser module parses the user input and passes the parsed data to the underlying layers. The `sync end service` accepts the data from the parser layer and sends the notification to Slack.
- The Collection object uses the Composite pattern where a Collection contains multiple EndPoints and each End Point has attributes such as URL, method type, name, etc.

## Documentation
### What is Sync Ends?

Please have a look at the point descriptions of each function/class through this [documentation file](https://github.com/jaymodi98/Sync-Ends/blob/master/docs/src/index.html) generated via `pdoc3`. To view this documentation, clone the repository and then open the linked file in the browser.

### Why use Sync Ends?
Sync ends is a productivity service that focuses on saving developer time by automating API changes to their consumers in real-time thus improving your team's productivity. 
Consider an API consumer using multiple APIs in their system. In this ever-changing world, it is impossible for the consumer to be updated with each and every API change. This is the problem that Sync Ends service addresses. The service is easy to install and this reduces the communication overhead on side of the API devs. So avoid crashes and jump on the Sync Ends bandwagon! :)

This version of sync ends is highly usable as it can be simply downloaded through PyPI. It is a single package which satisfies all your needs with clean documentation. Using  just a simple config file, you can start the service from terminal through our CLI interface. All your API's from the Postman collection will be fetched and their changes will be reflected as notifications in your slack channel.

<img src="https://github.com/jaymodi98/Sync-Ends/blob/master/src/meme.jpg" width=40% />

```Transcript(Hindi to English) - API can change anytime```

*Reference : Meme From TV Series [Mirzapur](https://www.google.com/search?q=mirzapur)*


### How to use Sync Ends?
#### Installation
```
pip install sync-ends
```
The code is deployed as a python package on PyPI which is a single step installation process.

#### Usage

1. The package is primarily run through a CLI (single step) for ease of use.

Run the following command with required parameters.
```
syncends  --config_file </path/to/your/local/config/file>
```
What is `--config_file`?
```
config_file - the configuration file used by the Sync Ends service
```
##### How to write the config_file? (format of the file should be `.json`)
```
{
    "postman_api_key": "<a>",
    "slack_token": "<b>",
    "trigger_interval": <c>,
    "collections": [
        {
            "collection_name": "<d>",
            "slack_channel": "<e>"
        }
    ]
}
```
where,
- `a`: postman api key generated using steps shown in setup
- `b`: slack token generated using steps shown in setup
- `c`: **[optional: default=10]** time (in seconds), after which application will check for api changes
- `d`: collection name from postman collections
- `e`: **[optional: default="general"]** slack channel in which notifications will be sent (must be a public channel)

#### What happens after this command is run?

This command is the entry point to a background process which fetches all the `Postman collections` using the `Postman API key` and posts a message through the `Slack bot token` configured in the `Slack channel` specified. The background service fetches the Postman collections every `trigger interval` seconds. This means that developer on changing the API in the Postman does not have to worry about notifying any API consumers of the change. That magic is done by our bot :)

## Experimentation Phase for Project 3

In the experiment phase, we will be planning to evaluate the performance improvement of the API consumer (tester) in a rapidly developing environment. The experiment is planned to be run in pairs where one person will act as a developer and the other will act as an API consumer (tester). The job of the developer will be to change API schemas in Postman which mocks the behaviour that a change has been made in the serving of API in the actual codebase. The job of the tester will be to monitor these changes and note them down which mocks the behaviour that the API consumer is now aware that a change needs to be made in the codebase where this API is used.

### It vs Not It

In the presence of our Sync Ends service, once the developer makes a change in the APIs in the Postman collection, the changes will be directly fetched from Postman and a Slack message will be sent in the channel with a detailed diff notifying the API consumer of this change. <br>

In the absence of our service, the developer will have to manually notify changes to the API consumer and if the developer forgets to do so, the API consumer will be unaware of API changes and this would mock the fact that the API consumer will have a crash when their application tries to call the updated API with old parameters.

### Idea for the Experimentation

The primary idea for the experiment is to provide the participants(lab rats) with a clear setup for interaction with the service. As we mentioned, the experiment is planned to be run in pairs. As a result, the team picking up this project will simply have to configure a general Postman account with a single collection but multiple APIs. The developer half of the lab rats will interact with this Postman account where they will change APIs and our Sync Ends service will take care of the rest. For the tester half of lab rats, they will need to be added to a Slack channel along with configuring a Slack Bot which interacts with our Sync Ends service. We leave it upto the team picking up this project to define whether they will add all pairs of participants in a common Slack channel or make multiple Slack channels for different experiments. The same goes for the Postman Collection part. <br>

To get an even better read on the effectiveness of the system, the roles of the developer and tester(API consumer) can be swapped and the experiment begin again so that both the lab rats can experience the halves and you can get a larger sample size to prove the validity of the observations.

Rest Assured, the [Experimentation Setup](INSERT LINK HERE) section defines clear and precise steps to get done with the setup part. In our view and based on our own preliminary trial, it will be easier for the team to just make a `single Postman collection` from the sample collection schema provided and add lab rats to and remove them from a common Slack channel. However, the final say is left upto the team conducting this experiment.

### Experimentation SetUp
As mentioned above, the team needs to setup 3 things for the experiment: (1) a Postman collection (2) a Slack channel (3) a [config json](INSERT LINK HERE).

The team will have to provide the `config json file` and a `Postman account` to each developer so that they can change the API schemas in the collection and the sync ends service which is run would parse the changes based on the `parameters in the config file`. The developer will only need to have Python installed as our package is hosted on PyPI and will be able to access [Web Postman](https://web.postman.co/workspaces). In the presence of our system, the developer won't have to be added to any Slack channels as that is handled by our service. However, in the absence of our system, the developer will need to have some way to communicate with API consumer, probably Slack and hence would need to be added the Slack channel where the API consumer is also added.

The API consumer(tester) will only need to be added to the `Slack channel` and the tester's job is to simply identify changes in APIs through Slack messages or otherwise.

#### Step 1 : Setup Postman
1. Sign in to [Postman](https://identity.getpostman.com/login).
2. If you do not have any pre-exiting collections on Postman, import this sample [collection](https://www.getpostman.com/collections/dfa93d217bf211237c8f).
3. To integrate with the Sync Ends service, a Postman API key is required. Generate API key by visiting this [page](https://web.postman.co/settings/me/api-keys).
4. Copy the generated API key. This is required during the time of execution of the service. Make sure you store it safely as you won't be able to view this any other time.

#### Step 2 : Create a Slack workspace and integrate Slack bot

##### 2a.Creating Slack team
1. Open https://slack.com/.
2. Provide your email ID. Select `Create New workspace`.
3. Check your email and enter the code to verify your email.
4. Provide your name and set a password.
5. Add some details to your workspace in the next page.
6. Provide a company name.
7. Workspace URL should be unique. Also remember this URL, this is what is used to login to your Slack instance.
8. Agree with the terms.
9. Skip the invite step.
10. You are up and running with your own instance of Slack.

##### 2b. Creating Slack bot
1. Open your `<workspace-URL>/apps` (the one you created above). For example, [https://test-visual.slack.com/apps](https://test-visual.slack.com/apps).
2. Search for bot in the search bar and select `Bots`.
3. In the Bots landing page, click on `Add configuration`.
4. Provide a Bot name. For example, `wolfpack-bot` and click on `Add Bot integration`.
5. In the `Setup instruction` page: `Copy and store the API Token`. For example, the token may look something like this: `xoxb-22672546-n1X9APk3D0tfksr81NJj6VAM`.
6. Save the Bot integration.

### Experimentation Process

### Experimentation Measures

## Congratulations
### **You just saved yourself from unwanted crashes**
<img src="https://media.tenor.com/images/73cca45a93f91944b2c9fdd4b05c3c53/tenor.gif"/>

## License

This project is licensed under the MIT License.
