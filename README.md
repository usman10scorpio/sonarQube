# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

After you run the `npm run build` and build folder is made successully, you can check if its working correct locally by installing `serve` locally (https://create-react-app.dev/docs/deployment/ ) and run below command to check

`npx serve -s build` 

## Screenshots

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/one.png "User Inteface mains screen")

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/two.png "Search results - web")

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/three.png "Search results - mobile")

## SonarQube

SonarQube is an open-source platform that is used to measure and analyze the quality of source code. It provides continuous inspection of code quality and security vulnerabilities in a variety of programming languages, including Java, C#, Python, and JavaScript, among others.
The platform offers a variety of tools and features to help developers identify and fix issues in their code, including static code analysis, code coverage metrics, code duplication detection, and security vulnerability detection. SonarQube can be integrated with various development tools and workflows, including Continuous Integration and Continuous Delivery (CI/CD) pipelines.

By using SonarQube, developers can improve the overall quality of their code, reduce technical debt, and minimize the risk of security vulnerabilities. Additionally, SonarQube can help teams enforce coding standards and best practices, leading to more consistent and maintainable code over time.

## Architecture of SonarQube

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/four.png "architecture of sonarqube")

## How to use SonarQube locally via docker?

```
version: '3'
services:
  sonarqube:
    image: sonarqube:latest
    ports:
      - "9000:9000"
    networks:
      - sonarnet
    environment:
      - SONARQUBE_JDBC_URL=jdbc:postgresql://db:5432/sonar
      - SONARQUBE_JDBC_USERNAME=sonar
      - SONARQUBE_JDBC_PASSWORD=sonar
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_logs:/opt/sonarqube/logs
      - sonarqube_extensions:/opt/sonarqube/extensions
    depends_on:
      - db

  db:
    image: postgres:latest
    environment:
      - POSTGRES_USER=sonar
      - POSTGRES_PASSWORD=sonar
      - POSTGRES_DB=sonar
    volumes:
      - postgresql:/var/lib/postgresql
    networks:
      - sonarnet

volumes:
  sonarqube_data:
  sonarqube_logs:
  sonarqube_extensions:
  postgresql: 

networks:
  sonarnet:

```

1.	Make a docker-compose.yaml file in your root directory of your project and paste the above code. For me I have added it in microservices folder where all microservices are listed.

2.	Go to sonarqube scanner page and download the package. For me it was Mac OS X 64-bit. Unzip this folder and place it somewhere. Copy its path and add it in your path. 

  For mac, run the below command

  sudo nano /etc/paths

  and add your path to sonar-scanner/bin

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/five.png "paths")

3.	Now go in the root directory of your project folder or all microservices folder and run docker-compose up. You can check your container up and running in docker.

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/six.png "docker")

4.	Based on your port setting in docker-compose.yml you will now be able to view sonarqube web UI on localhost:9000. Use “admin” as username and password. It will you ask you to update your password. For me after changing the password, I update the password back to “admin”.

5.	Now you will see a screen like below.

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_one")

   click on manually and add details

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_two")

   click on setup and after that go to your project and generate a token.

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_three")

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_four")

  Do the changes according to your project for us its JavaScript and your OS (macOS) for me.

  Copy the execute scanner command. We need to modify it.

  Click on project settings, we need to exclude java files.

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_five")

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_six")

  Delete the .java field and save it. Reason of doing it is because in our microservices there are some files in java and which we don’t want to analyze.

6.	Now it’s time to run the sonar scanner command and see the magic. Remember what password we have set? “ad**n”

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_seven")

  I have added (login, password, and language type of our project) as modification. Run this command in your bash shell or zsh in your project root.

7.	After the command run successfully, you will see success in logs. Check out the below image.

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_eight")

  and now if you refresh your SonarQube web page you will see below image.

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_nine")

  click on your project name and checkout different tabs (Overview, Issues, Security Hotspots, Measures, Code, Activity)

![Alt text](https://github.com/usman10scorpio/usman-iqbal-githubsearch-web/blob/main/public/screenshots/seven.png "sonarqube_screen_ten")

  Note: This is the most basic setup to learn our code quality and security hotspots. You can always check it out more in SonarQube documentation.


