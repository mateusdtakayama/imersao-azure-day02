# Imersão Azure Expert - Day 02

## Lab 1 - Azure Storage - Blobs (15 minutes)

1. In the Azure portal, search for and select **Storage accounts** and, on the **Storage accounts** blade, select **+ Create**.

1. On the **Basics** tab of the **Create storage account** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | the name of a new resource group **RG-IAE** |
    | Storage account name | any globally unique name between 3 and 24 in length consisting of letters and digits **saiaeblob###** |
    | Location | the name of an Azure region where you can create an Azure Storage account  |
    | Performance | **Standard** |
    | Account kind | **StorageV2 (general purpose v2)** |
    | Replication | **Locally redundant storage (LRS)** |

1. Select **Next: Networking >**, on the **Networking** tab of the **Create storage account** blade, review the available options, accept the default option **Public endpoint (all networks}** and select **Next: Data protection >**.

1. On the **Data protection** tab of the **Create storage account** blade, review the available options, accept the defaults, select **Next: Advanced >**.

1. On the **Advanced** tab of the **Create storage account** blade, review the available options, accept the defaults, select **Review + Create**, wait for the validation process to complete and select **Create**.

1. On the Storage account blade, in the Blob service section, click Containers.

1. Select **Create Blob Container**, and use the empty text box to set the container name to **azureexpert**.

1. Select **azureexpert**, in the **azureexpert** pane, select **Upload**, and in the drop-down list, select **Upload Files**.

1. In the **Upload Files** window, select the ellipsis button next to the **Selected files** label, in the **Choose files to upload** window, select **files** select random files your computer, and select **Open**.

1. Back in the **Upload Files** window, select **Upload**

1. On your computer, start Browser and navigate to the download page of [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/)

1. On your computer, download and install Azure Storage Explorer with the default settings. 

