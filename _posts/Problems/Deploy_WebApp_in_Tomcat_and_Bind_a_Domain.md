#Deploy WebApp in Tomcat8.0 and Bind a Domain
##Get an available domain
1. get a domain:use freenom
2. DNS: use dnsla
3. put the host message of dnsla into your domain manage in freenom
4. try to ping it.
5. Port mapping: for me,I use hiwifi as my routers,![](http://i.imgur.com/coqmKUO.png)

##Prepare
I use eclipse to write my J2EE webapps, but eclipse does not support remote host. 

the default webapps is stored in <b>&lt;YOUR\_WORKSPACE&gt;/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps</b>

however, the default webapps path in Tomcat is <b> &lt;CATALINA\_BASE&gt;\webapps(or &lt; CATALINA\_HOME &gt;\webapps, for example:E:\\tomcat)</b> 

Thus,we need to copy the webapp from <b>&lt;YOURWORKSPACE&gt;/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps</b> into <b> &lt;CATALINA\_BASE&gt;/webapps</b>

We can do it automatically in Eclipse,

1. open configuration of server in eclipse
2. clear the deployed apps below the server(if exists)
3.  start the server
4.  change Server location into use Tomcat location,set server path = &lt;CATALINA\_BASE&gt;, set deploy path = webapps
5.  ctrl+s save it.

Before:
![](http://i.imgur.com/GcemO36.png)

After:
![](http://i.imgur.com/bDDLaEh.png)

##Edit server.xml
1. open &lt;CATALINA\_BASE&gt;\conf\server.xml.
2. replace 

		<Engine defaultHost="localhost" name="Catalina">
	
	as
		
		<Engine defaultHost="<YOUR_DOMAIN>" name="Catalina">

	or

		<Engine defaultHost="<YOUR_IP>" name="Catalina">
3. replace

		<Host appBase="webapps" autoDeploy="true" name="www.xuesu.tk" unpackWARs="true">
	
	as
		
		<Host appBase="webapps" autoDeploy="true" name="<YOUR_DOMAIN>" unpackWARs="true">

	or

		<Host appBase="webapps" autoDeploy="true" name="<YOUR_IP>" unpackWARs="true">
4. <font color='red'>start &lt;CATALINA\_BASE&gt;\bin\startup.bat.</font>

##Attention
1. eclipse will automically change the server configuration in Tomcat, so need to correct server.xml each time we use eclipse in this workspace.
2. China Telecom ban the direct access of port 80,8080 unless we have put the official records, so I use port 8110.
3. use startup.bat other than directly use tomcat8.exe

