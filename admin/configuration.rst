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
``host``                                    Server bind address. Default is ``localhost``.
``port``                                    Server port. Default is ``3030``.
``encrypt_data``                            Whether the collected data are encrypted at rest in the database. Default is ``false``. Overridden by the ``ENCRYPT_DATA`` environment variable.
``encrypt_iv``                              Secret string used to derive the encryption initial vector — **must be changed in production**. Overridden by the ``APP_SECRET_IV`` environment variable.
``mongodb``                                 `MongoDB connection string <https://www.mongodb.com/docs/manual/reference/connection-string/>`_. Overridden by the ``MONGODB_URL`` environment variable. Default is ``mongodb://localhost:27017/amber``.
``client_urls``                             Allowed client URLs (comma separated) for CORS check. Wildcard ``*`` is supported. Overridden by the ``CLIENT_URLS`` environment variable. Default is ``*``.
``amber_studio_url``                        The Amber Studio URL to be included in notification emails. Overridden by the ``AMBER_STUDIO_URL`` environment variable. Default is ``http://localhost:3080``.
``amber_collect_url``                       The Amber Collect URL to be included in notification emails. Overridden by the ``AMBER_COLLECT_URL`` environment variable. Default is ``http://localhost:3090``.
``amber_visit_url``                         The Amber Visit URL to be included in notification emails. Overridden by the ``AMBER_VISIT_URL`` environment variable. Default is ``http://localhost:3070``.
``api_url``                                 The public URL of the Amber Server API. Overridden by the ``APP_URL`` environment variable. Default is ``http://localhost:3030/``.
``recaptcha_secret_key``                    The `reCAPTCHA v3 <https://developers.google.com/recaptcha/docs/v3>`_ secret key. Leave empty to disable CAPTCHA validation. Overridden by the ``RECAPTCHA_SECRET_KEY`` environment variable.
=========================================== =========================================================================

Pagination Settings
~~~~~~~~~~~~~~~~~~~

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``paginate.default``                        Default number of items returned per page. Default is ``10``.
``paginate.max``                            Maximum number of items that can be requested per page. Default is ``10000``.
=========================================== =========================================================================

Signup Settings
~~~~~~~~~~~~~~~

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``signup.whitelist``                        List of email domains allowed to self-register. Use ``*`` as a wildcard to allow all domains. Default is ``["*"]``.
``signup.blacklist``                        List of email domains explicitly blocked from self-registering. Use ``*`` as a wildcard. Default is ``["example.com","example.org"]``.
=========================================== =========================================================================

Authentication Settings
~~~~~~~~~~~~~~~~~~~~~~~

See `Feathers Authentication Service <https://feathersjs.com/api/authentication/service.html#configuration>`_ and `Feathers Local Authentication <https://feathersjs.com/api/authentication/local.html>`_ documentations for more details.

**General**

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.secret``                   The JWT signing secret, also used for encrypting individual data (when enabled). **Must be changed in production.** Overridden by the ``APP_SECRET_KEY`` environment variable.
``authentication.authStrategies``           List of enabled authentication strategies. Default is ``["jwt","local","participant","campaign","apiKey"]``.
``authentication.totp2faRequired``          Whether time-based OTP (TOTP) two-factor authentication is enforced for users. Default is ``true``.
``authentication.otpTimeout``               Validity period in minutes of the email-based OTP. Set to ``0`` to disable email OTP. Default is ``5``. Overridden by the ``OTP_TIMEOUT`` environment variable.
``authentication.activityTimeout``          Duration of inactivity after which a session expires. Default is ``5d``.
=========================================== =========================================================================

**JWT Options**

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.jwtOptions.header.typ``    JWT header ``typ`` claim. Default is ``access``.
``authentication.jwtOptions.audience``      JWT ``aud`` claim — should be set to the application URL in production. Overridden by the ``APP_URL`` environment variable. Default is ``https://example.com``.
``authentication.jwtOptions.issuer``        JWT ``iss`` claim. Overridden by the ``APP_NAME`` environment variable. Default is ``amber``.
``authentication.jwtOptions.algorithm``     JWT signing algorithm. Default is ``HS256``.
``authentication.jwtOptions.expiresIn``     JWT expiration duration. Default is ``60d``.
=========================================== =========================================================================

**Local Strategy**

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.local.usernameField``      Field used as username in the local auth strategy. Default is ``email``.
``authentication.local.passwordField``      Field used as password in the local auth strategy. Default is ``password``.
=========================================== =========================================================================

**Participant / Campaign Strategy**

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.participant.service``      Feathers service used to look up participants. Default is ``participant``.
``authentication.participant.hashSize``     bcrypt hash rounds for participant passwords. Default is ``10``.
``authentication.participant.passwordLength`` Length of the auto-generated participant access code. Default is ``8``.
``authentication.campaign.service``         Feathers service used for campaign-based participant authentication. Default is ``participant``.
``authentication.campaign.hashSize``        bcrypt hash rounds for campaign passwords. Default is ``10``.
``authentication.campaign.passwordLength``  Length of the auto-generated campaign access code. Default is ``8``.
=========================================== =========================================================================

