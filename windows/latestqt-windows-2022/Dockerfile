# escape=`
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2022
ARG QT_VERSION=6.9.3
SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]
# Install Chocolatey
RUN Set-ExecutionPolicy Bypass -Scope Process -Force; `
    [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
# Install build tools and dependencies
RUN choco install -y `
    visualstudio2022buildtools `
    visualstudio2022-workload-vctools `
    cmake `
    ninja `
    git `
    python3 `
    7zip `
    innosetup
# Install aqtinstall
RUN python -m pip install --upgrade pip; `
    pip install aqtinstall
# Install Qt for Windows with MSVC 2022
RUN aqt install-qt windows desktop $env:QT_VERSION win64_msvc2022_64 -O C:\Qt -m qt5compat qthttpserver qtimageformats qtmultimedia qtshadertools qtwebsockets
# Set Qt environment variables
ENV PATH="C:\Qt\${QT_VERSION}\msvc2022_64\bin;${PATH}"
ENV QT_PLUGIN_PATH="C:\Qt\${QT_VERSION}\msvc2022_64\plugins"
ENV QML_IMPORT_PATH="C:\Qt\${QT_VERSION}\msvc2022_64\qml"
WORKDIR C:\workspace