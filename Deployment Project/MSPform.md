
# MSP Form -Project Outline

  *This project is an outline of work I completed on the job, thought the repo is not available to view, I have included a complete outline of the projet below.*


### The Form
 
As pictured above, the user selects their “Reason to Contact” as “MSP Credential Company Enrollment” then give important information such as their name, email, company, etc. The blank labeled “Service Provided to HP” is what determines where the email copy of this form will be sent.


### FRONT END

A. Key Libraries 

-	React 
-	Veneer for styling

B. Visual Components

-	The input fields: This is where a user will enter needed information. The components were easily to implement using code snippets from veneer libraries as shown below

       `<TextBox

                defaultValue=”Value”

                label=”label”

                placeholder=”placeholder” 

                />`

-	The checkboxes: The checkboxes represent different supplier tools a supplier may be requesting access for. These are also easily implemented from veneer libraries as shown below
  

                `<Checkbox

                 defaultChecked

                id="checkbox"

                label="Label"
                />`


-	The dropdown menu: The dropdown menu is for suppliers to choose what service they are providing to HP to determine what team handles their request. Also styled by veneer

    `() => {
               
                const items = [
                { value: 1, label: 'Item 1' }

                ];

        const [value, setValue] = React.useState([]);

        const [options, setOptions] = React.useState(items);

        const onChange = (selectedOption) => setValue
        ([selectedOption.value]);

        const onClear = () => setValue([]);
}
    return(

        <Select

            options={options}

            id="select-usage"

            label="Select"

            onChange={onChange}

            value={value}

            />`

### BACK END

A. Dependencies 

-	Express – Express is a Node.js web application framework 
-	Body-parser - Body Parser is a middleware of Node JS used to handle HTTP POST request. 
-	NodeMailer- package for sending emails 
-	Dotenv - allow developers to create a . env file that has custom environment files that are added into the process 
-	Axios – make http request 
-	Validator – add validation over data through http request. 

B. Node Server details 
This is running as the middleware. Handles traffic from an Apache file

C. Apache Configuration 
Routes all traffic to the node server over HTTP internally on the server file

D. Verify Token 
We have implemented Google ReCAPTCHA in “Contact us” forms for avoiding spamming using reCAPTCHA npm package. 
We also need to get register on google reCAPTCHA website and give information about domains. Then google reCAPTCHA site produces site key and private key. Public key we need to pass to React component. private key we need to put on server to make further api call. 


`<ReCAPTCHA 

          sitekey={siteKey} // produced by google ReCAPTCHA 

          onVerify={handleChangeCaptcha}//calling function 

          ref={captchaRef} // giving reference to reset after 
some actions 

        /> `


Above, the site key is stored in variable and passed to site Key property. 

ReCAPTCHA is a free service from Google that helps protect websites from spam and abuse. A “CAPTCHA” is a Turing test to tell human and bots apart. It is easy for humans to solve, but hard for “bots” and other malicious software to figure out. 


D. Email 
/send_mail – this route accepts users form info and process it though validator service and then sends email to team to help with user request.
In the application, the form calls the sendMail service (a JavaScript function). When the form calls this method, it passes the payload(form info) to that service.  
 
`const reqObj = {} // data form collects 

    sendMail({ data: reqObj }) 

        .then(result => {})// if call get successful 

    .catch(err => {}) // if call get fail `
 


E. Validator 
/validator - this route accepts user info and verifies data is not empty or contain other errors 
Validation in frontend is needed for user data input restrictions and checking accuracy / quality of data. Javascript is used to implement validation in react application. Validation also occurs on the backend.
In the application, form validation is implemented though JavaScript.  
 
 
  `const [errors, setErrors] = useState({}); `
 
Above code is to declare state which will store errors in one JS Object. 
    

`  const err = {}; 
 
    if (name.trim() === '') err.name = 'Please enter name'; 

    if (email.trim() === '') err.email = 'Please enter email'; 

    if (!/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,})+$/.test
(email.trim())) err.email = 'Please enter valid email id'; 

   setErrors(err); `
 

F. Routing 
GET and POST express routes to create site functions such as validation and send mail. 
GET: / - base URL I.e. https://supplierportal.hpcloud.hp.com  
This route serves react build. Specifically, build/index.html 
POST : /send_mail – this route accepts payload and process it though validator service and then sends email to specific user. 
POST: /verify_token – this route accepts site key and captures secret key from .env file and make post call to google reCAPTCHA service. if successful, send 200 back to client. 


G. Folder Structure

Server.js 

/services

-MSPcredentialFormService.js

-mailService4.js

-recaptchaservice.js 

/validator

-MSPcredentialFormValidation.js 

Package.json 

Package-lock.json 



### DEPLOYMENT

A.	Deployment Services
- 	HP Supplier Portal is hosted on AWS.
- 	WinSCP: An open-source file transfer service for windows. Used to transfer build folder or other backend code files to the server for deployment.
- 	Putty: Putty is an open-source terminal emulator, serial console and network file transfer app. Used to make changes to HP Supplier Portal such as server updates file changes, and restarting node or apache.
- 	Visual Studio Code: The code is written and built in VSCode
- 	Github: The code is hosted as a GitHub repo through HP

B.	Deployment Process

1.	When the application code is change and ready to be deployed or updated to the production environment, a “build” will need to be created. To create the build folder, the following command is run, npm run build, then a folder is created for deployment.
 
2.	This folder must then be moved to the server. This is where WinSCP comes in as the file transfer service. After logging into the correct AWS server in WinSCP, the build folder the local machine is then moved to the server files directory.
 
3.	Next, both node and apache will need to be turned off temporarily. Apache is restarted within Putty on the command line while Node can be turned off directly from logging into AWS Cloud dashboard and stopping the instance
4.	To make this build live and usable to all users (deployed), Putty is used to update the server with our file changes. Putty is used to login into the appropriate server and the build folder is unzipped and replaces the previous build folder, checking for any vulnerabilities or errors in the deployment process.
Command line instructions
Zip -r build_0101.zip build (to save the previous build folder as a new name)
Mv build_0101.zip old (to move the renamed build folder into a folder called old for safe keeping) 
Unzip build.zip (unzip the new build folder and replace the old)
Rm -f build.zip (delete the zip file once deployed)

5.	Lastly both node and apache are restarted. Apache is restarted on the command line and Node is restarted via AWS Cloud dashboard by starting the instance again.
 

