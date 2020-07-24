# About Simple Tracer

On the 31st of December 2019, the world as we knew it began to crumble. As we celebrated the beginning of a new decade, a deadly new virus was spreading in Wuhan, China. And it spread fast, one infected person could spread COVID-19 to thousands of people. As we built this project, we were still fighting the pandemic and the battle is very far from over. We've seen first hand, the effect a pandemic can leave. 

One thing we've observed is the effectiveness of contact tracing as a utility to fight the pandemic. So we built a tool that allows for contact tracers to identify people who enter the same building. The idea behind it is that any administration could deploy it in under an hour. This means that if one person who entered a shop gets infected, the people who were at the shop get a message that serves a quarantine order and it is logged that they have entered quarantine. 

Simple Tracer consists of five key components:

1. Flamingo, the app for residents to check in to buildings. Built with Ionic.

2. Eagle, an API that manages checking in and out to allow for new solutions to be built. Built with Express and Node.js.

3. Hummingbird, a website that powers building registration and QR code generation. Built with HTML, CSS & JS.

4. Hornbill, a web app for contact tracers to identify contacts and issue quarantine orders.

5. Parrot, a python script for creating admin users for Hornbill.


Collectively, all of these can deployed with just a few clicks by following the guide below.

### 🚩Stage 1: Airtable

We use Airtable for a database. You can learn more about Airtable [here](https://airtable.com). The free plan for Airtable is sufficient to demo this app, however to deploy this solution in production you will almost certainly need the Airtable Enterprise plan. You can learn more about it [here](https://airtable.com/enterprise).

The reason for using Airtable is that it can be built on top of extremely quickly and every day counts in a pandemic. This will allow you to build custom solutions.

1. To begin, we need to create a workspace. Here is a [guide on how to do that](https://support.airtable.com/hc/en-us/articles/360004513573-Creating-a-new-workspace).

2. Next you need to make a copy of the base template we have created. You can find it [here](https://airtable.com/universe/expOoFmg86RVNcbcl/simple-tracer-base-template). Click `Copy Base` in the top right corner.

3. So that your deployments will be able to interact with your Airtable base we will need to get an API key and the Base key. To do this you must:

    1. Go to [this page](https://airtable.com/account). 
    
    2. Find the API section and click generate
    
    3. Copy the provided key this is your API key.
    
    4. To get the Base key go to [this page](https://airtable.com/api) and click the base we created earlier.
    
    5. Use control f or command f to find 'The ID of this base is' on the page.
    
    6. The ID following that will be your Base Key
    
    7. Make sure to note down both keys.
    

### 🚩Stage 2: Eagle

The next step is to deploy Eagle, the API. Here are the steps to do so these steps are for Heroku:

1. Click this [link](https://heroku.com/deploy?template=https://github.com/simple-tracer/eagle/).
2. Fill in your app name and a server location.
3. For the `AIRTABLE_BASE` enviromental variable, enter your Airtable Base Key.
4. For the `AIRTABLE_KEY` enviromental variable, enter your Airtable API Key.
5. For the `SECRET_KEY` enviromental variable, enter a random string of letters. You can use this [site](https://www.random.org/strings/). Don't forget this.
6. Click `Deploy App`.
7. Once the app is deployed, click `View App`. Copy the URL and take note of it.

### 🚩Stage 3: Hornbill

Now we want to deploy Hornbill, our admin tools system. This setup also uses Heroku and is similar to Eagle's.

