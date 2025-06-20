# Key Parameter Information Security

* **Parameter Storage Security**\
  The parameters you fill in are securely stored on the server in an encrypted form. Only the user can view their parameters in plain text; others will only see the data in ciphertext, even if they obtain it.
* **Why Are Parameters Stored?**\
  Storing certain data helps to:
  * **Retry Deployment in Case of Failure**: It allows you to quickly retry the deployment if it fails.
  * **Trace Issues**: It helps analyze and troubleshoot problems.
  * **Ease of Re-deployment**: When deploying again, the user won’t need to re-enter the same parameters.
* **Additional Security Features**\
  We will introduce a “One-click Clear Parameters” function in the future, and we will also implement secondary verification for critical data (such as double encryption). Users will need to set a security key or enable two-factor authentication (2FA) to access the data.
* **Security Tips**\
  Although we have implemented several security measures, we strongly recommend using a new wallet for any project involving private keys. Please also ensure the security of your account and password.
