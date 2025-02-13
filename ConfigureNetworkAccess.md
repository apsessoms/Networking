# Configure Network Access

In this lab, we will configure the access to a virtual machine (VM) thats hosting a web server and explain the reasons for configuring network access. 

## Steps

## 1. **Open the Azure portal**: Navigate to the [Azure portal](https://portal.azure.com/) and log in with your credentials.

Open Azure CLI in the Azure portal by clicking on the Cloud Shell icon in the top right corner of the Azure portal.
    + Run the following command to get your VM's IP address:
    ```
    az vm list-ip-addresses
    ```
    + Run ```curl --connect-timeout 5 http://20.9.132.224``` to test the connectivity to the VM. You will see an error message stating that the connection timed out. 
    + Try to copy and paste the IP address into a browser window to access your web server. You will see that the connection is refused or that it can't reach the page. 

## 2. List current NSG Rules
**What we know**: The server is not accessible. But why? 
    + Run the following command to list the current NSG rules associated with the VM:
    ```
    az network nsg list --resource-group "homelab-webservervm-rg" --query '[].name' --output tsv
    ```
    If you see something like "my-vmNSG" or "homelabwebservervm1-NSG" then Azure has created a default NSG for your VM.
    + Run ```az network nsg rule list``` to list the rules associated with the NSG.

This creates a large list of rules in JSON format but we can make it easier to read. My output looks like this:
```
PS /home/ann> az network nsg rule list --resource-group "homelab-webservervm-rg" --nsg-name homelabwebservervm1-nsg --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' --output table
Name    Priority    Port    Access
------  ----------  ------  --------
RDP     300         3389    Allow
SSH     320         22      Allow
PS /home/ann>
```

The default rule <em>default-allow-ssh & default-allow-rdp</em> were chosen by me when I created the VM initially. SSH over port 22 is a protocol used on Linux to allow admins to remote access into them. Priority of this rule is 1000 and they are processed in order of priority (lower numbers are processed first).

## 3. Create NSG Rule

Let's create a network security rule that allows inbound access on Port 80 (http).

Run the following command to create this rulled known as <em>allow-http</em>:
```
az network nsg rule create --resource-group "homelab-webservervm-rg" --nsg-name homelabwebservervm1-nsg --name allow-http --protocol tcp --priority 100 --destination-port-range 80 --access Allow
```

You will see the status change from "starting" to "running" and the finally to "succeeded". Notice we set the priority to 100. After running that command, your output should look like this:
```
{
  "access": "Allow",
  "destinationAddressPrefix": "*",
  "destinationAddressPrefixes": [],
  "destinationPortRange": "80",
  "destinationPortRanges": [],
  "direction": "Inbound",
  "etag": "W/\"ed4aee6a-a609-44d4-965b-7bdcdac9cc25\"",
  "id": "/subscriptions/98b0e576-e7ad-4cb3-8290-6a6265da4f18/resourceGroups/homelab-webservervm-rg/providers/Microsoft.Network/networkSecurityGroups/homelabwebservervm1-nsg/securityRules/allow-http",
  "name": "allow-http",
  "priority": 100,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "homelab-webservervm-rg",
  "sourceAddressPrefix": "*",
  "sourceAddressPrefixes": [],
  "sourcePortRange": "*",
  "sourcePortRanges": [],
  "type": "Microsoft.Network/networkSecurityGroups/securityRules"
}
```

To verify configuration, run the ```az network nsg rule list``` command again. You should see the new rule listed. 

```
Name        Priority    Port    Access
----------  ----------  ------  --------
RDP         300         3389    Allow
SSH         320         22      Allow
allow-http  100         80      Allow
```

You should know see the <em>allow-http</em> rule listed with a priority of 100 over port 20. 

4. Access web server
Now that we opened that port 80, you should be able to access the web server.  Run the following command to test the connectivity:
```
 curl --connect-timeout 5 http://20.9.132.224 
 ```

You should see this output:
```html
<html><body><h2>Welcome to Azure! My name is homelabwebservervm1 (the name of your VM).</h2></body></html>
```

You can also try visiting the IP address in a browser window. 

## Delete Resources

Delete your resources if you are done testing or shut them off in order to save money. 
