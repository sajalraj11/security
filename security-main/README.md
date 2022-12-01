# security
Pages and components for creating an AA login system.

A six minute video explaining this repo can be found here: https://www.viddler.com/v/9116e917

### Components in this Repo

login.a5wcmp - This UX allows users to log in. Upon sucessful login, users are taken to a page called portal.a5w. The component is embedded into the login.a5w page.

requestReset.a5wcmp - This UX is where users enter their email to request a password reset. The component contains a function called resetRequest, which relies on you to supply a connection string to a table called PWreset. Look for the part in the code that reads [[YOUR CONNNECTION STRING NAME]] The structure needed for the PWreset table is shown below. 
![image](https://user-images.githubusercontent.com/12627665/119546088-8376a400-bd61-11eb-9068-b44451a35ad1.png)

You will also need to replace the Sparkpost key so that the system can send emails with the password reset links. (See sparkpost.com for details. Alternatively, you could edit the code to send using a different email provider). Look for for the part of the code that reads [[INSERT YOUR KEY HERE]]. This component is embedded in the resetPart2.a5w page. You will also want to change the wording of the password reset email especially the part of the email that specifies the URL of the password reset link. 

userChangePassword.a5wcmp - This UX lets the user enter their new password. It is a derivative of the built-in UX template
also called userChangePassword. In this version of the component, the user is assumed to be logged in, and their username and 
current (a.k.a. "old") password are stored in session variables. These session variables automatically fill the username and 
password fields, which are hidden from the user. After the user resets their password, they are brought to a page called portal.a5w. This component embedded in a page called resetPart2.a5w.

### Pages in this Repo

login.a5w - This is the login page and is used to hold the login.a5wcmp UX component.

forbidden.a5w - This is a page the user sees if they try to get to a page they are not allowed to access. (The other pages in this project, do not rely on this page. It is just here for completeness when setting up the project's security properties)

requestReset.a5w - This is the page that holds he requestReset.a5wcmp UX component.

resetPart1.a5w - This is the page the user gets to when they click a password reset link in their email. The page expects the URL to contain a query string with a GUID. The page then checks to see if the GUID is present, valid, and has not expired. The 
page is hardcoded to only allow GUIDs issued within the last 20 minutes. This page also relies on you to supply a connection string to a table called PWreset. Look for the part of the code that reads [[YOUR CONNNECTION STRING NAME]].  There are two instances of [[YOUR CONNNECTION STRING NAME]] in the code, so make sure you replace both of them. (See requestReset.a5wcmp above for notes about the structure of the PWreset table.) If the GUID is accepted, the user is immediately redirected to the resetPart2.a5w page. 

resetPart2.a5w - This is the page where the user enters their new password. It holds the userChangePassword.a5w embedded component.

portal.a5w - This is the page the user gets to when they have successfully logged in. It's meant to be replaced with your own content.


For questions about this content, please contact guides@alphasoftware.com
