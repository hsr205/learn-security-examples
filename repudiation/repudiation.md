# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.

- The vulnerability found in the **insecure.ts** module is both insufficient logging and logging that cannot identify the activities of a non-malicious user or malicious user.

2. Briefly explain why the vulnerability is addressed in **secure.ts**.

- In the **secure.ts** module extensive server logs are being written enabling developers to identify the request method, URL and IP address of any user that engages in a behaviour on the site.
With the addition of these logs the ability for the developer of a site to bring action against a malicious actor is greatly increased by having the additional information in hand.

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?

-  The design pattern used primarily within the **secure.ts** module is the middleware pattern. 
The middleware pattern in the **secure.ts** module is leveraged for logging and error handling purposes.
The logging middleware is the core difference between the **secure.ts** and **insecure.ts** modules allowing for a more expansive understanding of exactly what / who is executing a given behaviour on the site.
The error handling middleware provides crash logs in the instance a given exception is thrown during execution of the application.