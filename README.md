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
    Get-ChildItem -Path ./*.txt # Get a list filtering with a wildcard
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