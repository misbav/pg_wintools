# pg_wintools #

PostgreSQL Windows extension that allows easier integration of PostgreSQL in the windows ecosystem.

It implements some methods that are usually found in a SQL Server environment.

- [pg_read_registry](#pg_read_registry)
- [pg_write_event_log_entry](#pg_write_event_log_entry)
- [pg_fixed_drives_list](#pg_fixed_drives_list)
- [pg_hostname](#pg_hostname)
- [pg_file_exists](#pg_file_exists)

______________________________________________________
<a name="pg_read_registry"></a>
pg_read_registry
================
Reads the value of a registry key.

Expected params :

- root key text ('HKLM' or 'HKCR' or 'HKCU')
- key name text
- key value text

 Returns : 

- text with the value. 
 *If the value is binary, the output is made of hexa values in the form 'xx xx xx ' with 
 a maximum length of 1024. (+- 340 bytes)*

 Example :
 ```select pg_Read_Registry('HKLM','SOFTWARE\Microsoft\Windows\CurrentVersion\Installer','InstallerLocation');```

**This function can only be executed by a superuser.**

----
<a name="pg_write_event_log_entry"></a>
pg_write_event_log_entry
========================
Function to write an entry into the eventlog that will be under the "Postgresql" source.

Expected params :

- message text. *Maximum size of 32k.*
- eventtype int (1=error, 2=warning, 4=information)

Returns : 

- ```null```

 Example : ```select pg_write_event_log_entry('Test from psql',4);```



----
<a name="pg_fixed_drives_list"></a>
pg_fixed_drives_list
========================
Function that returns fixed disks information (Name, total size and free space).

Expected params :
 
- none

Returns : 

- SETOF RECORD with the form (drive text, total_size, free_space). 
*One record for each fixed disk.*
 
Example :
```select * from pg_fixed_drives_list() lst (drive text,total_size int, free_space int)```

**This function can only be executed by a superuser.**

----
<a name="pg_hostname"></a>
pg_hostname
==============
Gets the hostname of the server running the postgresql cluster

Expected params : 

- none

Returns : 

- text containing the hostname

Example :
	```select pg_hostname();```

----

<a name="pg_file_exists"></a>
pg_file_exists
==============
Checks that a file/folder exists on the machine.
Expected params :

 - filename text. 

Returns : 

- ```true``` if file exists **AND** access is granted by OS, ```false``` otherwise.

 Example : 
 ```select pg_file_exists('c:\windows\explorer.exe');```

*Works with filename given as unc like \\server\share\filename*

________________________________________________

Build
-----
The build requires Visual Studio 2013 with C++ on the build computer.

**Visual Studio is not required on the PostgreSQL Server.**

It can be build from the Developer Command Prompt with msbuild and the following cmd :

- ```msbuild /p:Configuration=Release /p:Platform="Win32"``` for 32bits
- ```msbuild /p:Configuration=Release /p:Platform="x64"``` for 64bits

The build is configured to use PostgreSQL libraries from the following folders :

- ```C:\Program Files (x86)\PostgreSQL\9.5\``` for 32bits
- ```C:\Program Files\PostgreSQL\9.4\``` for 64bits

The output path are in the solution directory :

- ```Release_Win32``` for 32bits
- ```Release_x64``` for 64bits


Installation
------------
The pg_wintools.dll must be placed in the ```lib\``` folder of your postgresql installation.
(i.e. : ```C:\Program Files (x86)\PostgreSQL\9.5\lib\```)

Once it's done, you can create a function in any database that needs it with :

```
CREATE OR REPLACE FUNCTION pg_write_event_log_entry(
    text,
    integer)
  RETURNS void AS
'pg_wintools', 'pg_write_event_log_entry'
  LANGUAGE c ;

CREATE OR REPLACE FUNCTION pg_file_exists(text)
  RETURNS boolean AS
'pg_wintools', 'pg_file_exists'
  LANGUAGE c ;


CREATE OR REPLACE FUNCTION pg_hostname()
  RETURNS text AS
'pg_wintools', 'pg_hostname'
  LANGUAGE c ;

CREATE OR REPLACE FUNCTION pg_read_registry(
    text,
    text,
	text)
  RETURNS text AS
'pg_wintools', 'pg_read_registry'
  LANGUAGE c ;
  
CREATE OR REPLACE FUNCTION pg_fixed_drives_list()
  RETURNS SETOF RECORD AS
'pg_wintools', 'pg_fixed_drives_list'
  LANGUAGE c ;

```

----
Tested with PostgreSQL 9.4 (64bits) and 9.5b (32bits) on the following platforms :

- Windows Server 2008 R2
- Windows Server 2012 R2	
- Windows 8.1		
- Windows 10	


# Install GPMC - Group Policy Management Console

Download the latest version from Releases:       
https://github.com/poldeploy/GPMC/releases/tag/1.0.2

## System requirements

* Requires .NET Framework version 4.6 or higher
* Minimum supported operating systems: Windows Vista or Windows Server 2008

## Install instructions

1. Proceed with one of the following options:

   * To launch the installation right away, click **Open** or **Run this program from its current location**.
   * To save the setup file for later use, click **Save** or **Save this program to disk**.
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
 
