name: ARM-TTK Validation

on:
  push:
    branches:
      - main

jobs:
  build_and_test:
    runs-on: windows-latest
    steps:
      - name: Install Azure PowerShell Module
        uses: Azure/powershell@v1
        with:
          azPSVersion: '3.1.0'
          inlineScript: |
            Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
            choco Install azure-cli -y
      - name: Clone ARM-TTK 
        run: |
          git clone https://github.com/Azure/arm-ttk.git
      - name: Validate ARM templates using ARM-TTK
        shell: pwsh
        working-directory: ./github/worflows/main.yml
        run: |
          Get-ChildItem *.ps1, *.psd1, *.ps1xml, *.psm1 -Recurse | Unblock-File
          Import-Module .\arm-ttk.psd1
          Test-AzTemplate -TemplatePath ./mainTemplate.json

          https://github.com/kar122/clonerepo/blob/main/mainTemplate.json
