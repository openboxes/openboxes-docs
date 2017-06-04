Configuration
=============

openboxes-config.properties (sample)
------------------------------------

::

    # Database connection settings
    dataSource.url=jdbc:mysql://localhost:3306/openboxes
    dataSource.username=openboxes
    dataSource.password=openboxes

    # OpenBoxes administrator emails
    openboxes.admin.email=justin.miranda@gmail.com,jmiranda@pih.org
     
    # Only used on local machines when dataSource.url is overriden
    openboxes.fixtures.enabled=false
     
    # OpenBoxes Identifier Formats 
    # N: Numeric, L: Letter, A: Alphanumeric
    # For example, NNNLLL might lead to the following random identifier being generated 123ABC.
    openboxes.identifier.order.format = NNNLLL
    openboxes.identifier.product.format = LLNN
    openboxes.identifier.requisition.format = NNNLLL
    openboxes.identifier.shipment.format = NNNLLL
    openboxes.identifier.transaction.format = AAA-AAA-AAA
     
    # OpenBoxes Identifier Characters
    openboxes.identifier.numeric = 0123456789
    openboxes.identifier.alphabetic = ABCDEFGHJKMNPQRSTUVXYZ
    openboxes.identifier.alphanumeric = 0123456789ABCDEFGHJKMNPQRSTUVWXYZ
     
    # Report logo header (not supported yet)
    # openboxes.report.header.logo = file:///home/jmiranda/Desktop/images.jpg
    openboxes.report.header.logo = http://localhost:8080/openboxes/images/hands.jpg
    openboxes.report.header.title = OpenBoxes
     
    # OpenBoxes Error Email feature (bug report)
    # Use your own address if you want to handle bug reports yourself. Otherwise leave as-is and OpenBoxes
    # support these support requests.
    openboxes.mail.errors.enabled = true
    openboxes.mail.errors.recipients = support@openboxes.com

    # OpenBoxes Barcode Scanner detection 
    # NOTE: This feature is an experimentation. If enabled you can scan barcode on any page and the app will 
    # try to locate an object (product, shipment, etc) that is associated with that barcode. If an object is 
    # found, the app just redirects to the details page for that database object. In the future, I'm hoping to 
    # improve the barcode scanner to integrate with workflows (e.g. add item to purchase order). 
    openboxes.scannerDetection.enabled = true
     
    # Used to specify default roles for newly registered users (implies automatic activation)
    #openboxes.signup.defaultRoles=ROLE_MANAGER,ROLE_ASSISTANT
      
    # General mail settings
    grails.mail.enabled=true
    grails.mail.host=<smtp server>
    grails.mail.port=<smtp port>
    grails.mail.username=<username>
    grails.mail.password=<password>
    grails.mail.from=<from address>
     
    # Example of general mail settings 
    #grails.mail.default.from=username@gmail.com
    #grails.mail.host=smtp.gmail.com
    #grails.mail.port=465
    #grails.mail.username=username@gmail.com
    #grails.mail.password=password
    #grails.mail.props = ["mail.smtp.auth":"true", "mail.smtp.socketFactory.port":"465", "mail.smtp.socketFactory.class":"javax.net.ssl.SSLSocketFactory", "mail.smtp.socketFactory.fallback":"false"]

    # Error email properties
    mail.error.debug=true
    mail.error.server=<smtp server>
    mail.error.username=<smtp username>
    mail.error.password=<smtp password>
    mail.error.port=<smtp port>
    mail.error.to=<to address>

    # Example of error email properties 
    #mail.error.server=localhost
    #mail.error.server=smtp.pih.org
    #mail.error.username=openboxes
    #mail.error.password=password
    #mail.error.to=justin.miranda@gmail.com
    #Possible values: default|dynamic|alternate
    mail.error.appender=dynamic

    # OpenBoxes > Choose Location > Required Activities
    # The supported activities required in order for a location a location to show up on Choose Location page.
    # Possible values: MANAGE_INVENTORY, PLACE_ORDER, PLACE_REQUEST, FULFILL_ORDER, FULFILL_REQUEST, SEND_STOCK, RECEIVE_STOCK, EXTERNAL
    openboxes.chooseLocation.requiredActivities = MANAGE_INVENTORY

    # Amazon web service (not supported yet)
    aws.s3.domain=s3.amazonaws.com
    aws.s3.accessKey=0123456789ABCDEFG
    aws.s3.secretKey=0123456789ABCDEFGHIJKLMNOPQRS
    aws.s3.bucketName=files

    # Google Product Search (no longer supported -- Google deprecated API)
    # URL: https://www.googleapis.com/shopping/search/v1/public/products?key=${google.productSearch.key}&country=US&q=${q}&alt=scp&crowdBy=brand:1
    google.api.key=<no longer supported>

    # Hipaaspace.com NDC Lookup (not supported yet)
    hipaaspace.api.key=<not supported yet>

    # RXNorm (not supported yet)
    # URL: http://rxnav.nlm.nih.gov/REST/
    rxnorm.api.key=<not supported yet>

    # Google analytics
    google.analytics.enabled = false 
    google.analytics.webPropertyID = <enter your google analytics property ID>

