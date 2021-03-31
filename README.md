# Powershell essential training repository

## Basic CmdLets

* __`Get-Help`__ Getting help from all the Powershell CmdLets:

    ```powershell
    Get-Help * # Display available help articles
    Get-Help -Name Get-ChildItem # Display basic help information about a cmdlet
    Get-Help -Name Get-Process -Examples # Display cmdlet examples
    Get-Help -Name Get-Content -Online # Display online version of help
    Get-Help -Name Write-Host -Detailed # Display more information for a cmdlet
    Get-Help -Name New-PSSession -Parameter ComputerName # Display selected parts of a cmdlet by using parameters
    ```

* __`Get-Alias` and `Set-Alias`__ Using Aliases with Powershell:

    ```powershell
    Get-Alias # Get all aliases in the current session
    Get-Alias -Definition Get-ChildItem # Get aliases for a cmdlet
    New-Alias -Name "List" -Value Get-ChildItem # Create an alias for a cmdlet
    ```

* __Get-PSDrive__ and `Set-Location` Browse across drives:

    ```powershell
    Get-PSDrive # Get a list of available drivers in the system
    Set-Location Env: # Change the drive to the Environments
    ```