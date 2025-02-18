

## Desc

a unified, open-source service management framework for starting, stopping and managing daemons, applications, processes, and scripts.


## Property List

Example plist for running a script locally. 
`chmod +x` of course of the user generated script.

```swift
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Label</key>
	<string>local.sensehack.github.runner.auto.start</string>
	<key>Program</key>
	<string>/Users/builder/actions-runner/run-helper.sh</string>
	<key>StartInterval</key>
	<integer>3600</integer>
	<key>StandardOutPath</key>
	<string>/Users/builder/kay_logs/auto_script/log.stdout</string>
	<key>StandardInPath</key>
	<string>/Users/builder/kay_logs/auto_script/log.stdin</string>
	<key>StandardErrorPath</key>
	<string>/Users/builder/kay_logs/auto_script/log.stderr</string>
</dict>
</plist>
```

## Commands


Load the script.

```sh
launchctl load -w ~/Library/LaunchAgents/auto_run_script.plist
```

Start a specific job.
```sh
launchctl start auto_run_script
```

Check the status of your job. A status of zero is a successful run.

```sh
launchctl list | grep "local.sensehack"
```

The label is where the name of the running job is listed as in the terminal processes.


## References

[launchd Info](https://www.launchd.info/)

[good tutorial for simple launchd script](https://veerpalbrar.github.io/blog/How-to-Run-A-Program-or-Script-Hourly-on-MacOS/)

