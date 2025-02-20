# Setup Instructions


### Prerequisites

In order to run the SDAccel AWS F1 Developer Labs, you will need the following:

<details>
<summary><strong>An AWS account</strong> <i>(expand for details)</i></summary><p>

If you do not already have an Amazon Web Services (AWS) account, create one here: [https://aws.amazon.com/](https://aws.amazon.com)
<p></details><br>
<details>
<summary><strong>Access to AWS F1 instances</strong> <i>(expand for details)</i></summary><p>

AWS users need to request access to use F1 instances. Here are the steps to do so:

* Open the Service Limit Increase form: [http://aws.amazon.com/contact-us/ec2-request](http://aws.amazon.com/contact-us/ec2-request)
* Make sure your account name is correct
* Submit a 'Service Limit Increase' for 'EC2 Instances'
* Select the region where you want to access F1 instances: US East (N.Virginia), US West (Oregon) or EU (Ireland)
* Select 'f1.2xlarge' as the primary instance type
* Set the 'New limit value' to 1 or more
* Fill the rest of the form as appropriate and click 'Submit'

Requests are typically processed in 24 to 48 hours.
<p></details><br>

### Launching, Configuring and Connecting to an F1 Instance

The following steps explain how to launch an EC2 F1 instance starting from the FPGA Developer AMI and setting it up to connect via a remote desktop client. 

#### Launch an EC2 F1 instance with RDP connection enabled 
1. Navigate to the AWS EC2 dashboard: [https://console.aws.amazon.com/ec2](https://console.aws.amazon.com/ec2)
1. In the top right corner, select a region with F1 instances: US East (N.Virginia), US West (Oregon) or EU (Ireland) 
1. Click **Launch Instance**. This takes you to the AMI selection step.
1. Click **Community AMIs** (in the left pane)
1. Enter **FPGA Developer AMI - 1.7.0** in the search box 
1. **Select** the "FPGA Developer AMI". This brings up a pop-up screen showing pricing details. 
1. Click **Continue** to proceed to the instance type selection step.
1. Scroll down to select a **f1.2xlarge** instance
1. At the top of the console, click on **6. Configure Security Groups** 
1. Click **Add Rule**
1. Select **RDP** from the pulldown menu
1. Select **My IP** from the **Source** pulldown
1. Click **Review and Launch**. This brings up the instance launch review page.
1. Click **Launch** to launch your instance.
1. Select a valid key pair and **check** the acknowledge box at the bottom of the dialog
1. Select **Launch Instances**. This brings up the launch status page
1. When ready, select **View Instances** at the bottom of the page

#### Connect to your EC2 F1 instance
1. When the status of the newly launched instance switches to green (Running), you are ready to connect to it.
    - Allow about 10 seconds for the instance to get in the 'running' state. 
    - If needed, click the **Refresh** icon (![Refresh](../images/setup/refresh2.png?raw=true)) in the top-right corner of the EC2 Console to update the instance status information.
1. In the AWS EC2 dashboard, select your instance to display its information in the bottom pane
1. Copy or write down the **IPv4 Public IP** address of the instance.
1. Using that IP address, connect to your instance using SSH (Linux) or PuTTY (Windows)
    ```sh
    ssh -i <AWS key pairs.pem> -ssh centos@<IPv4 Public IP of EC2 instance> 22 
    ```
    ```sh
    putty -i <AWS key pairs.ppk> -ssh centos@<IPv4 Public IP of EC2 instance> 22 
    ```
1. An ASCII art message welcomes you to your instance

#### Installing a GUI Desktop

The FPGA Developer AMI doesn't include a GUI Desktop. These steps install the Gnome window manager and start RDP services to allow remote desktop connections.

1. In the remote shell, run the following command:
    ```sh
    source <(curl -s https://s3.amazonaws.com/aws-fpga-developer-ami/1.5.0/Scripts/setup_gui.sh)
    ```
1. The script will take about 10 minutes to run and finishes by setting a password for the 'centos' user. **IMPORTANT: Take note of the password generated by the script.** You will need it to connect using RDP.
1. Return to the **AWS EC2 dashboard** in your web browser
1. Select your instance, then from the **Actions** menu, select **Instance State** and then select **Reboot**
1. Wait a couple of minutes for the instance to complete the reboot cycle.

#### Connect using a remote desktop client
1. From your local machine, start a remote desktop protocol (RDP) client
    - On Windows: press the Windows key and type "mstsc.exe" in the Windows run prompt
    - On Linux: use an RDP client such a Remmina or Vinagre
    - On macOS: use the Microsoft Remote Desktop v8.0.43 (that version offers color depth settings) from the Mac App Store
1. **IMPORTANT**: Set your RDP client to use **24-bit for color depth**
    - On Windows: In the bottom-left corner of connection prompt, click Options, then select the Display tab and set Colors to True Colors (24 bit)
1. In the RDP client, enter the **IPv4 Public IP** of your instance.
1. Click **Connect**. This should bring up a message about connection certificates. 
1. Click **Yes** to dismiss the message. The Remote Desktop Connection window opens with a login prompt.
1. Login with the following credentials:
    - User: **centos**
    - Password: _password generated by the set_gui.sh script_   
1. Click **Ok**.

You are now connected via RDP to your F1 instance running Centos 7 and the FPGA Developer AMI.


---------------------------------------

<p align="center"><b>
<a href="../README.md#module-1---introduction-to-the-sdaccel-flow">Start the SDAccel Developer Labs</a>
</b></p>
