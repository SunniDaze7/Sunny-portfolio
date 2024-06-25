## Hackathon Project - Backlog Checker

### High-level overview of the project's purpose
The Backlog checker app creates an efficient way to get the backlog message count for one of my team's suply chain application at the press of a button. 

### Situation
   This project is directly tied to my role at HP to solve and issue of counting backlog messages sent to one of our applications. Before, the backlog count would be counted directly from the database using a SQL query. With this app, you can directly see the number by simply pressing a button.The SQl query is automatically deployed in the background, then the backlog number is displayed on the front end for the user to see. This provides a more efficient way to get the data saving time so the backlog can be handled quickly.
   
### Task
 When deployed, the app displays a basic homepage and a banner displaying the app name. Underneath a button is displayed to commence the backlog check. Once the button is pressed, a loading animation is displayed with a message telling the user the approximate wait time. Once the backlog is counted, the loading screen disappears and the number of backlog messages is displayed as well as a back button to go to the original button. I designed the app to be simplistic as possible to emphasize efficiency 
 
### Action
To create the app, I used a basic react app template(create-react-app). I utilized basic divs and navs to build simple components for each of the individual main 3 pages. The main page's main focus is UI; displaying a nav bar and button component using react. Upon the button press, a useState is changed from false to true which then begins the loading page. I also utilized an npm package to display a loading animation. To keep the lading animation displayed until the results are ready useEffect has a setTimeout to when the database returns data. Once the data is returned, the last page is displayed. On this page, again UI is the focus. The UI is similar to the main page with the number being displayed in a brief message. Then if the user wishes to return to the main page, the back button can be pressed which changes a useState variable from false to true, returning them to the main page.

### Result


## Technologies
- React
- HTML
- CSS
- Javascript
- NodeJS
- Oracle

## Competencies
### JF 2.5 - Can implement a responsive User Interface
- I have demonstrated this competency on the job directly through the application I am responsible for. I am assigned in creating new functionalies for users to interact with on a public facing site.
- Through this project, I was able to display this competency by creating a site that can be interacted with simply and effectively. All interactive aspects of the projects work as intended. To accomplish this goal, I linked an Oracle database to the application with a DB file. This allowed for when a user selects to see backlog count, the code responds with the requested information.
- This project helped me understand the importance of simplistic UI design for some projects. A detailed design is not always required depending on the use case. I was also able to display how I can use this competency to provide impact to my team creating efficiency.

### JF 4.6 - Can test code and analyze results to correct errors found using unit testing
- I have demonstrated this competency on the job through the application I am responsible for. There are several tests set up within an Apptest.js file that run before code is deployed. I have edited that code to have new tests when I edit the site for new functionality.
- Through this project I demonstrated this competency by creating a test file(App.test.js). In this file, several tests were created to check that key UI is being displayed correctly (such as the buttons and text)
- This competency helped me to understand the importance of creating effective tests and how they can help create controls in code allowing you to catch erros quickly.

## Challenges
- During this project, I faaced challenges integrating an outside database from Oracle into my code. I was not familiar with the technology and wasn't sure where to begin. To overcome this challenge I turned to both Oracle and NodeJS documentation. In reading this docmentation, I found that a DB file could be created and I can plug in my log in info for Oracle into this file as well as the SQL query needed to accessd the backlog count from the data. I learned that there is usually documentation for problems I run into and when reading carefullyand some problem solving, I can solve the issue.
