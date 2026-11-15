# STIG-9

<#
.SYNOPSIS
    This PowerShell script ensures Kerberos encryption types are configured to prevent weak encryption algorithms (AES only).

.NOTES
    Author          : Htain Ney
    Date Created    : 2026-06-12
    Last Modified   : 2026-06-12
    Version         : 1.0
    CVEs            : N/A
    Plugin IDs      : N/A
    STIG-ID         : WN11-SO-000190

.TESTED ON
    Date(s) Tested  : 2026-11-14
    Tested By       : Htain Ney
    Systems Tested  : Windows 11
    PowerShell Ver. : 5.1

.USAGE
    PS C:\> .\STIG-ID-WN11-SO-000190.ps1
#>

$registryPath = "HKLM:\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters"
$valueName = "SupportedEncryptionTypes"
$valueData = 2147483640 # 0x7FFFFFF8 (Enforces AES128, AES256, and Future types)

if (-not (Test-Path $registryPath)) { New-Item -Path $registryPath -Force }
Set-ItemProperty -Path $registryPath -Name $valueName -Value $valueData -Type DWord
Write-Host "Registry value '$valueName' set to '$valueData' at '$registryPath'."
