# Tampering

This example demonstrates information disclosure by injecting malicious query objects to a NoSQL database.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Insert test data in the MongoDB database. Make sure the mongod is up and running by typing the `mongosh` command in the termainal. If mongod process is up then you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with mongosh and running the command `show dbs;`.

2. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

3. In the browser, pretend to be a hacker and type a malicious request

    ```
        http://localhost:3000/userinfo?username[$ne]=
    ```

4. Do you see user information being displayed despite the malicious request not having a valid username in the request?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**

- The vulnerability displayed in the **insecure.ts** module is the user asked for their user-name the user-name is never sanitized. 
This results in whatever the user may input as a user-name being directly sent to the database in the form of a NoSQL query. 

2. Briefly explain how a malicious attacker can exploit them.

- As the input from the user goes directly to the backend NoSQL database the user (if a malicious actor) can run a NoSQL injection attack on the application.
This involves a malicious actor inserting specific NoSQL commands as input to the application allowing the malicious actor the potential ability to gain access to personally identifiable information (PII) and or other sensitive information. 

3. Briefly explain the defensive techniques used in **secure.ts** to prevent the information disclosure vulnerability?

- The logic provided in the **secure.ts** module does some sanitizing of the user inputted user-name. 
The user-name inputted is checked for its data type prior to query the database.
This user-name sanitation removes all non-alphanumeric characters in the inputted user-name which is one of many methods to guard against a NoSQL injection attack.  