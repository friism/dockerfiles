FROM microsoft/windowsservercore

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

ENV JDK_VERSION zulu8.19.0.1-jdk8.0.112-win_x64

RUN Invoke-WebRequest "http://cdn.azul.com/zulu/bin/$Env:JDK_VERSION.zip" -OutFile jdk.zip -UseBasicParsing ; \
	Expand-Archive jdk.zip -DestinationPath C:\jdk-temp ; \
	New-Item -Type Directory C:\jdk ; \
	mv C:\jdk-temp\$Env:JDK_VERSION\* C:\jdk\. ; \
	Remove-Item .\jdk.zip ; \
	Remove-Item -Recurse -Force C:\jdk-temp

RUN $newPath = ('C:\jdk\bin;{0}' -f $env:PATH); \
	setx /M PATH $newPath
RUN setx /M JAVA_HOME 'C:\jdk\bin'
