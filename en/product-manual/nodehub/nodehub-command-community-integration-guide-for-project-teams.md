# NodeHub Command Community Integration Guide for Project Teams

***

### 1. Introduction

NodeHub is a decentralized platform designed to support Web3 projects with node deployment, operational collaboration, and compute power sharing. Through the Command Community, project teams can efficiently standardize and automate deployment scripts, rapidly scale their testnet/mainnet nodes, and lower the entry barrier for users.

### 2. Applicable Scenarios

**Early-stage Testnet/Mainnet Projects**: Need to quickly scale up node deployment and attract real users. NodeHub provides high-quality, one-IP-per-device access to effectively mitigate Sybil attack risks and accelerate network bootstrapping.

**Projects with Complex Node Deployment**: Node operations involve complex commands or environment configurations that hinder non-technical users from participating. NodeHub simplifies the process with script-based one-click execution.

**Community Co-building Requirements**: Reduce node operation and maintenance costs through community participation mechanisms while increasing engagement and depth of involvement.

### 3. Integration Process

| Step                    | Description                                              |
| ----------------------- | -------------------------------------------------------- |
| Define Deployment Logic | Clarify detailed steps and requirements for node setup   |
| Submit Integration Form | Provide basic project info and technical requirements    |
| Generate Command Script | NodeHub helps create standardized bash scripts           |
| Launch Internal Testing | Test internally and optimize based on community feedback |

### 4. Required Information Template

| Item                    | Description/Requirements                            |
| ----------------------- | --------------------------------------------------- |
| Project Name            | e.g., 0G Labs                                       |
| Node Type               | Validator / RPC / Full Node, etc.                   |
| Supported Systems       | Ubuntu 22.04 / 24.04                                |
| System Requirements     | 2CPU, 4GB RAM, 16GB ROM                             |
| Deployment Dependencies | Golang, Docker, Make, Python, system packages, etc. |
| Network Requirements    | Fixed ports or outbound access needed               |
| Wallet Configuration    | Need for test tokens / wallet format                |
| Startup Parameters      | Node ID, Token, Key registration needed             |
| Official Resources      | GitHub / documentation / node tutorial links        |
| Contact Person          | For technical support                               |

### 5. Command Script Guidelines

Refer to the [technical documentation](https://docs.node-x.xyz/chan-pin-shou-ce/nodehub/zhi-ling-bian-xie-wen-dang) for command script standards.

### 6. Runtime Environment

All commands are executed within the user’s local environment. NodeHub does **not** host user environments.

Scripts run with the permissions of the user's connected environment by default (should support non-root execution).

### 7. User Execution Flow

* User connects a device
* Executes installation command with one click (via NodeHub)
* Views node status on the node management page (via NodeHub)

### 8. Benefits for Project Teams

* One-click deployment lowers the technical barrier, attracting more non-technical users
* Automation reduces the need for ongoing community tech support
* Seamless user experience prevents technical user churn
* Can be tied to incentive models as part of ecosystem growth metrics

### 9. Contact for Integration

Telegram: [@Rachelbbb](https://t.me/Rachelbbb)\
Email: [node-x@node-x.xyz](mailto:node-x@node-x.xyz)\
Website: [https://hub.node-x.xyz](https://hub.node-x.xyz/)

#### We welcome project teams to submit node deployment information. We will assist in generating standardized command scripts and publishing them to the NodeHub Command Community.

