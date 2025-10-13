# Finding the hardware UUID of a device

In order to help us identify and locate any device that is flagged for investigation by Microsoft Defender for Endpoint (MDE) we aim to record the hardware UUID (Universal Unique Identifier) of each laptop purchased through the department. 

## Windows

Open the “Terminal” app (or open “Command Prompt” and then type `powershell`) and then run the following PowerShell command:
```
Get-CimInstance -ClassName Win32_ComputerSystemProduct | Select-Object -Property UUID
```

## macOS

Click the Apple icon, then select "About This Mac" then "More Info..." and "System Report".

## Linux

Run the following command:
```
sudo dmidecode | grep UUID
```