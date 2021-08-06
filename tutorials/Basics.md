# Installation [https://docs.microsoft.com/en-us/windows/wsl/install-win10]
- install docker
- install WSL
    - Step 1 - Enable the Windows Subsystem for Linux
        * `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
    - Enable Virtual Machine feature
        * `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
    - Set WSL 2 as your default version
        * `wsl --set-default-version 2` 



# Command to run

docker run -d -p 80:80 docker/getting-started


