FROM mcr.microsoft.com/dotnet/framework/sdk:3.5

COPY ./setups/ c:/setups/

# Run all the setups and copy this two files so msbuild can find the files when running
RUN Start-Process msiexec.exe -Wait -ArgumentList '/i c:\setups\NETCFSetupv2.msi /qn' ;\
    Start-Process msiexec.exe -Wait -ArgumentList '/i c:\setups\NETCFSetupv35.msi /qn' ;\
    Start-Process msiexec.exe -Wait -ArgumentList '/i c:\setups\NETCFv35PowerToys.msi /qn' ;\
    Remove-Item C:/setups -Recurse ;\
    Copy-Item c:\Windows\Microsoft.NET\Framework\v3.5\Microsoft.CompactFramework.CSharp.targets -Destination 'C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\MSBuild\Current\Bin\Microsoft.CompactFramework.CSharp.targets' ;\
    Copy-Item c:\Windows\Microsoft.NET\Framework\v3.5\Microsoft.CompactFramework.Common.targets -Destination 'C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\MSBuild\Current\Bin\Microsoft.CompactFramework.Common.targets' ;\
# Install Chocolatey
    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) ;\
# Install Git
    choco install git.install -y
