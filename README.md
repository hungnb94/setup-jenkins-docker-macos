# Jenkins + Docker setup instructions step by step
## Install Jenkins
### Install the latest LTS version
`brew install jenkins-lts`
### Start the Jenkins service:
`brew services start jenkins-lts`
### After starting the Jenkins service, browse to http://localhost:8080 and follow the instructions to complete the installation

## Install Docker


# Fix common issues
## How to access Jenkins web interface from anywhere (not just on the local machine)?

- Open file homebrew.mxcl.jenkins-lts.plist. This file located in
  - /opt/homebrew/Cellar/jenkins-lts/2.414.1/homebrew.mxcl.jenkins-lts.plist (2.414.1 is jenkins-lts version)
  - or /usr/local/opt/jenkins-lts/homebrew.mxcl.jenkins-lts.plist

- Find this line:
`<string>--httpListenAddress=127.0.0.1</string>`

- And change it to:
```<string>--httpListenAddress=0.0.0.0</string>```

## How to fix docker command not found
- Open file homebrew.mxcl.jenkins-lts.plist
- Add following content
```
	<key>EnvironmentVariables</key>
	<dict>
	<key>PATH</key>
	<string>/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/Docker.app/Contents/Resources/bin/:/Users/hungba/Library/Group\ Containers/group.com.docker/Applications/Docker.app/Contents/Resources/bin</string>
	</dict>
```
- Full content of file:
```<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Label</key>
	<string>homebrew.mxcl.jenkins-lts</string>
	<key>LimitLoadToSessionType</key>
	<array>
		<string>Aqua</string>
		<string>Background</string>
		<string>LoginWindow</string>
		<string>StandardIO</string>
		<string>System</string>
	</array>
	<key>ProgramArguments</key>
	<array>
		<string>/opt/homebrew/opt/openjdk@17/bin/java</string>
		<string>-Dmail.smtp.starttls.enable=true</string>
		<string>-jar</string>
		<string>/opt/homebrew/opt/jenkins-lts/libexec/jenkins.war</string>
		<string>--httpListenAddress=127.0.0.1</string>
		<string>--httpPort=8080</string>
	</array>
	<key>RunAtLoad</key>
	<true/>
	// Add from here
	<key>EnvironmentVariables</key>
	<dict>
	<key>PATH</key>
	<string>/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/Docker.app/Contents/Resources/bin/:/Users/hungba/Library/Group\ Containers/group.com.docker/Applications/Docker.app/Contents/Resources/bin</string>
	</dict>
	// finish add
</dict>
</plist>
```
