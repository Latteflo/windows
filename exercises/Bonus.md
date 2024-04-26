# P0w3rsh3ll Bonus  

## The mission

**[Iron scripter](https://ironscripter.us/)** doesn't seem to be up online all the time, if not use the time machine to get there anyway. Find the March 10, 2022 challenge entitled **"An Up and Down PowerShell Challenge"** and try to write us a nice function. It'll make the Chairman happy.
<br>
<br>

<p align="center">
  <img src="https://images3.memedroid.com/images/UPLOADED172/5c8ff6e3201a0.jpeg" />
</p>


## Instructions - An Up and Down PowerShell Challenge :
The Chairman has a new challenge to prepare his scripting warriors for the upcoming PowerShell Summit. The challenge is aimed at intermediate to advanced scripters. You are encouraged to fulfill as many of the requirements as you can.

The Chairman would like a tool that he can use to query a Windows-based server to discover the following information:

    When was a server last shutdown?
    When did the server start up again?
    How long was it down?
    What is the current uptime?

Naturally, the output should include the computer name. To show your scripting superiority, the output should also include the account that initiated the shutdown or reboot. The function should accept alternate credentials and be able to accept pipeline input for a list of server names.

## Solution

```powershell
    function Get-ServerUptime {
        [CmdletBinding()]
        param (
            [Parameter(ValueFromPipeline = $true)]
            [string[]]$ComputerName = $env:COMPUTERNAME,
            [pscredential]$Credential
        )

        begin {
            $os = Get-CimInstance -ClassName Win32_OperatingSystem
        }
    
        process {
            foreach ($computer in $ComputerName) {
                $params = @{
                    ComputerName = $computer
                    Credential = $Credential
                }
    
                $os = Get-CimInstance -ClassName Win32_OperatingSystem @params
    
                $lastBootUpTime = $os.LastBootUpTime
                $lastShutdownTime = $os.LastShutdownTime
                $uptime = $os.LocalDateTime - $lastBootUpTime
                $downtime = $lastBootUpTime - $lastShutdownTime
    

                [PSCustomObject]@{
                    ComputerName = $computer
                    LastShutdownTime = $lastShutdownTime
                    LastBootUpTime = $lastBootUpTime
                    Uptime = $uptime
                    Downtime = $downtime
                    Account = (Get-WinEvent -LogName System -ComputerName $computer -MaxEvents 1 |
                        Where-Object { $_.Id -eq 1074 -or $_.Id -eq 1076 } |
                        Select-Object -ExpandProperty Properties |
                        Where-Object { $_.ValueName -eq 'User' }).Value
                }
            }
        }
    }

