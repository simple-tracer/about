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