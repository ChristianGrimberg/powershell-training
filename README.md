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
    Set-Location Env: # Change the drive to the Environments
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