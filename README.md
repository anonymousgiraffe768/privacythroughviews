# Privacy Through Views

The Policy Generator is a Python Script that starts a GUI and is used to help generate the XML files the backend needs to enforce the views. To run it needs to be connected to a database so that it can check the validity of views.

To install the tool:
Download and unzip CustomInterceptor.zip and install the 3 jar files in the external libraries folder of the web application, e.g. WebContent/WEB-INF/lib/. Then modify the web application to use the new custom.jar instead of the default one by passing it as an argument when setting up the Java Database Connector, as follows:
```
final String driver=”com.mysql.jdbc.Driver”;
final String mySQL_inter=”jdbc:mysql://localhost:3306/database name”;
// jdbc parameter to specify a custom interceptor
final String custom=”?statementInterceptors=custom.Interceptor”;
java.sql.DriverManager.registerDriver((java.sql.Driver)(Class.forName(driver).newInstance()));
java.sql.Connection conn = java.sql.DriverManager.getConnection(mySQL_inter+custom, ”username” ,”password”) ;
```
The final step is to link to the policy XML file when setting up a session by adding the following snippet:

```
<%@ page import=”custom.SessionInfo”%>
<% Long thread_ID = new Long(Thread.currentThread().getId());
/∗ session is an http session variable ∗/
SessionInfo.setSessionValues(thread_ID, session);
SessionInfo.setPolicyFilepath(”/.../policy.xml”); %>
```
to the main/default jsp file for the application.
