# Install GPMC - Group Policy Management Console

Download the latest version from Releases:       
https://github.com/poldeploy/GPMC/releases/tag/1.0.2

## System requirements

* Requires .NET Framework version 4.6 or higher
* Minimum supported operating systems: Windows Vista or Windows Server 2008

## Install instructions

1. Proceed with one of the following options:

   * To launch the installation right away, click Open or Run this program from its current location.
   * To save the setup file for later use, click Save or Save this program to disk.
2. To install the GPMC, execute the `.bat` file. After you agree to the End User License Agreement (EULA), all required files will be installed in the “%Program Files%\GPMC” directory.
3. Before running or using the GPMC, make sure to review the release notes file `RelNotes.rtf` located in the “%Program Files%\GPMC” folder.
4. Once the GPMC installation is complete, you can open the snap-in using one of the following methods:

   * Launch the pre-configured `GPMC.msc` file by clicking **Start**, selecting **Run**, typing **GPMC.msc**, and then pressing **OK**. Alternatively, open **Group Policy Management** from the **Administrative Tools** section in the Control Panel.
   * You can also create a custom MMC console that includes the GPMC snap-in. To do so:

     * Open MMC by clicking **Start**, choosing **Run**, typing **MMC**, and pressing **OK**.
     * From the **File** menu, select **Add/Remove Snap-in**, and then click **Add**.
     * In the **Add Standalone Snap-in** dialog box, select **Group Policy Management** and click **Add**.
     * Click **Close**, then **OK** to confirm.
5. GPMC comes with several sample scripts stored in the `%ProgramFiles%\GPMC\Scripts` directory. Use `cscript.exe` to run these sample scripts. For additional details, refer to the `ScriptingReadMe.rtf` file in the scripts folder. To view instructions and usage information for any script, execute it with the “/? ” parameter.
 
