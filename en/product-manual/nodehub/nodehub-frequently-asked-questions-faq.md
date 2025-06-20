# NodeHub Frequently Asked Questions (FAQ)

#### Q: What is NodeHub?

**A:** NodeHub is the core software platform of the Node-X ecosystem, designed to optimize decentralized computing and node management. It supports both mobile and web interfaces, offering one-click deployment, batch server management, and real-time monitoring. NodeHub simplifies node operations and enhances efficiency. By integrating a command-sharing community and a points-based incentive system, it lowers the entry barrier for everyday users, boosts trust for project teams, and drives overall network activity.

***

#### Q: What problems does NodeHub solve?

**A:**

* Complex deployment and uneven compute resource allocation hinder efficient management.
* Tedious workflows and low task execution efficiency increase operational complexity.
* Limited community collaboration reduces user participation and stifles ecosystem growth.
* Project teams face challenges identifying fake or inactive nodes, leading to high trust costs.

***

#### Q: How do I register for NodeHub?

**A:** Go to [https://hub.node-x.xyz/](https://hub.node-x.xyz/) and simply sign up to log in

***

#### Q: How can I become a command creator?

**A:** You can apply through the "User Center." Once your application is approved, you’ll be able to create and publish custom commands.

***

#### Q: How do I add a server?

**A:**\
Navigate to **Server List > Add**, then fill in the following:

* Custom server name
* System type (default: Ubuntu)
* Server IP address
* SSH port (default: 22)
* Username (usually `root` or `ubuntu`)
* Server password

***

#### Q: How do I batch import servers?

**A:**\
Navigate to **Server List > Import**\
Steps:

* Download the template
* Fill in the server details as specified in the header
* Upload the file to import servers in bulk

***

#### Q: What should I do if server installation fails?

**A:** Please double-check your username and password. The most common usernames are `root` and `ubuntu`.

***

#### Q: Why does it show “Healthy” but “Offline” after running a command?

**A:**

* If using an **official built-in command**, there may be issues with the script itself.
* If using a **custom command**, the creator’s script may contain errors.\
  You're encouraged to leave feedback or questions in the comment section to facilitate resolution.

***

#### Q: Why does it show “Unhealthy” or “Offline” after running a command?

**A:**

**1.Command Not Yet Configured**\
The creator has not completed the setup of this command, resulting in execution failure.

**2.Script Errors in the Command**\
The command contains logical or syntactical errors that prevent proper execution.

&#x20;**Status Check**: Missing expected outputs such as\
`<process_name> is running (PID: xxxx)` or\
`<process_name> is not running`.

**Health Check**:

* No boolean return (true/false);
* Contains disruptive statements such as `exit 1`.

**3.Server-Side Issues**\
The target server may have network issues, insufficient resources, or unreachable SSH ports, causing the node to be undetectable.

**4.Manual Termination or Uninstallation by the User**\
The user manually stopped or removed the service via terminal/SSH, causing the system to lose tracking of the project.

**5.Project Process Has Terminated Unexpectedly**\
The service or container is no longer running due to crash, exit, or abnormal shutdown, leading to an unhealthy status.

**6.Project Has Ended or Been Closed by the Project Team**\
The project has completed its lifecycle or has been intentionally taken down by the project owner.

**7.Only Status Check Was Executed Without Installation**\
The installation command was not executed prior to the status check, resulting in incomplete deployment and failure in validation.
