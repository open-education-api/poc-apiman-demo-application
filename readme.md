# SURFnet - Open Onderwijs API - Demo application
========================

An application demonstrating the open onderwijs API Proof of Concept setup. The OOAPI PoC setup consist of:  

* JBoss Keycloak for OAuth authentication and delegating authentication to a SAML based IdP like Surfconext
* JBoss Apiman for publishing services in a managed and secured way.

The demo application enables the user to:  

* Login using JBoss Keycloak directly or indirectly via an Identity Provider like Surfconext
* Acquire an OAuth bearer token (from JBoss Keycloak)
* Invoke API calls on JBoss Apiman using the OAuth bearer token

The demo application is a Javascript application that uses the [JBoss Keycloak Javascript Adapter](http://keycloak.github.io/docs/userguide/keycloak-server/html/ch08.html#javascript-adapter) for securing the application and supporting login and acquiring the token. 

The demo application is by default configured to operate as a public OAuth client that is assumed to be deployed on the same application server as JBoss Apiman and JBoss Keycloak. In case of a different setup src/main/webapp/keycloak.json should be adjusted to reflect this. By default it assumes:  

* The **apiman** is realm is available and is configured with the secret that comes prepackaged with the JBoss Apiman distribution
* A client **js-console** is available within the **apiman** realm. The client is setup as:
	* A public client
	* With `/js-console/*` as a valid redirection URL


# Build
Build the project using `maven install`. This generates a WAR file in target/js-console.war

# Installation

* Deploy the WAR, target/js-console.war, on the same application server as JBoss Apiman and JBoss Keycloak. The WAR has been tested on JBoss Wildfly.


# Run

The test client is available on the URL: <protocol>://<host>:<port>/js-console/ where <protocol>, <host> and <port> should be adjusted to meet your environment.

# Usage

* Choose *Inloggen* from the navigation bar to be redirected to the login screen of JBoss Keycloak. After completing the login you will be redirected back to the test client. A valid login session is required to use any of the other features.
* Choose one of the options in the *Keycloak* menu from the navigation bar to:
	* view the content of OAuth token;
	* renew the OAuth token;
	* view the URL's of the Keycloak environment;
* Choose an API call from the dropdown menu to invoke an API call on JBoss Apiman using the OAuth token of the logged in user.