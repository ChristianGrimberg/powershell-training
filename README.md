# PowerShell essential training repository

## Basic CmdLets

* Getting help from all the Powershell CmdLets with __`Get-Help`__:

    ```powershell
    Update-Help # Update the command's helpers included in PowerShell
    Get-Help * # Display available help articles
    Get-Help -Name Get-ChildItem # Display basic help information about a cmdlet
    Get-Help -Name Get-Process -Examples # Display cmdlet examples
    Get-Help -Name Get-Content -Online # Display online version of help
    Get-Help -Name Write-Host -Detailed # Display more information for a cmdlet
    Get-Help -Name New-PSSession -Parameter ComputerName # Display selected parts of a cmdlet by using parameters
    ```

* Working with commands:

    ```powershell
    Get-Command # Get a list of available commands
    Get-Command -Name Get-* # Get a list of commands filtering by a wildcard name
    Get-Command -CommandType Function # Get a list of command by type
    ```

* Using Aliases:

    ```powershell
    Get-Alias # Get all aliases in the current session
    Get-Alias -Definition Get-ChildItem # Get aliases for a cmdlet
    New-Alias -Name "List" -Value Get-ChildItem # Create an alias for a cmdlet
    ```

* Browse across drives:

    ```powershell
    Get-PSDrive # Get a list of available drivers in the system
    Set-Location -Path Env: # Change the drive to the Environments
    ```

* Manage PowerShell Modules:

    ```powershell
    Get-Module # Get a list of imported modules in the system
    Find-Module -Filter backup # Find a module with a filter
    Install-Module -Name azurerm # Gets one or more modules that meet specified criteria from an online repository.
    Import-Module -Name azurerm # Adds one or more modules to the current session
    Remove-Module -Name azurerm # Removes the members of a module, such as cmdlets and functions
    ```

* Managing files and folders:

    ```powershell
    Get-ChildItem # Get a list of files and folders on current directory
    Get-ChildItem -Path ./ # Get a list with relative positions
    Set-Location -Path ../ # Change the location to a relative directory or absolute location
    Get-ChildItem -Directory # Get a list of folders only
    Get-ChildItem -File # Get a list of files only
    Get-Item -Path ./ # Get info about a specific folder or file
    Get-ChildItem -Path ./*.txt # Get a list filtering by a wildcard
    ```

* Manipulating files and folders:

    ```powershell
    New-Item -Name test -ItemType Directory # Create a new folder
    New-Item -Name example.txt - ItemType File # Create a new file
    Get-Content -Path ./test/example.txt # Get file's content
    Set-Content -Path ./test/example.txt -Value "Writing values" # Write all the content of the specific file
    Add-Content -Path ./test/example.txt -Value "Another values" # Add values to a specific file before a line break
    Clear-Content -Path ./test/example.txt # Clear all the content of specific file
    Rename-Item -Path ./test/example.txt example2.txt # Rename the specific file or folder
    Remove-Item -Path ./test/example2.txt # Remove the file or folder without ask
    ```

## Managing Windows Operating System

* Managing Operating System's Process:

    ```powershell
    Get-Process # Get a entire list of running process in the operating system
    Get-Process -Name Docker # Get a list of process named as specific name
    Start-Process -FilePath ./process # Start a specific process located at specific path
    Stop-Process -Id 1 # Stop the process with a specific Id
    Stop-Process -Name Docker # Stop all the process with name Docker
    Wait-Process -Id 1 # Waiting in the console until the process has stoped
    ```

* Managing Microsoft Windows Services:

    ```powershell
    Get-Service # Get a list of Windows Services
    Get-Service -Name x* # Get a list of Windows Services filtering by a wildcard name
    Get-Service | Select-Object * # Get a list of Windows Services with all their objects
    Start-Service -Name SensorService # Run a specific Windows Service
    Stop-Service -Name SensorService # Stop a specific Windows Service
    Restart-Service -Name SensorService # Restart a specific Windows Service
    Suspend-Service -Name Winmgmt # Pause a specific Windows Service
    Resume-Service -Name Winmgmt # Play a paused Windows Service
    New-Service -Name Test -BinaryPathName ./service.exe # Create a new service with a specific binary file
    ```