**API Key Strategy**

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.apiKey.allowedKeys``       List of valid API keys for background task triggers — **must be changed in production**. Default is ``["CHANGEME"]``. Overridden by the ``APP_API_KEYS`` environment variable.
``authentication.apiKey.header``            HTTP header name used to carry the API key. Default is ``x-access-token``.
=========================================== =========================================================================

**OAuth / OIDC**

OAuth providers are configured as named sub-objects under ``authentication.oauth``. The provider name becomes part of the OAuth callback URL (e.g. ``/oauth/github/callback``). Provider names starting with ``_`` are ignored (useful for commented-out examples).

The strategy used for each provider is selected automatically:

* A provider named ``github`` uses the GitHub strategy.
* A provider named ``google`` uses the Google strategy.
* Any provider whose config contains ``issuer_url`` uses the generic OIDC strategy (OpenID Connect discovery).
* Any other provider name uses the base OAuth2 strategy.

Role mapping from OAuth/OIDC profiles: if the profile contains a ``groups`` or ``roles`` array, the values ``{app_name}-administrator``, ``{app_name}-manager``, and ``{app_name}-interviewer`` are mapped to the corresponding Amber roles. All other authenticated users receive the ``guest`` role.

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.oauth.origins``            Allowed OAuth redirect origins. Default is ``[]``.
``authentication.oauth.redirect``           URL to redirect to after a successful OAuth login. Default is ``/``.
``authentication.oauth.github.key``         GitHub OAuth App client ID. Overridden by the ``GITHUB_KEY`` environment variable.
``authentication.oauth.github.secret``      GitHub OAuth App client secret. Overridden by the ``GITHUB_SECRET`` environment variable.
``authentication.oauth.google.key``         Google OAuth client ID. Overridden by the ``GOOGLE_KEY`` environment variable.
``authentication.oauth.google.secret``      Google OAuth client secret. Overridden by the ``GOOGLE_SECRET`` environment variable.
=========================================== =========================================================================

For a generic OIDC provider (any name other than ``github`` / ``google`` that includes ``issuer_url``):

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``authentication.oauth.<name>.key``         OIDC client ID. Overridden by the ``OIDC_KEY`` environment variable.
``authentication.oauth.<name>.secret``      OIDC client secret. Overridden by the ``OIDC_SECRET`` environment variable.
``authentication.oauth.<name>.issuer_url``  OIDC issuer URL used for discovery and UserInfo endpoint resolution (e.g. ``https://your-idp/realms/myrealm``). Overridden by the ``OIDC_ISSUER_URL`` environment variable.
``authentication.oauth.<name>.authorize_url`` *(optional)* Override for the authorization endpoint.
``authentication.oauth.<name>.access_url``  *(optional)* Override for the token endpoint.
``authentication.oauth.<name>.scope``       *(optional)* Array of OIDC scopes (e.g. ``["openid","email","profile"]``). Overridden by the ``OIDC_SCOPE`` environment variable.
``authentication.oauth.<name>.nonce``       *(optional)* Whether to include a nonce in the authorization request. Overridden by the ``OIDC_NONCE`` environment variable. Default is ``false``.
=========================================== =========================================================================

Notification Email Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Mail Service**

By default, the mail service connects to an SMTP server. Alternatively, other mail transport providers can be used: the SMTP settings can be overridden by the ``GMAIL``/``GMAIL_PASSWORD`` environment variables (Gmail), or by the ``BREVO_API_KEY`` environment variable (Brevo, formerly Sendinblue).

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
``from_email``                                    The sender's email address. Default is ``no-reply@example.org``. Overridden by the ``FROM_EMAIL`` environment variable.
``email_templates.otp``                           Sent to a user when an email-based OTP is issued.
``email_templates.notifySignup``                  Sent to administrators when a new user signs up.
``email_templates.resendVerifySignup``            Sent to a user with a new email verification link.
``email_templates.verifySignup``                  Confirmation sent to a user after their email is verified.
``email_templates.sendResetPwd``                  Sent to a user with a password-reset link.
``email_templates.resetPwd``                      Confirmation sent to a user after a successful password reset.
``email_templates.passwordChange``                Notification sent to a user after their password changes.
``email_templates.infoParticipantsAboutToInit``   Sent to interviewers before participant accounts are activated.
``email_templates.initParticipants``              Sent to interviewers when new participant accounts are activated.
``email_templates.infoParticipantsAboutToExpire`` Sent to interviewers when participant accounts are close to expiring.
``email_templates.remindParticipants``            Periodic reminder sent to interviewers about incomplete interviews.
``email_templates.summaryParticipants``           Summary of participant progress for a campaign.
``email_templates.interviewCompleted``            Sent to interviewers when a participant completes an interview.
=========================================== =========================================================================

Tasks Settings
~~~~~~~~~~~~~~

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``tasks.delimiter``                         Column delimiter used in CSV task files. Default is ``;``.
``tasks.extension``                         File extension expected for task files. Default is ``.csv``.
=========================================== =========================================================================

Other Settings
~~~~~~~~~~~~~~

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``export.entity_type``                      Entity type label used in data exports. Default is ``Participant``.
``export.identifier_variable``              Variable name used as the participant identifier in exports. Default is ``id``.
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
