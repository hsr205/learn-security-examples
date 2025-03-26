# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?id[$ne]=
    ```

4. Do you see the server crashing?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts** that can lead to a DoS attack.

- The vulnerabilities found in the **insecure.ts** module that can lead to a DoS attack are found in the logics inability to set a limit on the number of requests that can be executed in a given timeframe from a given user.

2. Briefly explain how a malicious attacker can exploit them.

- In the event of a DoS attack a malicious actor could employ the use of a bot created to programmatically send an overwhelming amount of requests to the application crashing the server as a result.
In this occurrence the malicious attacker now has control whether the site is active or in a crashed state.

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the DoS vulnerability?

- The defensive technique leveraged in the **secure.ts** module is the use of a rate limiter.
The rate limiter sets a ceiling on the number of requests that can be sent in a given time frame and the number of requests sent from a given IP address.
This efficiently protects the application from trying to ingest an overwhelming amount of requests in a short duration.