* Working with Windows Registry:

    ```powershell
    Set-Location -Path HKLM:\SOFTWARE # Go the the specific Windows Registry Key
    Get-ChildItem -Path ./ # List keys under the specific path
    Get-ItemProperty -Path ./ # List values under a specific path
    New-Item -Path ./ -Name Test # Create a new key on a specific Windows Registry path
    New-ItemProperty -Path ./ -Name ValueName -Value example # Create a new value in the specific Windows Registry key
    Remove-ItemProperty -Path ./ -Name ValueName # Delete a specific Windows Registry value
    Remove-Item -Name Test # Delete a specific Windows Registry key
    ```

* Get info from Windows Management Instrumentation with __`Get-WmiObject`__:

    ```powershell
    Get-WmiObject -Class Win32_DiskDrive # Get info about a WMI Class
    Get-WmiObject -Class Win32_Bios | Select-Object * # List all objects from specific WMI Class
    ```

## Using object oriented sintax

* Get object properties and methods:

    ```powershell
    Get-Item -Path ./ | Select-Object * # Get all the properties on specific path
    Get-Process -Name Docker | Select-Object * # Get all the properties on specific process
    Get-Item -Path ./ | Get-Member # Get all object members including proerties and methods
    $folder = Get-Item -Path ./ # Storing the object into a variable
    $folder.ToString() # For example, using a method of this object
    $folder.CreationTime # For example, using a property of this object
    ```

## Combine operations with CmdLets in PowerShell

* Operators:

    ```powershell
    # -eq: equal
    # -gt: greater than
    # -lt: less than
    # -like: like a
    # -le: less or equal
    # -ge: greater or equal
    # -and: and
    # -or: or
    ```

* Filtering and sorting the results using the pipeline:
    ```powershell
    Get-ChildItem -Path ./ | Where-Object -Property Extension -like "*.txt" # Example filtering by extension
    Get-ChildItem -Path ./ | Sort-Object -Property Length # Example sorting in the specific path
    Get-ChildItem -Path ./ | Where-Object -Property Extension -like "*.txt" | Sort-Object -Property Length # Example combining two pipes
    Get-ChildItem -Path ./ | Where-Object -Property Length -gt 200 # Example filtering by length
    Get-ChildItem -Path ./ | Where-Object -Property Name -eq "file.txt" # Example filtering with specific property
    Get-ChildItem -Path ./ -File | Where-Object -Property Length -lt 10000 # Example filtering files by Length
    Get-ChildItem -Path ./ -File | Where-Object {(($_.Name like "w*") -and ($_.Length -gt 300)) -or ($_.Extension -like ".txt")} # Example with multiple filtering
    ```

* Statistical results using the pipeline:

    ```powershell
    Get-ChildItem -Path ./ | Measure-Object # Get a general statist results
    Get-ChildItem -Path ./ | Measure-Object -Property Length -Average # Get average of file's length on specific path
    Get-ChildItem -Path ./ | Measure-Object -Property Length -Sum # Get the total length of all the objects in specific path
    Get-ChildItem -Path ./ | Measure-Object -Property Length -Maximum # Get the largest file on specific path
    Get-Content -Path ./file.txt | Measure-Object -Character -Line -Word # Get full statist of a file content
    ```

* Select results using the pipeline:

    ```powershell
    Get-ChildItem -Path ./ | Select-Object -Property Name, Length, CreationTime # Get a list with specific property's columns
    Get-Process | Select-Object -Unique # Get a process list with unique results
    Get-ChildItem -Path ./ -File | Select-Object -Property Name, Length -First 5 # Get the first results with specific columns
    Get-ChildItem -Path ./ -File | Sort-Object -Property Length | Select-Object -First 3 # Get the fists result with largest length
    ```