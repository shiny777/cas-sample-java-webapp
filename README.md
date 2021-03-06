# Example CASified Java Web Application

This is sample java web application that exercises the CAS protocol features via the Java CAS Client.

Configure
---------

- Adjust the url endpoints of the CAS server and the application server in the [`web.xml`](https://github.com/UniconLabs/cas-sample-java-webapp/blob/master/src/main/webapp/WEB-INF/web.xml) file.
- If you wish to exercise proxy authentication, switch your CAS client filters to be `AuthenticationFilter` and `Cas20ProxyReceivingTicketValidationFilter` in the same file.

##Build

###Ant Build

- Adjust the [`build.xml`](https://github.com/Unicon/iam-labs/blob/master/cas-sample-java-webapp/build.xml) file to note the location of the application server and the way environment variables are configured. (i.e. `catalina.home`, `M2_HOME`, etc)
- From the root of the project directory run `ant deploy`. 
- The resulting WAR file will be available inside the container's `webapps` directory as `cas-sample-java-webapp.war`

###Maven Build

- If you prefer a Maven build, From the root of the project directory run `mvn clean package`. 
- The resulting WAR file will be available inside the prohject's `target` directory as `cas-sample-java-webapp.war`. Copy the file over to your container's environment. 

##Run
Pull up the URL `https://[server-address]/cas-sample-java-webapp` in your browser. 
You'll immediately be redirected to the CAS server login page, and back to the application with authentication 
details and attributes displayed in the [`index.jsp`](https://github.com/Unicon/iam-labs/blob/master/cas-sample-java-webapp/src/main/webapp/index.jsp) file.

##Testing High Availability
Assuming you have deployed CAS on two nodes, you can use the sample application to make sure all nodes are properly
sharing the ticket state. To do this, in the `web.xml` file ensure that:

- The `casServerLoginUrl` of the `CAS Authentication Filter` points to CAS node 1 (i.e `https://cas1.sso.edu:8443/cas/login`).
- The `casServerUrlPrefix` of the `CAS Validation Filter` points to CAS node 2 (i.e `https://cas2.sso.edu:8443/cas`)
- For both of the above filters, the `serverName` should always point to the location where *this sample application* is deployed.


Deploy the application and test. You may also want to reverse the order of CAS nodes 1 and 2 in the above cnfiguration, redeploy and test again.




