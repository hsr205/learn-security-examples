# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, send a GET request

    ```
        http://localhost:3000/send-form
    ```

4. Try different UserIds and see which one gives you authorized access to change the role of that user.

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

- The vulnerabilities found in the **insecure.ts** module can be found in the lack of authentication required to change the privileges of a given user through the `/update-role` endpoint.

2. Briefly explain how a malicious attacker can exploit them.

- Due to the lack of authentication behind who is changing the privileges of a given user, any user could in theory elevate or deescalate their own or another user's privileges at will.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the privilege escalation vulnerability?

- The defensive techniques found in **secure.ts** module include the use of session middleware requiring the user to authenticate themselves within a given session.
Given the user has the appropriate authentication credentials then the user is checked whether they are in fact logged into the application.
Once these first and second levels of authentication are passed only then can the request to change a given user's privileges is sent to the backend database.  