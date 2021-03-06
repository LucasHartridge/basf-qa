## UI

The UI Folder contains all the tests to cover the BASF Coding Challenge Test Engineer Front End Task. This framework is based on Cypress. I never used before cypress but I thought that it should be a good challenge for me to implement this solution using a framework that I did not use before to show my essence as an Engineer, I am always open to learning new tools.

### Prerequesites

1. Login https://qknows-qa.basf.com"
2. Enter your username and password
3. Enter the Google Authenticator Code
4. Right Click on your browser -> Go to Applications Tab -> Cookies -> Get the XSRF-TOKEN and AUTHSESSIONID
5. Go to cypress -> fixtures -> profile.json
6. Replace the value for XSRF-TOKEN
7. Replace the value for AUTHSESSIONID

To find this values you will need to
Note this is in case that the current credentials did not work. The reason why I had to to this is explained in `Problems that I found` section

### Steps to Run the Test:

1. Type `npm install` or `npm i` in Terminal - This will install all the dependencies
2. Execute the command on Step 1
3. Type `npm run open-cypress in Terminal`
4. Execute the command on Step 2
5. Note that a new window with Cypress Runner will be opened
6. Here you will see 2 spec files. One contains the test for login and another one for the search functionality
7. Clicking on each file will launch the test individually
8. To run all the test click on Run 2 integration specs

### Problems that I found

- It is not possible to automate the login process because the Google Authenticator Factor is required. This code is only given by the Authenticator App on the Phone. That is why I had to implement the Cookies solution, setting up the cookies manually before going to the site
- I found an issue with the Terms and Condition Sign. After checking, the ‘Agree with terms and condition’ and click the ‘Proceed to QKnows’ button a 400 Error is displayed in Network Console. Because of this each time that you refresh the page, the ‘QKnows Terms of Use’ is displayed
