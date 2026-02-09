# aily blockly Offline Service  
`This program is for educational purposes only, commercial use is prohibited`  
aily blockly offline service can cache all aily blockly resources to local computers, allowing users to use aily blockly related development boards, libraries and other resources in an offline environment.

## Quick Start
0. Download [nodejs](https://npmmirror.com/mirrors/node/v22.21.1/node-v22.21.1-x64.msi), and install.  
1. Download [aily blockly offline service program](https://github.com/ailyProject/aily-blockly-offline-service/archive/refs/heads/main.zip), and extract
2. Enter the extracted directory, right-click the blank space, select `Open in Terminal`, run the following command to `install related dependencies`:
```shell
npm i
```
> Only the first time using this service, you need to install dependencies  

3. Use the following command to `run the offline service`:  
```shell
node cli.js run
```
> After every reboot, you can use this command to enable the offline service.  

4. Run the following command to `update the local npm repository and related resources`:  
```shell
node cli.js update
```
> After every time you need to update the npm repository, you can use this command

5. Open aily blockly software, through the upper left menu, open the `Settings` window, click `Service Region`, select `Local`.

Now the configuration is complete, you will use the local service when creating new projects and installing libraries in the software.

## Stop Service
Run the following command to stop the service
```shell
node cli.js stop
```
In aily blockly settings, you can modify the repository settings to use the official cloud service  

## Project Address  
[Github](https://github.com/ailyProject/aily-blockly-offline-service)  
