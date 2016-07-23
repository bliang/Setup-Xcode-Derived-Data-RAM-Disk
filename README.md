# Get the Fastest Build Times in Xcode

Instead of having Xcode’s Derived Data be based in a spinning disk or solid-state drive, moving it to a RAM disk can make the performance of Xcode build operations *as fast as possible* and make it so that your Derived Data content is continually freshened.

I’ve crafted a script in Swift to perform the necessary configuration. I start the script in a launch agent that runs at startup so that my RAM disk is always available. Returning to a standard Xcode configuration simply requires ejecting the RAM disk.

## Installation

Copy `main.swift` to a local path of your choosing such as

	~/bin/setupXcodeDerivedDataRAMDisk.swift
	
Make it executable.

## Run at Startup

Create a file with the following content. **Edit it so that it fits your system.**

    <?xml version=1.0 encoding=UTF-8?>
    <!DOCTYPE plist PUBLIC -//Apple//DTD PLIST 1.0//EN http://www.apple.com/DTDs/PropertyList-1.0.dtd>
    <plist version=1.0>
    <dict>
    <key>Label</key>
    <string>com.ikiapps.setupXcodeDerivedDataRamDisk.plist</string>
    <key>ProgramArguments</key>
    <array>
    <string>/usr/bin/xcrun</string>
    <string>/Users/USERNAME/bin/setupXcodeDerivedDataRAMDisk.swift</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>LaunchOnlyOnce</key>
    <true/>
    </dict>
    </plist>

Give it a name like `com.ikiapps.setupXcodeDerivedDataRamDisk.plist` and copy it to

	~/Library/LaunchAgents
	
The minimum permission for this property list launch agent file is that it is readable by you.

The agent can be started manually using

	launchctl load com.ikiapps.setupXcodeDerivedDataRamDisk.plist
	
If everything went well, the script will now run every time you login.