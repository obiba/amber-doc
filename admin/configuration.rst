Configuration
=============

HTTP Server Configuration
-------------------------


========================= ==================
Property                  Description
========================= ==================
========================= ==================

MongoDB Server Configuration
----------------------------

Amber server will store its data (system configuration, studies, forms, records, etc.) in a MongoDB database. You must specify how to connect to this database.

=========================== ===========================
Property                    Description
=========================== ===========================
``spring.data.mongodb.uri`` MongoDB URI. `Read Standard Connection <https://docs.mongodb.com/manual/reference/connection-string/>`_ String Format to learn more.
=========================== ===========================

By default MongoDB does not require any user name, it is highly recommended to configure the database with a user. This can be done by enabling the Client Access Control procedure.

Follow these steps to enable the Client Access Control on your server:

* create a user with the proper roles on the target databases
* restart the MongoDB service with Client Access Control enabled

.. note::

  Once the MongoDB service runs with Client Access Control enabled, all database connections require authentication.

**MongoDB User Creation Example**

The example below creates the *amberadmin* user for *amber* database:

.. code-block:: javascript

  use admin

  db.createUser( {
    user: "amberadmin", pwd: "amberadmin",
    roles: [
         { "role" : "readWrite", "db" : "amber" },
         { "role" : "dbAdmin", "db" : "amber" },
         { "role" : "readAnyDatabase", "db": "admin" }
    ]
  });

Here is the required configuration snippet in **/etc/amber/application.yml** for the above user:

.. code-block:: yaml

  spring:
    data:
      mongodb:
        uri: mongodb://amberadmin:amberadmin@localhost:27017/amber?authSource=admin

.. note::

  amber requires either **clusterMonitor** or **readAnyDatabase** role on the *admin* database for validation operations. The first role is useful for a cluster setup and the latter if your MongoDB is on a single server.

Miscelaneous Configuration
--------------------------

Advanced settings.

=================================== ================================
Property                            Description
=================================== ================================
``xxx``                             XXXX
=================================== ================================

User Directories
----------------

Reverse Proxy Configuration
---------------------------

Amber server can be accessed through a reverse proxy server.

**Apache**

Example of Apache directives that:

* redirects HTTP connection on port 80 to HTTPS connection on port 443,
* specifies acceptable protocols and cipher suites,
* refines organization's specific certificate and private key.

.. code-block:: text

  <VirtualHost *:80>
      ServerName amber.your-organization.org
      ProxyRequests Off
      ProxyPreserveHost On
      <Proxy *>
          Order deny,allow
          Allow from all
      </Proxy>
      RewriteEngine on
      ReWriteCond %{SERVER_PORT} !^443$
      RewriteRule ^/(.*) https://amber.your-organization.org:443/$1 [NC,R,L]
  </VirtualHost>
  <VirtualHost *:443>
      ServerName amber.your-organization.org
      SSLProxyEngine on
      SSLEngine on
      SSLProtocol All -SSLv2 -SSLv3
      SSLHonorCipherOrder on
      # Prefer PFS, allow TLS, avoid SSL, for IE8 on XP still allow 3DES
      SSLCipherSuite "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+AESG CM EECDH EDH+AESGCM EDH+aRSA HIGH !MEDIUM !LOW !aNULL !eNULL !LOW !RC4 !MD5 !EXP !PSK !SRP !DSS"
      # Prevent CRIME/BREACH compression attacks
      SSLCompression Off
      SSLCertificateFile /etc/apache2/ssl/cert/your-organization.org.crt
      SSLCertificateKeyFile /etc/apache2/ssl/private/your-organization.org.key
      ProxyRequests Off
      ProxyPreserveHost On
      ProxyPass / http://localhost:3030/
      ProxyPassReverse / http://localhost:3030/
  </VirtualHost>

For performance, you can also activate Apache's compression module (mod_deflate) with the following settings (note the json content type setting) in file */etc/apache2/mods-available/deflate.conf*:

.. code-block:: text

  <IfModule mod_deflate.c>
    <IfModule mod_filter.c>
        # these are known to be safe with MSIE 6
        AddOutputFilterByType DEFLATE text/html text/plain text/xml
        # everything else may cause problems with MSIE 6
        AddOutputFilterByType DEFLATE text/css
        AddOutputFilterByType DEFLATE application/x-javascript application/javascript application/ecmascript
        AddOutputFilterByType DEFLATE application/rss+xml
        AddOutputFilterByType DEFLATE application/xml
        AddOutputFilterByType DEFLATE application/json
    </IfModule>
  </IfModule>

Recommended security headers are (to be added to the ``apache2.conf`` file, requires ``headers`` module):

.. code-block:: text

  # Security Headers, see https://securityheaders.com/
  Header set Strict-Transport-Security "max-age=63072000"
  Header set X-Frame-Options DENY
  Header set X-XSS-Protection 1;mode=block
  Header set X-Content-Type-Options nosniff
  Header set Content-Security-Policy "frame-ancestors 'none'"
  Header set Referrer-Policy "same-origin"
  Header set Permissions-Policy "fullscreen=(self)"
  Header onsuccess edit Set-Cookie ^(.+)$ "$1;HttpOnly;Secure;SameSite=Strict"
