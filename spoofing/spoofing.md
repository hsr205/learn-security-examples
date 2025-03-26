# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.

- The vulnerability displayed in the **insecure.ts** module is found where the developer inappropriately hard coded a user-secret to a given user session. 
As a result, the user-secret is static and can be easily intercepted by a malicious actor. 
In addition, the developer never sets the `sameSite` field to `true` which would prevent a user's cookie from being leveraged across different sites. 

2. Briefly explain different ways in which vulnerability can be exploited.

- As illustrated in the `mal-steal-cookie.html` file, the current implementation found in the **insecure.ts** module always for a malicious actor to both intercept and print the user's secret to the console. 
The secret can then be leveraged to say execute a `POST` request imitating the actual user found in the `mal-csrf.html` file.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.

   - The **secure.ts** module enhances the **insecure.ts** module in the following ways:

   - (1) Does not hard code the user's session secret
     - This allows for the password to be passed in dynamically via the user allowing the password to be different across sessions as opposed to hard coded for each user.
   - (2) Sets the cookie key-word values of `httpOnly` and `sameSite` to `true`
     - Setting `httpOnly` to true enables the session cookie only sends any cookie related information via HTTP/HTTPS. This eliminated the possibility for cookie data to be accessible via the document object model (DOM).
     - Setting `sameSite` to true enables all cookie data to be restricted to just a single site. Meaning the `mal-csrf.html` file could no longer use a user's session cookie on a different site.