Configuration file location
---------------------------

As mentioned in the installation instructions, you can override
application configuration properties by creating a file called
``$USER_HOME/.grails/openboxes-config.properties``. If you are a
developer, ``$USER_HOME`` should resolve to your home directory (e.g.
``/home/jmiranda`` on Ubuntu). If you are deploying the application to
Tomcat, the file is usually located under the
``TOMCAT_HOME/.grails/openboxes-config.properties``.

If you are having trouble locating where the application is looking for
the file you can determine the path by deploying the application to
Tomcat and checking the log file. The first few lines of the Tomcat
catalina.out file display the path(s) being used. You can safely ignore
the "Unable to load specified config location" for the locations that
you are not using. Notice below that there are 4 configuration locations
and only 3 ``Unable to load specified config location`` lines. That
means that there was a file found at one of the locations (namely,
``file:/usr/local/tomcat6/.grails/openboxes-config.properties``.

::

    INFO: Deploying web application archive openboxes.war
    Using configuration locations [classpath:openboxes-config.groovy, classpath:openboxes-config.properties, 
    file:/usr/local/tomcat6/.grails/openboxes-config.groovy, file:/usr/local/tomcat6/.grails/openboxes-
    config.properties] [staging]
    Unable to load specified config location classpath:openboxes-config.groovy : class path resource 
    [openboxes-config.groovy] cannot be opened because it does not exist
    Unable to load specified config location classpath:openboxes-config.properties : class path resource 
    [openboxes-config.properties] cannot be opened because it does not exist
    Unable to load specified config location file:/usr/local/tomcat6/.grails/openboxes-config.groovy : 
    /usr/local/tomcat6/.grails/openboxes-config.groovy (No such file or directory)

Configuration properties
------------------------

Database connection properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------------+------------+--------------------------+
| Setting                   | Required   | Description              |
+===========================+============+==========================+
| ``dataSource.url``        | Yes        | JDBC connection string   |
+---------------------------+------------+--------------------------+
| ``dataSource.username``   | Yes        | JDBC username            |
+---------------------------+------------+--------------------------+
| ``dataSource.password``   | Yes        | JDBC password            |
+---------------------------+------------+--------------------------+

Example
^^^^^^^

::

    dataSource.url=jdbc:mysql://localhost:3306/openboxes
    dataSource.username=<username>
    dataSource.password=<password>

Application properties
~~~~~~~~~~~~~~~~~~~~~~

+-------+-------+-------+-------+
| Setti | Requi | Descr |
| ng    | red   | iptio |
|       |       | n     |
+=======+=======+=======+=======+
| openb | No    | Used  |
| oxes. |       | to    |
| signu |       | speci |
| p.def |       | fy    |
| aultR |       | defau |
| oles  |       | lt    |
|       |       | roles |
|       |       | assig |
|       |       | ned   |
|       |       | to    |
|       |       | newly |
|       |       | regis |
|       |       | tered |
|       |       | users |
|       |       | (impl |
|       |       | ies   |
|       |       | autom |
|       |       | atic  |
|       |       | activ |
|       |       | ation |
|       |       | ).    |
|       |       | Shoul |
|       |       | d     |
|       |       | only  |
|       |       | be    |
|       |       | used  |
|       |       | in    |
|       |       | cases |
|       |       | where |
|       |       | you   |
|       |       | eithe |
|       |       | r     |
|       |       | trust |
|       |       | your  |
|       |       | regis |
|       |       | tered |
|       |       | users |
|       |       | (e.g. |
|       |       | app   |
|       |       | is    |
|       |       | runni |
|       |       | ng    |
|       |       | on    |
|       |       | LAN)  |
|       |       | or    |
|       |       | you   |
|       |       | don't |
|       |       | care  |
|       |       | what  |
|       |       | users |
|       |       | are   |
|       |       | allow |
|       |       | ed    |
|       |       | to do |
|       |       | (e.g. |
|       |       | demo  |
|       |       | serve |
|       |       | r).   |
+-------+-------+-------+-------+
| openb | No    | Not   |
| oxes. |       | curre |
| syste |       | ntly  |
| m.def |       | suppo |
| aultT |       | rted. |
| imezo |       |       |
| ne    |       |       |
+-------+-------+-------+-------+
| openb | No    | Only  |
| oxes. |       | used  |
| fixtu |       | on    |
| res.e |       | local |
| nable |       | machi |
| d     |       | nes   |
|       |       | when  |
|       |       | dataS |
|       |       | ource |
|       |       | .url  |
|       |       | is    |
|       |       | overr |
|       |       | iden. |
|       |       | When  |
|       |       | set   |
|       |       | to    |
|       |       | true  |
|       |       | this  |
|       |       | will  |
|       |       | trigg |
|       |       | er    |
|       |       | the   |
|       |       | creat |
|       |       | ion   |
|       |       | of    |
|       |       | data  |
|       |       | fixtu |
|       |       | res   |
|       |       | used  |
|       |       | for   |
|       |       | testi |
|       |       | ng.   |
+-------+-------+-------+-------+

Example
^^^^^^^

::

    openboxes.fixtures.enabled=false
    openboxes.signup.defaultRoles=ROLE_MANAGER,ROLE_ASSISTANT
    openboxes.system.defaultTimezone=America/Chicago

Email configuration
~~~~~~~~~~~~~~~~~~~

The default email configuration properties.

::

    grails.mail.host=localhost
    grails.mail.port=25

Add the following properties if you want to use a service like Mandrill
as your SMTP server.

::

    grails.mail.enabled=true
    grails.mail.debug=true
    grails.mail.from=<from-email>
    grails.mail.host=smtp.mandrillapp.com
    grails.mail.port=587
    grails.mail.username=<username>
    grails.mail.password=<password>

Add the following properties if you want to use Gmail as your SMTP
server.

::

    grails.mail.enabled=true
    grails.mail.debug=true
    grails.mail.from=<from-email>
    grails.mail.host=smtp.gmail.com
    grails.mail.port=465
    grails.mail.username=<your-username>
    grails.mail.password=<password-generated-from-google-accounts>
    grails.mail.props = ["mail.smtp.auth":"true", "mail.smtp.socketFactory.port":"465", "mail.smtp.socketFactory.class":"javax.net.ssl.SSLSocketFactory", "mail.smtp.socketFactory.fallback":"false"]

NOTE: I have not been able to able to get the Gmail configuration to
work, but I'm sure someone with more time and intelligence will have no
trouble figuring it out.

Identifier Formats
~~~~~~~~~~~~~~~~~~

You can configure all of the identifiers according to your
specifications (N = Numeric, L = Letter, A = Alphanumeric). The default
configuration looks like the following, but feel free to configure
identifiers however you'd like. Once the format has been choosen, values
for these identifiers are randomly generated when an item is created.
There's also a Quartz process that runs in the background that generates
a unique identifier for any object that does not currently have one.

::

    openboxes.identifier.order.format = NNNLLL
    openboxes.identifier.product.format = LLNN
    openboxes.identifier.requisition.format = NNNLLL
    openboxes.identifier.shipment.format = NNNLLL
    openboxes.identifier.transaction.format = AAA-AAA-AAA