1. Navigate to the [Azure portal](https://portal.azure.com), and sign-in by providing credentials of the user account with the Owner role in the subscription you are using in this lab.

1. Navigate to the blade of the newly created storage account, select **Access keys** and review the settings of the target blade.

1. On the storage account blade, select **Shared access signature** and review the settings of the target blade.

1. On the resulting blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Allowed services | **Blob** |
    | Allowed resource types | **Service**, **Container** and **Object** |
    | Allowed permissions | **Read**, **List** |
    | Blob versioning permissions | disabled |
    | Start | 24 hours before the current time in your current time zone | 
    | End | 24 hours after the current time in your current time zone |
    | Allowed protocols | **HTTPS only** |
    | Signing key | **key1** |

1. Select **Generate SAS and connection string**.

1. Copy the value of **Blob service SAS URL** into Clipboard.

1. On your computer, start Azure Storage Explorer. 

1. In the Azure Storage Explorer window, in the **Connect to Azure Storage** window, select **Use a shared access signature (SAS) URI** and select **Next**.

1. In the **Attach with SAS URI** window, in the **Display name** text box, type **saIAEblob###**, in the **URI** text box, paste the value you copied into Clipboard, and select **Next**. 

    >**Note**: This should automatically populate the value of **Blob endpoint** text box.

1. In the **Connection Summary** window, select **Connect**. 

1. Select **Storage account** and "Blob containers", Open and download uploaded files

1. Leave the Azure Storage Explorer window open.

## Lab 2 - Azure Storage - Files (15 minutes)

1. In the Azure portal, search for and select **Storage accounts** and, on the **Storage accounts** blade and create a new Storage account **saiaefiles###**, in the **File service** section, click **File shares**.

1. Click **+ File share** and create a file share with the following settings:

    | Setting | Value |
    | --- | --- |
    | Name | **azureexpert** |
    | Quota | **1024** |
    | Tiers | hot |

1. Click the newly created file share and click **Connect**.

1. On the **Connect** blade, ensure that the **Windows** tab is selected, and click **Copy to clipboard**.

1. On your computer, start Windows PowerShell and, in the **Administrator: Windows PowerShell** window run the following to set map share. 

1. Verify that the script completed successfully. 

1. Connect share and upload files.

## Lab 3 - Azure App Service with Staging and Autoscale (30 minutes)

### Task 1 - Create an Azure Web App

In this task, you will create an Azure web app.

1. Sign in to the [**Azure portal**](http://portal.azure.com).

1. In the Azure portal, search for and select **App services**, and, on the **App Services** blade, click **+ Create**.

1. On the **Basics** tab of the **Create Web App** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- | ---|
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | **rg-iae** |
    | Web app name | any globally unique name |
    | Publish | **Code** |
    | Runtime stack | **PHP 8.2** |
    | Operating system | **Linux** |
    | Region | the name of an Azure region where you can provision Azure web apps |
    | App service plan | accept the default configuration |

1. Click **Review + create**. On the **Review + create** tab of the **Create Web App** blade, ensure that the validation passed and click **Create**.

    >**Note**: Wait until the web app is created before you proceed to the next task. This should take about a minute.

1. On the deployment blade, click **Go to resource**.

### Task 2: Create a staging deployment slot

In this task, you will create a staging deployment slot.

1. On the blade of the newly deployed web app, click the **URL** link to display the default web page in a new browser tab.

1. Close the new browser tab and, back in the Azure portal, in the **Deployment** section of the web app blade, click **Deployment slots**.

    >**Note**: The web app, at this point, has a single deployment slot labeled **PRODUCTION**.

1. Click **+ Add slot**, and add a new slot with the following settings:

    | Setting | Value |
    | --- | ---|
    | Name | **staging** |
    | Clone settings from | **Do not clone settings**|

1. Back on the **Deployment slots** blade of the web app, click the entry representing the newly created staging slot.

    >**Note**: This will open the blade displaying the properties of the staging slot.

1. Review the staging slot blade and note that its URL differs from the one assigned to the production slot.

### Task 3: Configure web app deployment settings

In this task, you will configure web app deployment settings.

1. On the staging deployment slot blade, in the **Deployment** section, click **Deployment Center** and then select the **Settings** tab.

    >**Note:** Make sure you are on the staging slot blade (rather than the production slot).
    
1. On the **Settings** tab, in the **Source** drop-down list, select **Local Git** and click the **Save** button

1. On the **Deployment Center** blade, copy the **Git Clone Url** entry to Notepad.

    >**Note:** You will need the Git Clone Url value in the next task of this lab.

1. On the **Deployment Center** blade, select the **Local Git/FTPS credentials** tab, in the **User Scope** section, specify the following settings, and click **Save**.

    | Setting | Value |
    | --- | ---|
    | User name | any globally unique name (must not contain `@` character) |
    | Password | any password that satisfies complexity requirements|

    >**Note:** You will need these credentials in the next task of this lab.

### Task 4: Deploy code to the staging deployment slot

In this task, you will deploy code to the staging deployment slot.

1. In the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

1. If prompted to select either **Bash** or **PowerShell**, select **PowerShell**.

    >**Note**: If this is the first time you are starting **Cloud Shell** and you are presented with the **You have no storage mounted** message, select the subscription you are using in this lab, and click **Create storage**.

1. From the Cloud Shell pane, run the following to clone the remote repository containing the code for the web app.

   ```powershell
   git clone https://github.com/maiaacademy/php-docs-hello-world
   ```

1. From the Cloud Shell pane, run the following to set the current location to the newly created clone of the local repository containing the sample web app code.

   ```powershell
   Set-Location -Path $HOME/php-docs-hello-world/
   ```

1. From the Cloud Shell pane, run the following to add the remote git (make sure to replace the `[deployment_user_name]` and `[git_clone_url]` placeholders with the value of the **Deployment Credentials** user name and **Git Clone Url**, respectively, which you identified in previous task):

   ```powershell
   git remote add [deployment_user_name] [git_clone_url]
   ```

    >**Note**: The value following `git remote add` does not have to match the **Deployment Credentials** user name, but has to be unique

1. From the Cloud Shell pane, run the following to push the sample web app code from the local repository to the Azure web app staging deployment slot (make sure to replace the `[deployment_user_name]` placeholder with the value of the **Deployment Credentials** user name, which you identified in previous task):

   ```powershell
   git push [deployment_user_name] master
   ```

1. If prompted to authenticate, type the `[deployment_user_name]` and the corresponding password (which you set in the previous task).

1. Close the Cloud Shell pane.

1. On the staging slot blade, click **Overview** and then click the **URL** link to display the default web page in a new browser tab.

1. Verify that the browser page displays the **Hello World!** message and close the new tab.

### Task 5: Swap the Staging slots

In this task, you will swap the staging slot with the production slot

1. Navigate back to the blade displaying the production slot of the web app.

1. In the **Deployment** section, click **Deployment slots** and then, click **Swap** toolbar icon.

1. On the **Swap** blade, review the default settings and click **Swap**.

1. Click **Overview** on the production slot blade of the web app and then click the **URL** link to display the web site home page in a new browser tab.

1. Verify the default web page has been replaced with the **Hello World!** page.

### Task 6: Configure and test autoscaling of the Azure web app

In this task, you will configure and test autoscaling of Azure web app.

1. On the blade displaying the production slot of the web app, in the **Settings** section, click **Scale out (App Service plan)**.

1. Click **Custom autoscale**.

    >**Note**: You also have the option of scaling the web app manually.

1. Select **Scale based on a metric** and click **+ Add a rule**

1. On the **Scale rule** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- |--- |
    | Metric source | **Current resource** |
    | Metric namespace | **standard metrics** |
    | Metric name | **CPU Percentage** |
    | Operator | **Greater than** |
    | Metric threshold to trigger scale action | **2** |
    | Duration (in minutes) | **5** |
    | Time grain statistic | **Maximum** |
    | Time aggregation | **Maximum** |
    | Operation | **Increase count by** |
    | Instance count | **1** |
    | Cool down (minutes) | **5** |

1. Back on the Scaling blade, **Scale based on a metric** and click **+ Add a rule**

1. On the **Scale rule** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- |--- |
    | Metric source | **Current resource** |
    | Metric namespace | **standard metrics** |
    | Metric name | **CPU Percentage** |
    | Operator | **Less than** |
    | Metric threshold to trigger scale action | **1** |
    | Duration (in minutes) | **10** |
    | Time grain statistic | **Maximum** |
    | Time aggregation | **Maximum** |
    | Operation | **Decrease count by** |
    | Instance count | **1** |
    | Cool down (minutes) | **5** |

    >**Note**: These values do not represent a realistic configuration, since their purpose is to trigger autoscaling as soon as possible, without extended wait period.

1. Click **Add** and, back on the App Service plan scaling blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- |--- |
    | Instance limits Minimum | **1** |
    | Instance limits Maximum | **2** |
    | Instance limits Default | **1** |

1. Click **Save**.

    >**Note**: If you got an error complaining about 'microsoft.insights' resource provider not being registered, run `az provider register --namespace 'Microsoft.Insights'` in your cloudshell and retry saving your auto scale rules.

1. In the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

1. If prompted to select either **Bash** or **PowerShell**, select **PowerShell**.

1. From the Cloud Shell pane, run the following to identify the URL of the Azure web app.

   ```powershell
   $rgName = 'rg-iae'

   $webapp = Get-AzWebApp -ResourceGroupName $rgName
   ```

1. From the Cloud Shell pane, run the following to start and infinite loop that sends the HTTP requests to the web app:

   ```powershell
   while ($true) { Invoke-WebRequest -Uri $webapp.DefaultHostName }
   ```

1. Minimize the Cloud Shell pane (but do not close it) and, on the web app blade, in the Settings section, click **Scale out (App Service plan)**.

1. Select the **Run history** tab, and check the **Observed resource instance count**.

1. Monitor the utilization and the number of instances for a few minutes. 

    >**Note**: You may need to **Refresh** the page.

1. Once you notice that the number of instances has increased to 2, reopen the Cloud Shell pane and terminate the script by pressing **Ctrl+C**.

1. Close the Cloud Shell pane.

## Lab 4 - Deploy Azure Kubernetes Service (30 minutes)

Kubernetes architecture.

   ![Screenshot of the Kubernetes archicture](/AllFiles/Images/IMG03.png)

#### Register the Microsoft Kubernetes resource providers.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

1. If prompted to select either **Bash** or **PowerShell**, select **PowerShell**. 

    >**Note**: If this is the first time you are starting **Cloud Shell** and you are presented with the **You have no storage mounted** message, select the subscription you are using in this lab, and click **Create storage**. 

1. From the Cloud Shell pane, run the following to register the Microsoft.Kubernetes and Microsoft.KubernetesConfiguration resource providers.

   ```pwsh
   Register-AzResourceProvider -ProviderNamespace Microsoft.Kubernetes
   
   Register-AzResourceProvider -ProviderNamespace Microsoft.KubernetesConfiguration
   ```

1. Close the Cloud Shell pane.

#### Deploy an Azure Kubernetes Service cluster

1. In the Azure portal, search for locate **Kubernetes services** and then, on the **Kubernetes services** blade, click **+ Add**, and then click **+ Add Kubernetes cluster**. 

1. On the **Basics** tab of the **Create Kubernetes cluster** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | ---- | ---- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | **RG-IAE** |
    | Kubernetes cluster name | **aksiaecl** |
    | Region | the name of a region where you can provision a Kubernetes cluster |
    | Kubernetes version | accept the default |
    | Node size | accept the default |
    | Node count | **1** |

1. Click **Next: Node Pools >** and, on the **Node Pools** tab of the **Create Kubernetes cluster** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | ---- | ---- |
    | Virtual nodes | **Disabled** |
    | VM scale sets | **Enabled** |
	
1. Click **Next: Authentication >** and, on the **Authentication** tab of the **Create Kubernetes cluster** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | ---- | ---- |
    | Service principal | accept the default |
    | Enable RBAC | **Yes** |

1. Click **Next: Networking >** and, on the **Networking** tab of the **Create Kubernetes cluster** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | ---- | ---- |
    | Network configuration | **kubenet** |
    | DNS name prefix | any valid, globally unique DNS host name |

1. Click **Next: Integration >**, on the **Integration** tab of the **Create Kubernetes cluster** blade, set **Container monitoring** to **Disabled**, click **Review + create** and then click **Create**. 

    >**Note**: In production scenarios, you would want to enable monitoring. Monitoring is disabled in this case since it is not covered in the lab. 

    >**Note**: Wait for the deployment to complete. This should take about 10 minutes.

#### Deploy pods into the Azure Kubernetes Service cluster

1. On the deployment blade, click the **Go to resource** link.

1. On the **aksiaecl** Kubernetes service blade, in the **Settings** section, click **Node pools**.

1. On the **aksIAEcl - Node pools** blade, verify that the cluster consists of a single pool with one node.

1. In the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

1. Switch the **Azure Cloud Shell** to **Bash** (black background).

1. From the Cloud Shell pane, run the following to retrieve the credentials to access the AKS cluster:

    ```sh
    az aks get-credentials --resource-group rg-iae --name aksiaecl
    ``` 

1. From the **Cloud Shell** pane, run the following to verify connectivity to the AKS cluster:

    ```sh
    kubectl get nodes
    ```

1. In the **Cloud Shell** pane, review the output and verify that the one node which the cluster consists of at this point is reporting the **Ready** status. 

1. From the **Cloud Shell** pane, run the following to deploy the **nginx** image from the Docker Hub:

    ```sh
    kubectl create deployment nginx-deployment --image=nginx
    ```

    > **Note**: Make sure to use lower case letters when typing the name of the deployment (nginx-deployment)

1. From the **Cloud Shell** pane, run the following to verify that a Kubernetes pod has been created:

    ```sh
    kubectl get pods
    ```

1. From the **Cloud Shell** pane, run the following to identify the state of the deployment:

    ```sh
    kubectl get deployment
    ```

1. From the **Cloud Shell** pane, run the following to make the pod available from Internet:

    ```sh
    kubectl expose deployment nginx-deployment --port=80 --type=LoadBalancer
    ```

1. From the **Cloud Shell** pane, run the following to identify whether a public IP address has been provisioned:

    ```sh
    kubectl get service
    ```

1. Re-run the command until the value in the **EXTERNAL-IP** column for the **nginx-deployment** entry changes from **\<pending\>** to a public IP address. Note the public IP address in the **EXTERNAL-IP** column for **nginx-deployment**.

1. Open a browser window and navigate to the IP address you obtained in the previous step. Verify that the browser page displays the **Welcome to nginx!** message.

#### Scale Containerized workloads in the Azure Kubernetes service cluster

1. From the **Cloud Shell** pane, run the following to scale the deployment by increasing of the number of pods to 2:

    ```sh
    kubectl scale --replicas=2 deployment/nginx-deployment
    ```

1. From the **Cloud Shell** pane, run the following to verify the outcome of scaling the deployment:

    ```sh
    kubectl get pods
    ```

    > **Note**: Review the output of the command and verify that the number of pods increased to 2.

1. OPTIONAL: From the **Cloud Shell** pane, run the following to scale out the cluster by increasing the number of nodes to 2:

    ```sh
    az aks scale --resource-group rg-iae-aks --name aksiaecl --node-count 2
    ```

    > **Note**: Wait for the provisioning of the additional node to complete. This might take about 3 minutes. If it fails, rerun the `az aks scale` command.

1. From the **Cloud Shell** pane, run the following to verify the outcome of scaling the cluster:

    ```sh
    kubectl get nodes
    ```

    > **Note**: Review the output of the command and verify that the number of nodes increased to 2.

1. From the **Cloud Shell** pane, run the following to scale the deployment:

    ```
    kubectl scale --replicas=10 deployment/nginx-deployment
    ```

1. From the **Cloud Shell** pane, run the following to verify the outcome of scaling the deployment:

    ```
    kubectl get pods
    ```

    > **Note**: Review the output of the command and verify that the number of pods increased to 10.

1. From the **Cloud Shell** pane, run the following to review the pods distribution across cluster nodes:

    ```
    kubectl get pod -o=custom-columns=NODE:.spec.nodeName,POD:.metadata.name
    ```

    > **Note**: Review the output of the command and verify that the pods are distributed across both nodes.

1. From the **Cloud Shell** pane, run the following to delete the deployment:

    ```
    kubectl delete deployment nginx-deployment
    ```
1. Close the **Cloud Shell** pane.

## Lab 6 - Create and configure Microsoft Entra ID users (15 minutes)

In this task, you will create and configure Entra ID users.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. In the Azure portal, search for and select **Microsoft Entra ID**.

1. On the Microsoft Entra ID blade, scroll down to the **Manage** section, click **User settings**, and review available configuration options.

1. On the Microsoft Entra ID blade, in the **Manage** section, click **Users**, and then click your user account to display its **Profile** settings. 

1. Click **Edit properties**, and then in the **Settings** tab, set **Usage location** to **United States** and click **Save** to apply the change.

1. Navigate back to the **Users - All users** blade, and then click **+ New user**.

1. Create a new user with the following settings (leave others with their defaults):

    | Setting | Value |
    | --- | --- |
    | User name | **azureexpert-user1** |
    | Name | **azureexpert-user1** |
    | Let me create the password | enabled |
    | Initial password | **Provide a secure password** |
    | Usage location | **Brazil** |
    | Job title | **Cloud Architect** |
    | Department | **IT** |

    >**Note**: **Copy to clipboard** the full **User Principal Name** (user name plus domain). You will need it later in this task.

1. In the list of users, click the newly created user account to display its blade.

1. Review the options available in the **Manage** section and note that you can identify the Entra ID roles assigned to the user account as well as the user account's permissions to Azure resources.

1. In the **Manage** section, click **Assigned roles**, then click **+ Add assignment** button and assign the **User administrator** role to **azureexpert-user1**.

    >**Note**: You also have the option of assigning Entra ID roles when provisioning a new user.

1. Open an **InPrivate** browser window and sign in to the [Azure portal](https://portal.azure.com) using the newly created user account. When prompted to update the password, change the password to a secure password of your choosing. 

    >**Note**: Rather than typing the user name (including the domain name), you can paste the content of Clipboard.

1. In the **InPrivate** browser window, in the Azure portal, search for and select **Microsoft Entra ID**.

    >**Note**: While this user account can access the Microsoft Entra tenant, it does not have any access to Azure resources. This is expected, since such access would need to be granted explicitly by using Azure Role-Based Access Control. 

1. In the **InPrivate** browser window, on the Entra ID blade, scroll down to the **Manage** section, click **User settings**, and note that you do not have permissions to modify any configuration options.

1. In the **InPrivate** browser window, on the Entra ID blade, in the **Manage** section, click **Users**, and then click **+ New user**.

1. Create a new user with the following settings (leave others with their defaults):

    | Setting | Value |
    | --- | --- |
    | User name | **azureexpert-user2** |
    | Name | **azureexpert-user2** |
    | Let me create the password | enabled |
    | Initial password | **Provide a secure password** |
    | Usage location | **Brazil** |
    | Job title | **Azure Expert** |
    | Department | **IT** |

1. Sign out as the **azureexpert-user1** user from the Azure portal and close the InPrivate browser window.

## Lab 7 - Assign Azure RBAC roles

In this task, you will create an Microsoft Entra ID user, assign the RBAC role you created in the previous task to that user, and verify that the user can perform the task specified in the RBAC role definition.

1. In the Azure portal, search for and select **Microsoft Entra ID**, on the Microsoft Entra ID blade, click **Users**, and then click **+ New user**.

1. Create a new user with the following settings (leave others with their defaults):

    | Setting | Value |
    | --- | --- |
    | User name | **azureexpert-user3**|
    | Name | **azureexpert-user3**|
    | Let me create the password | enabled |
    | Initial password | **Provide a secure password** |

    >**Note**: **Copy to clipboard** the full **User name**. You will need it later in this lab.

1. In the Azure portal, navigate back to the Subscription and display its **details**.

1. Click **Access Control (IAM)**, click **+ Add** and then **Add role assignment**. On the **Role** tab, search for **Support Request Contributor (Custom)**. 

    >**Note**: if your custom role is not visible, it can take up to 10 minutes for the custom role to appear after creation.

1. Select the **Role** and click **Next**. On the **Members** tab, click **+ Select members** and **select** user account **azureexpert-user3-***********************.**********.onmicrosoft.com. Click **Next** and then **Review and assign**.

1. Open an **InPrivate** browser window and sign in to the [Azure portal](https://portal.azure.com) using the newly created user account. When prompted to update the password, change the password for the user.

    >**Note**: Rather than typing the user name, you can paste the content of Clipboard.

1. In the **InPrivate** browser window, in the Azure portal, search and select **Resource groups** to verify that the **azureexpert-user1** user can see all resource groups.

1. In the **InPrivate** browser window, in the Azure portal, search and select **All resources** to verify that the **azureexpert-user1** user cannot see any resources.

1. In the **InPrivate** browser window, in the Azure portal, search and select **Help + support** and then click **+ Create a support request**. 

1. In the **InPrivate** browser window, on the **Problem Description/Summary** tab of the **Help + support - New support request** blade, type **Service and subscription limits** in the Summary field and select the **Service and subscription limits (quotas)** issue type. Note that the subscription you are using in this lab is listed in the **Subscription** drop-down list.

    >**Note**: The presence of the subscription you are using in this lab in the **Subscription** drop-down list indicates that the account you are using has the permissions required to create the subscription-specific support request.

    >**Note**: If you do not see the **Service and subscription limits (quotas)** option, sign out from the Azure portal and sign in back.

1. Do not continue with creating the support request. Instead, sign out as the **workshop-az014-user1 user from the Azure portal and close the InPrivate browser window.

## Lab 8 - Azure Backup (20 minutes)

1. In the Azure portal, search for and select **Recovery Services vaults** and, on the **Recovery Services vaults** blade, click **+ Create**.

1. On the **Create Recovery Services vault** blade, specify the following settings:

    | Settings | Value |
    | --- | --- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | the name of a new resource group **RG-IAE** |
    | Name | **RSV-IAE-Backup** |
    | Region | the name of a region where you deployed the two virtual machines in the previous task |

    >**Note**: Make sure that you specify the same region into which you deployed virtual machines.

1. Click **Review + Create** and then click **Create**.

    >**Note**: Wait for the deployment to complete. The deployment should take less than 1 minute.

1. Create a new Windows Server VM.

1. When the deployment is completed, click **Go to Resource**. 

1. On the **RSV-IAE-Backup** Recovery Services vault blade, in the **Settings** section, click **Properties**.

1. On the **RSV-IAE-Backup - Properties** blade, click the **Update** link under **Backup Configuration** label.

1. On the **Backup Configuration** blade, note that you can set the **Storage replication type** to either **Locally-redundant** or **Geo-redundant**. Leave the default setting of **Geo-redundant** in place and close the blade.

    >**Note**: This setting can be configured only if there are no existing backup items.

1. Back on the **RSV-IAE-Backup - Properties** blade, click the **Update** link under **Security Settings** label. 

1. On the **Security Settings** blade, note that **Soft Delete (For Azure Virtual Machines)** is **Enabled** change to the **Disabled**.

1. Close the **Security Settings** blade and, back on the **RSV-IAE-Backup** Recovery Services vault blade, click **Overview**.

1. On the **RSV-IAE** Recovery Services vault blade, click **+ Backup**.

1. On the **Backup Goal** blade, specify the folowing settings:

    | Settings | Value |
    | --- | --- |
    | Where is your workload running? | **Azure** |
    | What do you want to backup? | **Virtual machine** |

1. On the **Backup Goal** blade, click **Backup**.

1. On the **Backup policy**, review the **DefaultPolicy** settings and select **Create a new policy**.

1. Define a new backup policy with the following settings (leave others with their default values):

    | Setting | Value |
    | ---- | ---- |
    | Policy name | **BP-VMS** |
    | Frequency | **Daily** |
    | Time | **22:00 PM** |
    | Timezone | the name of your local time zone |
    | Retain instant recovery snapshot(s) for | **2** Days(s) |

1. Click **OK** to create the policy and then, in the **Virtual Machines** section, select **Add**.

1. On the **Select virtual machines** blade, select your VM, click **OK**, and, back on the **Backup** blade, click **Enable backup**.

    >**Note**: Wait for the backup to be enabled. This should take about 2 minutes. 

1. Navigate back to the **RSV-IAE-Backup** Recovery Services vault blade, in the **Protected items** section, click **Backup items**, and then click the **Azure virtual machines** entry.

1. On the **Backup Items (Azure Virtual Machine)** blade of your VM, review the values of the **Backup Pre-Check** and **Last Backup Status** entries, and click the **your VM** entry.

1. On the **your VM** Backup Item blade, click **Backup now**, accept the default value in the **Retain Backup Till** drop-down list, and click **OK**.

 >**Note**: Do not wait for the backup to complete but instead proceed.

## After the Hands-on lab 

1. Delete all Azure resources created in support of this Hands-on lab.

1. End of Day 2 and **Imersao Azure Azure Expert**.

