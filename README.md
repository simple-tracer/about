# About Simple Tracer

On the 31st of December 2019, the world as we knew it began to crumble. As we celebrated the beginning of a new decade, a deadly new virus was spreading in Wuhan, China. And it spread fast, one infected person could spread COVID-19 to thousands of people. As we built this project, we were still fighting the pandemic and the battle is very far from over. We've seen first hand, the effect a pandemic can leave.

One thing we've observed is the effectiveness of contact tracing as a utility to fight the pandemic. So we built a tool that allows for contact tracers to identify people who enter the same building. The idea behind it is that any administration could deploy it in under an hour. This means that if one person who entered a shop gets infected, the people who were at the shop get a message that serves a quarantine order and it is logged that they have entered quarantine.

Simple Tracer consists of five key components:

1. **Flamingo**, the app for residents to check in to buildings. Built with Flask as a PWA.

2. **Hummingbird**, a website that powers building registration and QR code generation. Built with Flask

3. **Hornbill**, a web app for contact tracers to identify contacts and issue quarantine orders. Built with Flask

4. **Parrot**, a python script for creating admin users for Hornbill.

Collectively, all of these can deployed with just a few clicks by following the guide below.

**Table of Contents**

1. [Deployment Instructions](#deployment-instructions)

    1. [Airtable](#-stage-1-airtable)
    
    2. [Twilio](#-stage-2-twilio)
    
    3. [Hornbill](#-stage-3-hornbill)
    
    4. [Parrot](#-stage-4-parrot)
    
    5. [Flamingo](#-stage-5-flamingo)
    
    6. [Hummingbird](#-stage-6-hummingbird)

2. [Usage Instructions](#usage-instructions)
    
    1. [Hornbill](#hornbill)
    
    2. [Parrot](#parrot)
    
    3. [Flamingo](#flamingo)
    
    4. [Hummingbird](#hummingbird)

3. [FAQ](#faq)

4. [Contributors](#contributors)

## Deployment Instructions

### 🚩 Stage 1: Airtable

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

### 🚩 Stage 2: Twilio

This can get a bit complicated, we'll let the people over at Twilio explain with this [great guide](https://www.twilio.com/docs/notify/quickstart/sms). It will run you through the process of creating a Notify service in Twilio. You only need to follow the guide up to the **Gather account information** section.

Once you are done you should have the following information:

| Config Value         | Description                                                                                                                                 |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Account SID          | Used to authenticate REST API requests - [find it in the Twilio console here](https://www.twilio.com/user/account/settings).                |
| Auth Token           | Used to authenticate REST API requests - [like the Account SID, find it in the console here](https://www.twilio.com/user/account/settings)  |
| Service Instance SID | A Notify Service instance where all the data for our application is stored and scoped. You created it in Twilio console in the above guide. |

### 🚩 Stage 3: Hornbill

Now we want to deploy Hornbill, our admin tools system. This setup also uses Heroku and is similar to Eagle's.

1. Click this [link](https://heroku.com/deploy?template=https://github.com/simple-tracer/hornbill/).

2. Fill in your app name and a server location.

3. For the `AIRTABLE_BASE` enviromental variable, enter your Airtable Base Key.

4. For the `AIRTABLE_KEY` enviromental variable, enter your Airtable API Key.

5. For the `KEY` enviromental variable, we need to generate a key (unlike before we can't just use a random string of letters).

   1. To do this we will use Python, open your terminal and type python. Or use this [site](https://www.python.org/shell/) if you don't have Python installed.
   2. Next, type `import os` and click enter.
   3. Now, type `import base64` and click enter.
   4. To end, type `print(base64.urlsafe_b64encode(os.urandom(32)))`
   5. Copy the result, if your result has `b'` at the start delete that as well as the `'` at the end.

6. For the `TWILIO_ACCOUNT_SID` enviromental variable, enter your Twilio Account SID you made earlier.

7. For the `TWILIO_AUTH_TOKEN` enviromental variable, enter your Twilio Auth Token you made earlier.

8. For the `TWILIO_NOTIFY_SERVICE_SID` enviromental variable, enter your Twilio Service Instance SID you made earlier.

9. Click `Deploy App`.

10. Once the app is deployed, click `View App`. Welcome to Hornbill, but what is my password?

### 🚩 Stage 4: Parrot

Parrot is a simple command line tool that allows you to add admin users so you can login to Hornbill.

1. Write the following in your terminal:

```
mkdir parrot

cd parrot

git clone https://github.com/simple-tracer/parrot.git

python3 parrot.py new
```

2. This will start the process of creating a new user. Fill in the requested details, make sure the `Secret key` is the same as made in Step 5 of the Hornbill stage.

3. Now you have created a new user, you can login in on Hornbill.

4. To update a user's password replace `new` with `update`. To delete a user replace `new` with `remove`.

### 🚩 Stage 5: Flamingo

Next up we are deploying Flamingo, the tool everyday citizens use to check in and out of places. This setup also uses Heroku.

1. Click this [link](https://heroku.com/deploy?template=https://github.com/simple-tracer/flamingo/).

2. Fill in your app name and a server location.

3. For the `AIRTABLE_BASE` enviromental variable, enter your Airtable Base Key.

4. For the `AIRTABLE_KEY` enviromental variable, enter your Airtable API Key.

5. Click `Deploy App`.

6. Once the app is deployed, click `View App`.

### 🚩 Stage 6: Hummingbird

Lastly we are deploying Hummingbird, which powers place registration and QR code generation.. This setup also uses Heroku.

1. Click this [link](https://heroku.com/deploy?template=https://github.com/simple-tracer/hummingbird/).

2. Fill in your app name and a server location.

3. For the `AIRTABLE_BASE` enviromental variable, enter your Airtable Base Key.

4. For the `AIRTABLE_KEY` enviromental variable, enter your Airtable API Key.

5. Click `Deploy App`.

6. Once the app is deployed, click `View App`.

**🎉 Amazing! We've succesfully set up Simple Tracer!**

## Usage Instructions

### Hornbill

#### Login

When first loading up the app, you will be asked to login.

<img src="images/hornbill_login_required.png" alt="Login required" width="50%">

Enter the details you generated with [Parrort](#-stage-4-parrot).

<img src="images/hornbill_login_screen.png" alt="Login screen" width="50%">

And you are in!

#### Issuing Quarantine Orders

Click this button to fetch contacts.

<img src="images/hornbill_fetch_button.png" alt="Fetch button with arrow" width="50%">

Enter the ID number, ensure this is the one used with Simple Tracer.

<img src="images/hornbill_enter_id_number.png" alt="Form to enter ID Number" width="50%">

And here are the contacts, click on the boxes to expand and see more details. When you are ready click "Issue Quarantine Orders"

<img src="images/hornbill_contacts.png" alt="Contacts list" width="50%">

Clicking "Issue Quarantine Orders" will send them a text saying:

> You have been in contact with a recent COVID-19 case. Please do not leave your residence, you are now required to enter 14 days of self isolation. If you are outside, return home immediately. Thank you.

And you've done it!

#### See People serving Quarantine Orders

You can see the people who are serving quarantine orders by clicking this button.

<img src="images/hornbill_view_button.png" alt="View button with arrow" width="50%">

### Parrot

View [above](#-stage-4-parrot)

### Flamingo

To install Flamingo, users should go to your link and they will receive a prompt to install it as a PWA.

The first screen is this, it is a camera window which can be used to position the camera to see a QR code.

<img src="images/flamingo_qr_scan.jpg" alt="QR Scanning Page" height="400px">

The user will then be asked for more details

<img src="images/flamingo_first_page.jpg" alt="Page asking for ID Number" height="400px">

The system will check if it has details for that account, if it doesn't it will ask for more. Otherwise this page will be skipped.

<img src="images/flamingo_second_page.jpg" alt="Page asking for more details" height="400px">

And success!! The person has been checked in.

<img src="images/flamingo_success_page.jpg" alt="Check in success page" height="400px">

To checkout, they just need to scan the QR code and enter their ID again.

<img src="images/flamingo_success2_page.jpg" alt="Check out success page" height="400px">

### Hummingbird

Coming soon.

## FAQ

<details>
    <summary>I have an issue, what can I do?</summary>
    <br>
    Please report it in the Issues tab of the related Github repository. If you aren't sure which repository to report the issue in, you can report it here. If         your issue is sensitive or related to secruity please email <a href="mailto:contact@simpletracer.tech">contact@simpletracer.tech</a>.
</details>

<details>
    <summary>I don't have the technical know how to set up the app, what can I do?</summary>
    <br>
    We offer free set up to all goverment agencies. Please email <a href="mailto:contact@simpletracer.tech">contact@simpletracer.tech</a>, with details and verifaction of your identity. 
</details>

<details>
    <summary>Can I use a custom domain?</summary>
    <br>
    Yes! Check out: https://devcenter.heroku.com/articles/custom-domains 
</details>

<details>
    <summary>Which services do I have to pay for?</summary>
    <br>
    If you plan to use this in a real world setting, you will need Airtable Enterprise, the Heroku Hobby plan and a load of Twilio Credit.
</details>

<details>
    <summary>I'd like to contribute, how can I?</summary>
    <br>    
    First off, thank you. All our code is open source and each Github repository has instructions for contributing. For this repo, it's best to run through the guide and then add additional details you feel are missing. Once you've contributed add yourself to the contributors list below, here's<a href ="https://github.com/simple-tracer/about/issues"> how</a>.
</details>

<details>
    <summary>What is your Code of Conduct?</summary>
    <br>    
    Please view this document.
</details>

## Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="http://sampoder.com"><img src="https://avatars3.githubusercontent.com/u/39828164?v=4" width="100px;" alt=""/><br /><sub><b>Sam Poder</b></sub></a><br /><a href="https://github.com/simple-tracer/about/commits?author=sampoder" title="Code">💻</a> <a href="https://github.com/simple-tracer/about/commits?author=sampoder" title="Documentation">📖</a> <a href="#tutorial-sampoder" title="Tutorials">✅</a> <a href="#tool-sampoder" title="Tools">🔧</a> <a href="https://github.com/simple-tracer/about/issues?q=author%3Asampoder" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/darkthunder007"><img src="https://avatars3.githubusercontent.com/u/53977169?v=4" width="100px;" alt=""/><br /><sub><b>darkthunder007</b></sub></a><br /><a href="https://github.com/simple-tracer/about/commits?author=darkthunder007" title="Code">💻</a> <a href="#ideas-darkthunder007" title="Ideas, Planning, & Feedback">🤔</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
