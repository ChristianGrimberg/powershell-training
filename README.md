# PowerShell essential training repository

## Basic CmdLets

* Getting the version of PowerShell:

    ```powershell
    $PSVersionTable # Get info about PowerShell installation
    $PSVersionTable.PSVersion # Get the specific version of PowerShell installation
    ```

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

* List files and folders:

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

* Managing Windows Operating System's Process:

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
    Get-WmiObject -Class Win32_LogicalDisk -Filter "DeviceID='C:'" | Select-Object -Property FreeSpace # Get the free space of specific partition letter
    Get-WmiObject -Class Win32_Bios | Select-Object * # List all objects from specific WMI Class
    Get-WmiObject -Query "SELECT * FROM SoftwareLicensingService" | Select-Object -Property OA3xOriginalProductKey # Get the OEM Product Key
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
    * Pipeline operator:

        Operator     | Meaning                  | Example                               | Description
        :----------: | :----------------------- | :------------------------------------ | :----------
        `\|`         | Pipeline (ASCII 124)     | `Command-1 \| Command-2 \| Command-3` | Each pipeline operator sends the results of the preceding command to the next command.

    * Type operators:

        Operator     | Meaning                  | Example                               | Description
        :----------: | :----------------------- | :------------------------------------ | :----------
        `-is`        | Compare types            | `64 -is [Int] # true`                 | Validates if the type of the object on the left is the same as the one on the rigth.
        `-isNot`     | Compare types (inverted) | `99 -isNot [Int] # false`             | Validates if the type of the object on the left is not the same as the one on the right.
        `as`         | Cast                     | `1000 -as [DateTime]`                 | Converts the object on the left to the specific type.
        `.GetType()` | Show type                | `([Int]"676").GetType()`              | Shows the .NET Function for every object. Retrieves the type of the object.

    * Arithmetic operators:

        Operator       | Meaning                                        | Description
        :------------: | :--------------------------------------------- | :----------
        `+`            | Add                                            | Adds numeric object.<br>Concetenates strings, arrays and hash tables.
        `-`            | Subtract and negate                            | Subtracts numeric values.<br>Negate numbers.
        `*`            | Multiply                                       | Multiplies numeric values.<br>Multiplies strings and arrays the specified number of times.
        `/`            | Divide                                         | Divides numeric objects with the specified number of times.
        `%`            | Modulo                                         | Returns the remainder of a division.
        `-shl`         | Shift-left                                     | Moves all bits _n_ places to the left.
        `-shr`         | Shift-right                                    | Moves all bits _n_ places to the right.
        `()`           | Parentheses                                    | Mathematical predence order.

    * Assignment operators:

        Operator       | Meaning                                        | Description
        :------------: | :--------------------------------------------- | :----------
        `=`            | Assign                                         | Assigns the value on the right to the left one.
        `+=`           | Add and assign                                 | Adds the right value to the left one and assigns it.
        `-=`           | Subtract and assign                            | Subtract the right value from the left one and assigns it.
        `*=`           | Multiply and assign                            | Multiplies the right value by the left one and assigns it.
        `/=`           | Divide and assign                              | Divides the right value by the left one and assigns it.
        `%=`           | Modulo and assign                              | Invokes a modulo between the right value and the left one and assigns it.

    * Comparison operators:

        Operator       | Meaning                                        | Description
        :------------: | :--------------------------------------------- | :----------
        `-eq`          | Equals                                         | Returns equality between left and right value.
        `-ne`          | Not equal                                      | Returns equality negated.
        `-gt`          | Greater-than                                   | Returns if left value is greater than right one.
        `-ge`          | Greater-than or equal to                       | Returns if left value is greater than or equal to rigth one.
        `-lt`          | Less-than                                      | Returns if left value is less than right one.
        `-le`          | Less-than or equal to                          | Returns if left value is less than or equal to right one.
        `-like`        | Matching a defined filter                      | Returns if left value is similar to right one, using a filter/wildcard.
        `-notlike`     | Not matching a defined filter                  | Returns if left value is not similar to rigth one, using a filter/wildcard.
        `-match`       | Matching a defined _RegEx_ filter              | Returns if left value is similar to rigth one, using _RegEx_.
        `-notmatch`    | Not matching a defined _RegEx_ filter          | Returns if left value is not similar to right one, using _RegEx_.
        `-contains`    | Collection containing an object                | Returns is left collection contains one object, same as the rigth one.
        `-notcontains` | Collection not containing an object            | Returns is left collection does not contain one object, same as the right one.
        `-in`          | Value is in a collection of refence values     | Returns is left object is included in collection on the right.
        `-notin`       | Value is not in a collection of refence values | Returns is left object is not included in collection on the right.

        > If the letter __`i`__ is added to the beginning of the comparison operator, means __explicity case insensitive__, and if the letter __`c`__ is added to the beginning of the comparison operator, means __explicity case sensitive__.

    * Logical operators:

        Operator       | Meaning                                        | Description
        :------------: | :--------------------------------------------- | :----------
        `-and`         | Combines two expressions with `AND`            | Returns `true` if both are true.
        `-or`          | Combines two expressions with `OR`             | Returns `true` if one or both are true.
        `-xor`         | Combines two expressions with `XOR`            | Returns `true` if one of the expressions is true and the other one is false.
        `-not`         | Negate                                         | Negate the expression.
        `!`            | Negate                                         | Negate the expression.

    * Split and join operators:

        Operator       | Meaning                                        | Description
        :------------: | :--------------------------------------------- | :----------
        `-split`       | Split string                                   | Split strings and returns values as arrays.
        `-join`        | Join strings                                   | Jopins strings with specific layouts together.

        > If the letter __`i`__ is added to the beginning of the `split` operator, means __explicity case insensitive__, and if the letter __`c`__ is added to the beginning of the `split` operator, means __explicity case sensitive__.

    * Bitwise logical operators:

        Operator       | Meaning                                        | Description
        :------------: | :--------------------------------------------- | :----------
        `-band`        | Bitwise `AND`                                  | Returns the bitwise `AND` operation between left and right values.
        `-bor`         | Bitwise `OR` inclusive                         | Returns the bitwise `OR` operation between left and rigth values.
        `-bxor`        | Bitwise `OR` exclusive                         | Returns the bitwise `XOR` operation between left and rigth values.
        `-bnot`        | Bitwise `NOT`                                  | Returns the bitwise `NOT` operation between left and rigth values.

    * Replace operator:

        Operator     | Meaning                  | Example                                                   | Description
        :----------: | :----------------------- | :-------------------------------------------------------- | :----------
        `-replace`   | Replacement of strings   | `"Hello world" -replace "world", "human" # "Hello human"` | Allows for the systematic replacement of strings using regular expressions.

    * Unary Operators:

        ```powershell
        $a = 1 # Initialize variable
        $a++ # 2 -> Increment after
        $a-- # 1 -> Decrement after
        ++$a # 2 -> Increment before
        --$a # 1 -> Decrement before
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
    Get-ChildItem -Path ./ | Sort-Object -Property Length -Descending # Order a list by length and descending
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

* Format results:

    ```powershell
    # Concatenate string with variables
    $var = "World"
    Write-Host "Hello $var!"
    Write-Host ("Hello {0}!" -f $var)
    Write-Host ("Hello {0} {1}!" -f "cruel", $var)
    $var = Get-Date
    Write-Host ("The time is {0:HH:mm}" -f $var)
    $var = 0.5
    Write-Host ("The percent is {0:p}" -f $var)
    ```

* Tables, lists and grid results:

    ```powershell
    Get-ChildItem -Path ./ | Format-Table -Property Name, Length # Results in table with specific columns
    Get-ChildItem -Path ./ | Format-List -Property Name, Length # Results in a list with specific properties
    Get-ChildItem -Path ./ | Out-GridView # Show the results with graphic interface (only works on Windows)
    Get-ChildItem -Path ./ | Out-GridView -PassThru | Remove-Item # Remove selected item in graphical interface
    ```

## Export data format

* Export results to `TXT` format:

    ```powershell
    Get-Service | Out-File -Path ./Services.txt # Write a TXT file with the Service list in table format
    Get-Content -Path ./Services.txt
    ```

* Export results to `CSV` format:

    ```powershell
    Get-Service | Export-Csv -Path ./Services.csv # Export to CSV file with powershell format
    Get-Service | Export-Csv -Path ./Services.csv -NoTypeInformation # Export to CSV file without PowerShell format to read from other apps
    ```

* Export results to `XML` format:

    ```powershell
    Get-Service |  Export-Clixml -Path ./Services.xml # Export to XML file
    Import-Clixml -Path ./Services.xml # Import XML file to PowerShell
    ```

* Export result to `HTML` format:

    ```powershell
    Get-EventLog -LogName system -Newest 2 -EntryType error | ConvertTo-Html | Out-File -FilePath ./errors.html # Export to HTML file
    Get-EventLog -LogName system -Newest 2 -EntryType error | ConvertTo-Html -Title "Windows Errors" -Body (Get-Date) -PreContent "<p>Generated by IT</p>" -PostContent "For more details check the full server logs" | Out-File -FilePath ./errors.html
    ```

* Compare data file content:

    ```powershell
    Compare-Object -ReferenceObject (Import-Clixml -Path ./Services.xml) -DifferenceObject (Get-Service) -Property DisplayName, Status
    ```

## Scripting with PowerShell

* Using variables:

    ```powershell
    # View the variable type
    $var = "Hello"
    $var.GetType()
    $var = 2
    $var.GetType()
    # Remove the variable
    Remove-Variable var
    # Typed variables
    [String]$name = "Joe"
    [Int]$age = 10
    [Object]$Items = Get-ChildItem -Path ./
    ```

* Using Array Lists:

    ```powershell
    # Load lists into variables
    $var1 = 1,2,3
    $var2 = "One", "Two", "Three"
    # Access to specific value
    $var1[0]
    $var2[2]
    $var1[0,2]
    $var2 = $var2 + "Four"
    $var2[-1] # Access to last load value
    $var1[1..3] # Acces to a range of values
    # Load a list with keys/values
    $var = @{Name = "Chris"; LastName = "Grimberg"}
    $var # See a table with the keys and values
    $var.Name # Access to specific value from a key
    # Load a variable with a objects return from a cmdlet
    $var = Get-ChildItem -Path ./ # If you change a vale after that, it's not changing the objects in this variable
    $var | Select-Object -Property Name # You can pipe the results
    $var[0] # Access to the first object returns
    $var[0].Name # Access to a specific Object's Property
    ```

* Using IF statements:

    ```powershell
    # Sintax of IF statements: if (condition) {execution}
    if (1 -eq 1) {Write-Host "This is a first test"}
    if ($true) {Write-Host "This is a second test"}
    # Example 1: Indicate that there are less than 10 objects
    $var = Get-ChildItem -Path ./ | Measure-Object | Select-Object Count
    if ($var.Count -lt 10)
    {Write-Host "It has less than 10 objects."}
    # Sintax of IF/ELSEIF/ELSE statements: if (condition) {execution} elseif (other condition) {other execution} else {final execution}
    if ($var.Count -lt 10) {Write-Host "It's less than 10"}
    elseif ($var.Count -eq 10) {Write-Host "It's 10"}
    else {Write-Host "It's greather than 10"}
    ```

* Using SWITCH statements:

    ```powershell
    # Example: common use
    $var = 3
    switch ($var)
    {
        1 {Write-Host "One"}
        2 {Write-Host "Two"}
        3 {Write-Host "Three"}
        default {Write-Host "Other number"} # Optional
    }
    # Example: using wildcards
    $var = "Carl Sagan"
    switch -Wildcard ($var)
    {
        "Carl*" {Write-Host "Carl is your name"; break} # break is optional
        "*Sagan" {Write-Host "Sagan is your last name"}
        default {Write-Host "Nice to meet you"}
    }
    ```

* Using WHILE iterations:

    ```powershell
    # Example: common use
    [Int]$var = 1
    while ($var -lt 10)
    {
        Write-Host $var
        $var++
    }
    ```

* Using FOR iterations:

    ```powershell
    # Example: common use
    for ($var = 0; $var -lt 10; $var++)
    {
        Write-Host ("Number {0}" -f $var)
    }
    ```

* Using FOREACH and FOREACH-OBJECT iterations:

    ```powershell
    # Example: using foreach in common cases
    $names = "Jenny", "Jack", "Tom"
    foreach ($name in $names)
    {
        Write-Host ("Hi {0}!" -f $name)
    }
    # Example: using foreach-object in common cases
    $names = "Jenny", "Jack", "Tom"
    $names | ForEach-Object { Write-Host ("Hi {0}" -f $_)}
    # Example: using foreach-object with objects
    Get-ChildItem -Path ./ -Directory | ForEach-Object { Write-Host ("Folder Name: {0}" -f $_.Name)}
    ```

* Using arguments:

    ```powershell
    # Example: Script content to print all the arguments
    $args | ForEach-Object { Write-Host ("Value: {0}" -f $_)}
    # Example: Read argument by array id
    Write-Object ("Value of first argument: " -f $args[0])
    ```

* Read user input:

    ```powershell
    # Example: common use
    [Int]$number = Read-Host -Prompt "What´s for favorite number?"
    Write-Host ("Your favorite number is: {0}" -f $number)
    # Example: password input
    [String]$password = Read-Host -Prompt "Password" -AsSecureString
    ```

* Using parameters into script:

    ```powershell
    # Example using one parameter
    param (
        [Parameter(Mandatory=$true)] # Optional: This parameter is mandatory to input
        [String] # Optional: This parameter has case sensitive for the specific type
        $Var = "Hello" # Optional: This parameter has default value
    )

    #Example using more than one parameter
    param (
        [String]
        $Var1,
        [Int]
        $Var2
    )

    # Example using a array list in the parameter
    param (
        [Int[]]
        $Var
    )

    # Example using help content in the script
    <#
    .SYNOPSIS
        A simple description
    .DESCRIPTION
        A full description
    .PARAMETER Number
        A description of the parameter
    .EXAMPLE
        An example using this script
    #>
    param (
        [Int]
        $Number
    )
    ```