# Azure IoT Solution Accelerators Workshop

Use templates to create fully customizable solutions for common Internet of Things (IoT) scenarios—Bring your business together in insightful new ways—from increasing process efficiencies to delivering better customer experiences and generating new revenue streams. 

Get started quickly building your IoT solutions with the IoT solution accelerators. Add new devices and connect existing ones using device SDKs for multiple platforms, including Linux, Windows, and real-time operating systems. Easily scale from just a few sensors to millions of simultaneously connected devices and rely on the global availability of Azure, no matter how large or small your project.

## In this lab you will

* How to deploy the Azure IoT Remote Monitoring solution accelerator
  * Option 1: [Create Remote Monitoring Solution using website](#create-remote-monitoring-solution-using-website)
  * Option 2: [Create Remote Monitoring Solution using CLI](#Create-Remote-Monitoring-Solution-using-CLI)
* Use the solution Dashboard page to visualize simulated and real devices on a map, and the 
* Wear an operator hat and perform tasks from Web UI
* Learn to use an external Simulator to connect to Accelerator and send Data
* Learn to extend the solution to Time Series Insights and Data Lake Store

## Create Remote Monitoring Solution using website

Go To [Azure IoT Solutions Website](http://azureiotsolutions.com/). You will be creating and working with Remote Monitoring solution accelerator in this workshop.

![Solutions](images/solutions.png)

**Sign in** to the website.

![Signin](images/signin.png)

Click on **Your Solution Accelerators** button.

![Signin](images/yoursolutionacceleration.png)

Create a new solution.

![Create New Solution](images/createnewsolution.png)

Click on **Try now** button.

![Try now](images/trynow.png)

Create Remote Monitoring Solution.

For this workshop select **Basic** deployment option.

You have the choice of selecting a language

1. .NET
2. Java

Provide a solution name, select your subscription and region to deploy the solution. The **Details** button will be greyed out till the provisioning is in progress.

>**Make sure you provide a unique solution name when you provision a solution. Try to use your initials and a unique number so you dont have a name conflict with other workshop participants.**

![Provisioning](images/01provision.png)

Click **Create Solution** button.

Takes a few minutes to deploy the solution. Status of the solution creation can be seen on the website.

![Provisioning Details](images/02provision_submitted.png)

Click on the solution card you submitted to see the status of the provisioning. When the **Launch** button is greyed out provisioning is still in progress.

![Provisioning Details](images/03provisioning.png)

### Launch the Solution

After solution provisioning is complete **Launch** button is enabled.

Click **Launch** button.

![Launch](images/04launch.png)

You will be asked to provide permissions to read profile. Click **Accept** button

![Launch](images/05accept.png)

You will land on Remote Monitoring dashboard.

![Launch](images/06dashboard.png)

Filter to view **Chillers**

![Launch](images/chillers.png)

![Launch](images/chillerdash.png)

Go back to All Devices View by clicking on **All Devices** in the drop down.

### Manage Device Groups

Create a new device group by clicking on **Manage Device Groups** and click on **Create new device group** 

![Launch](images/07createnewdevicegroup.png)

Create a new **externalsimulators** device group. Remove condition.

![Launch](images/07aremovecondition.png)

Click **Save**

![Launch](images/08savegroup.png)

New device group is created and is part of the device group list.

![Launch](images/09externalsimulators.png)

Go To **Devices** from left menu. Click on **New Device**.

![Launch](images/10newdevice.png)

Select a **Physical** device and enter device id and click **Apply**.

![External Device](images/11piexternal.png)

Copy the connection string primary key

![Primary Connection String](images/12copyprimaryconnstring.png)

![Primary Connection String](images/13copyprimarystring.png)

Click on the link below to go to the PI Simulator

[PI Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

Replace the connection string with the primary key connection string copied in the previous steps

![Raspberry Pi Simulator](images/14raspberrypisimulator.png)

After you copy the connection string should look like below

![Run](images/15run.png)

Click **Run** and start sending messages. LED will start blinking

![MEssage](images/16json.png)

Device will be in connected status in the web ui if you refresh the web page.

click on the device to see device details. Click on **see raw message** to see the JSON data details.

![Pi Details](images/pidetails.png)

### Create new Rule

Click on **Rules** on the left navigation and create a new rule by clicking on **New Rule**

![New Rule](images/17newrule.png)

Create new rule for Pi Simulator

![Create New Rule](images/18rule.png)

New rule created is listed in the rule list

![Create New Rule](images/19rulelist.png)

### Maintenance

Click on **Maintenancce** on the left navigation.

![Maintenance](images/20maintenance.png)

Alerts generated will be listed. You can see alerts generated for Pi Simulator

![Maintenance](images/20maintenance.png)

Select an alert and click on **Acknowledge**.

![Acknowledge](images/22acknowledge.png)

Status will change to Acknowledged

![Acknowledged](images/23acknowledged.png)

Change status of the alert to closed by clicking on **Close**. Status will change to Closed

![Acknowledged](images/24closed.png)

## Create Remote Monitoring Solution using CLI

### Prerequisites
* [nodejs](https://nodejs.org/) used as the runtime for the CLI.  Please install node before attempting a deployment.
* [kubectl](https://kubernetes.io/docs/tasks/tools/#install-kubectl-binary-using-curl) **select the tab specific to your OS**
* [Azure Subscription](https://azure.microsoft.com/free/) (also see [permissions guidelines](https://docs.microsoft.com/azure/iot-suite/iot-suite-permissions)). **Can be skipped if redeemed demo code**

### Install and run the CLI
1. `npm install -g iot-solutions`
1. `pcs login`
![login-image](images/pcslogin.png)
1. `pcs -t remotemonitoring -s standard -r dotnet`
![standard-deployment](images/standard-ongoing.png)
1. Successfull deployment
![done](images/standard-done.png)

### Kubectl setup
#### Rename config-*{solutionname}*-cluster to config where *solutionname* is your solution name from step 1 of standard deployment
1. `cd .kube`
1. `move config-{solutionname}-cluster config`

### Kubectl Dashboard
1. `kubectl proxy` This should start service dashboard on localhost
1. Click this url: http://127.0.0.1:8001/api/v1/namespaces/kube-system/services/kubernetes-dashboard/proxy/
