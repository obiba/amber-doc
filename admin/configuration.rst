Configuration
=============

Amber Server
------------

See the `config/default.json <https://github.com/obiba/amber/blob/main/config/default.json>`_ settings in the source code for reference.

Some of these settings can be overridden by environment variables (``.env`` file supported, see `Dotenv <https://www.dotenv.org/>`_). The list of the environment variables is described in the `Amber Environment Variables <https://github.com/obiba/amber/blob/main/README.md#environment-variables>`_ documentation.

Main Settings
~~~~~~~~~~~~~

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``host``                                    Default is "localhost"
``port``                                    Default is ``3030``.
``encrypt_data``                            Whether the collected data are encrypted in the database. Default is ``false``.
``encrypt_iv``                              Encryption initial vector, to be modified. Overridden by the ``APP_SECRET_IV`` environment variable.
``mongodb``                                 `MongoDB connection string <https://www.mongodb.com/docs/manual/reference/connection-string/>`_. Overridden by the ``MONGODB_URL`` environment variable. Default is "mongodb://localhost:27017/amber"
``client_urls``                             Allowed client URLs (comma separated) for CORS check. Wildcard "*" is supported. Overridden by the ``CLIENT_URLS`` environment variable. Default is "*".
``amber_studio_url``                        The Amber Studio URL to be included in notification emails. Default is "http://localhost:3080".
``amber_collect_url``                       The Amber Studio URL to be included in notification emails. Default is "http://localhost:3090".
``api_url``                                 The Amber Server URL. Overridden by the ``APP_URL`` environment variable. Default is ": "http://localhost:3030/".
``recaptcha_secret_key``                    The `reCAPTCHA v3 <https://developers.google.com/recaptcha/docs/v3>`_ secret key. Overridden by the ``RECAPTCHA_SECRET_KEY`` environment variable.
=========================================== =========================================================================

Authentication Settings
~~~~~~~~~~~~~~~~~~~~~~~

See `Feathers Authentication Service <https://feathersjs.com/api/authentication/service.html#configuration>`_ and `Feathers Local Authentication <https://feathersjs.com/api/authentication/local.html>`_ documentations for more details.

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.secret``                   The authentication token (JWT) signing secret, also used for encrypting individual data (when enabled). Overridden by the ``APP_SECRET_KEY`` environment variable.
``authentication.jwtOptions.audience``      The JWT audience field. Overridden by the ``APP_URL`` environment variable. Default is "https://example.com".
``authentication.jwtOptions.issuer``        The JWT issuer field. Overridden by the ``APP_NAME`` environment variable. Default is "amber".
``authentication.jwtOptions.expiresIn``     Timeout after which the authentication token (JWT) expires. Default is ``60d``.
``authentication.totp2faRequired``          Whether the two-factor mechanism "Time based One Time Password" is enabled. Default is ``true``.
``authentication.activityTimeout``          Timeout after which the authentication token (JWT) expires when not used. Default is ``5d``.
=========================================== =========================================================================

Notification Email Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Mail Service**

By default, the mail service tries to connect to a SMTP server. Alternatively, other mail transport providers can be used: the SMTP server settings can be overridden by the the ``GMAIL``/``GMAIL_PASSWORD`` or the ``SENDINBLUE_API_KEY`` environment variables if defined. See `sendinblue docs <https://developers.sendinblue.com/docs>`_ for more details on this service.

See `Nodemailer SMTP <https://nodemailer.com/smtp/>`_ documentation for more details.

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``smtp.host``                               The SMTP server host name.
``smtp.name``                               The SMTP server (optional) name.
``smtp.user``                               The SMTP server user name.
``smtp.pw``                                 The SMTP server user password.
``smtp.secure``                             The SMTP server secure flag. Default is ``true``.
``smtp.require_tls``                        Whether SMTP server requires TLS. Default is ``false``.
``smtp.logger``                             Whether SMTP server logging is enabled. Default is ``false``.
``smtp.debug``                              Whether SMTP server debug is enabled. Default is ``false``.
=========================================== =========================================================================

**Mail Templates**

Mail templates are defined per language. They can be specified inline or in separate files.

Example of the ``resetPwd`` email template specified inline:

.. code-block:: json

  {
    "en": {
      "subject": "[{app_name}] Successfully Reset Password",
      "html": "<html><p>Dear {firstname} {lastname},</p> <p>The password was reset successfully.</p> <p>---<br/>This email was automatically sent, please do not reply.</p></html>"
    }
  }

Example of the ``resetPwd`` email template specified in a local file:

.. code-block:: json

  {
    "en": {
      "subject": "[{app_name}] Successfully Reset Password",
      "file": "/path/to/resetPwd-en-template.html"
    }
  }

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``from_email``                              The sender's email address. Default is "no-reply@example.org".
``email_templates.notifySignup``            Informs the administrators that a new user has signed up.
``email_templates.resendVerifySignup``      Sends link to verify email after sign up (resent).
``email_templates.verifySignup``            Sends link to verify email after sign up.
``email_templates.sendResetPwd``            Sends link to reset password email.
``email_templates.resetPwd``                Informs the password was reset successfully.
``email_templates.passwordChange``          Informs the password was updated successfully.
=========================================== =========================================================================

Other Settings
~~~~~~~~~~~~~~

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``export.entity_type``                      Entity type to be specified in the exported data dictionary. Default is "Participant".
``export.identifier_variable``              Identifier variable name to be used in the exported dataset: Default is "id".
=========================================== =========================================================================

Amber Studio
------------

Amber Studio is a Single Page Application (SPA) that needs to be built specifically for the deployment environment (Amber server URL and reCAPTCHA site key are to be provided). Then the configuration is used in the build phase. To facilitate the customization of the app, the `Amber Studio's settings.json <https://github.com/obiba/amber-studio/blob/main/settings.json>`_ can be amended.

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``theme``                                   Some CSS classes to be applied on different components to minimally alter the style.
``licenses``                                Licenses that can be applied to forms.
``i18n``                                    Translations, per language. New languages can be added.
=========================================== =========================================================================

Amber Collect
-------------

Amber Collect is a Single Page Application (SPA) that needs to be built specifically for the deployment environment (Amber server URL and reCAPTCHA site key are to be provided). Then the configuration is used in the build phase. To facilitate the customization of the app, the `Amber Collect's settings.json <https://github.com/obiba/amber-collect/blob/main/settings.json>`_ can be amended.

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``theme``                                   Some CSS classes to be applied on different components to minimally alter the style.
``lock``                                    Lock feature can be enabled, with an optionally shuffled numeric pad.
``links``                                   Useful links.
``licenses``                                Licenses that were applied to forms.
``i18n``                                    Translations, per language. New languages can be added.
=========================================== =========================================================================


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
  Header set X-Permitted-Cross-Domain-Policies "none"
  Header set Expect-CT: max-age=0
  Header onsuccess edit Set-Cookie ^(.+)$ "$1;HttpOnly;Secure;SameSite=Strict"
