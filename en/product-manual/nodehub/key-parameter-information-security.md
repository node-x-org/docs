# Key Parameter Information Security

<p align="right"><a href="https://docs.node-x.xyz/chan-pin-shou-ce/nodehub/yong-hu-guan-jian-can-shu-zi-xun-ji-vps-mi-ma-an-quan">中文</a></p>

*   ## Key Parameter Information Security

    ### 1. Parameter Storage Security

    The parameters you enter on NodeHub are encrypted and stored on our servers. Only the user can view their plain text parameters. Even if others obtain the data, they will only see the encrypted form and will not be able to decrypt or view the actual content.

    #### Why is it necessary to store parameters?

    Storing certain data helps streamline future operations. Specifically, it serves the following purposes:

    * **Deployment Retry**: If deployment fails, users can quickly retry using the saved parameters, improving operational efficiency.
    * **Issue Tracing**: Saved parameters assist in analyzing and troubleshooting issues that may arise during deployment.
    * **Convenient Redeployment**: For subsequent deployments, users do not need to re-enter the same parameters, saving time and effort.

    ### 2. Additional Security Features

    We plan to introduce the following security features in the future:

    * **One-click Parameter Clearance**: Users can clear their saved parameters at any time, ensuring data privacy is not compromised.
    * **Secondary Authentication Mechanism**: For critical data, we will introduce dual encryption and other secondary verification methods. Users will need to set up a security key or enable two-factor authentication (2FA) to access related data, further enhancing data security.

    ### 3. Security Tips

    Although we have implemented multiple security measures to protect user parameters and data, we still strongly recommend:

    * Using a new wallet for all projects involving private keys.
    * Properly safeguarding your account password and avoiding using the same password across multiple platforms or environments.

    **Summary of Security Tips**: Data security is our top priority. NodeHub continuously improves its encryption storage, dual authentication, and other measures to ensure security. We always advise users to adopt the strictest security practices to protect their accounts and private keys.
