---
lab:
    title: 'Lab: Managing Windows Server'
    type: 'Answer Key'
    module: 'Module 3: Windows Server administration'
---

# Lab answer key: Managing Windows Server

## Exercise 1: Implementing and using remote server administration

#### Task 1: Install Windows Admin Center

1. Connect to **SEA-ADM1**, and if needed, sign in with the credentials provided by the instructor.
1. On **SEA-ADM1**, select **Start**, and then select **Windows PowerShell (Admin)**.
1. In the **Windows PowerShell** console, enter the following command, and then press Enter to download the latest version of Windows Admin Center:
	
   ```powershell
	$parameters = @{
	     Source = "https://aka.ms/WACdownload"
	     Destination = ".\WindowsAdminCenter.exe"
	}
	Start-BitsTransfer @parameters
   ```
1. Enter the following command, and then press Enter to install Windows Admin Center:
	
   ```powershell
   Start-Process -FilePath '.\WindowsAdminCenter.exe' -ArgumentList '/VERYSILENT' -Wait
   ```

   > **Note**: Wait until the installation completes. This should take about 2 minutes.
   
   > **Note**: After installation completes, you may encounter the error message 'ERR_Connection_Refused'. If this occurs, restart SEA-ADM1 to correct the issue.

#### Task 2: Add servers for remote administration

1. On **SEA-ADM1**, start Microsoft Edge, and then go to `https://SEA-ADM1.contoso.com`.

   >**Note**: If the link does not work, on **SEA-ADM1**, open File Explorer, select Downloads folder, in the Downloads folder select **WindowsAdminCenter.msi** file and install manually. After the install completes, refresh Microsoft Edge.

   >**Note**: If you get **NET::ERR_CERT_DATE_INVALID** error, select **Advanced** on the Edge browser page, at the bottom of page select **Continue to sea-adm1-contoso.com (unsafe)**.

1. When prompted, in the **Windows Security** dialog box, enter the credentials provided by the instructor.
1. Review all tabs on the **Configure your Windows Admin Center Settings and environment** pop-up window, including the **Extensions** tab and select **Complete** to close the window.
1. Review the **New in this release** pop-up window and select **Close** in its upper-right corner.
1. Review the **All connections** page and note that it includes the **sea-adm1.contoso.com** entry. 
1. On the **All connections** page, select **+ Add**. 
1. In the Add or create resources pane, on the **Servers** tile, select **Add**.
1. In the **Server name** text box, enter **sea-dc1.contoso.com**.

#### Task 3: Configure Windows Admin Center extensions

1. On **SEA-ADM1**, in the upper-right corner of the Microsoft Edge window displaying Windows Admin Center, select the **Settings** icon (the cog wheel).
1. In the left pane, select **Extensions**. Review the available extensions.
1. Select the **DNS** extension, and then select **Install**. The extension will install and Windows Admin Center will refresh.
1. In the details pane, select **Installed extensions** and verify that the list includes the extension you just installed.
1. On the top menu, next to **Settings**, select the drop-down arrow, and then select **Server Manager**.
1. On the **Server connections** page, select the **sea-dc1.contoso.com** link.

1. To install the DNS PowerShell tools, in the left pane, in the list of **Tools**, select **DNS**, and then select **Install**. The tools will take less than a minute to install.
1. Select the **Contoso.com** zone and review the list of its DNS records.

#### Task 4: Verify remote administration

1. On **SEA-ADM1**, in Windows Admin Center, in the left pane, in the list of **Tools**, select **Overview**. Note that the details pane of Windows Admin Center displays basic server information and performance monitoring.
1. In the left pane, in the list of **Tools**, scroll down and review the basic administration tools available. Select **Roles & features** and note which roles and features are listed as installed and which ones are available to install. Scroll down, select the **Telnet Client** checkbox, and then select **+ Install** at the top of the pane.
1. In the **Install Roles and Features** pane, select **Yes** and wait for the message confirming that Telnet Client was installed successfully.
1. At the very top of the left pane, below the list of **Tools**, select **Settings**.
1. In the **Settings** section on the right side, select **Remote Desktop**.
1. In the **Remote Desktop** section, select the option **Allow remote connections to this computer** checkbox, and then select **Save**.
1. In the left pane, in the list of **Tools**, select **Remote Desktop**.
1. In the Remote Desktop pane, enter the password given by the instructor, then select the **Automatically connect with the certificate presented by this machine** checkbox, and then select **Connect**.
1. When prompted, select **Confirm**, and then select **Connect**.
1. Verify that you successfully connected via Remote Desktop to **SEA-DC1** within the Windows Admin Center interface.
1. Select **Disconnect**.
1. Close the Microsoft Edge window.

#### Task 5: Administer servers with Remote PowerShell

1. On **SEA-ADM1**, switch to the **PowerShell** console session. 
1. In the **Windows PowerShell** console, enter the following command, and then press Enter to start a PowerShell Remoting session to **SEA-DC1**:

   ```powershell
   Enter-PSSession -ComputerName SEA-DC1
   ```
1. From the **[SEA-DC1]** prompt, enter the following command and press Enter to display the status of the Application Identity service (AppIDSvc):

   ```powershell
   Get-Service -Name AppIDSvc
   ```

   > **Note**: Verify that the service is currently stopped.

1. From the **[SEA-DC1]** prompt, enter the following command and press Enter to start the Application Identity service:

   ```powershell
   Start-Service -Name AppIDSvc
   ```
1. From the **[SEA-DC1]** prompt, enter the following command and press Enter to display the status of the Application Identity service (AppIDSvc):

   ```powershell
   Get-Service -Name AppIDSvc
   ```

   > **Note**: Verify that the service is currently running.

### Results

After completing this exercise, you will have installed Windows Admin Center and connected it to the servers in your lab environment. You performed a number of remote management tasks including installing a feature as well as enabling and testing Remote Desktop connectivity. Finally, you used PowerShell Remoting to check the status of a service and then to start it.
