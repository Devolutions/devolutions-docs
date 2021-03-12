---
uid: wayk-agent-configuration
---

# Wayk Agent Configuration

### Configuration using UI

The Agent can be configured using the user interface, via the Options ("Preferences" on macOS) window. The Agent configuration requires administrative permissions to update; it may be necessary to click the unlock button and provide the proper credentials before it's possible to change any settings.

### Configuration using Command Line

After installing Wayk Agent on a machine, the *wayk-now* (*wayk-agent* on Linux) command-line becomes available for post-installation automation. The *config* command can be used to read and update the configuration. It's necessary in all cases to pass the `-global` switch to ensure that per-machine settings are overriden; e.g.

To update a setting:

`wayk-now config --global {settingname} {new value}`

To read a setting:

`wayk-now config --global {settingname}`

See [the list of available settings](#configurations).

### Configuration at Install Time

The Wayk Agent installer on Windows can accept configuration information at install time, as .msi parameters. This removes the need for an additional configuration step after installation.

For example:

`msiexec /i WaykAgent-x64-2021.1.0.0.msi CONFIG_AUTO_LAUNCH_ON_USER_LOGON="true" CONFIG_LANGUAGE="fr"`

Will install the Agent and configure WaykAgent.exe to automatically launch on logon, and the user interface to be configured to French.

Beyond [the list of available settings](#configurations), the installer also provides some additional install-time options:

| MSI Parameter Name       | Description | Example |
| :------------------------| :---------: | :-----: |
| INSTALLDESKTOPSHORTCUT | Clear this property to prevent the desktop shortcut from being created | `INSTALLDESKTOPSHORTCUT=""` |
| INSTALLSTARTMENUSHORTCUT | Clear this property to prevent the Start menu shortcut from being created | `INSTALLSTARTMENUSHORTCUT=""` |
| WAYK_ADMIN_PASS | If provided, the installer will create a local *wayk-user* account with the given password, suitable for connecting to the machine using the SRD authentication type | `WAYK_ADMIN_PASS="SecurePassword123!"` |
| SUPPRESSLAUNCH | Clear this property to automatically launch WaykAgent.exe once installation is complete | `SUPPRESSLAUNCH=""` |
| ENROLL_TOKEN_ID | Provide an enrollment token ID to automatically register the machine for unattended access. This must be used in conjunction with `ENROLL_DEN_URL`. | `ENROLL_TOKEN_ID="4203e0a8-525d-4769-b37a-1b3aea8e7b10"` |
| ENROLL_DEN_URL | Provide the URL of the Wayk Bastion server to register the machine with for unattended access. This must be used in conjunction with `ENROLL_TOKEN_ID` | `ENROLL_DEN_URL="https://bastion.ad.it-help.ninja"` |
| BRANDING_FILE | The path to a white label archive, to preconfigure the installation with custom branding. The path should be absolute. | `BRANDING_FILE="\\Server2\Share\Wayk\branding.zip"` |

## Configurations

### Access Control

Possible values are:

**1** Allowed (*Default*)

**2** Confirm

**4** Disabled

| Setting Name | MSI Name | Description |
| :----------- | :------- | :---------: |
| AccessControl.Viewing | CONFIG_ACCESS_CONTROL_VIEWING | Whether the client can see the Agent desktop |
| AccessControl.Interact | CONFIG_ACCESS_CONTROL_INTERACT | Whether the client can control the Agent desktop |
| AccessControl.Clipboard | CONFIG_ACCESS_CONTROL_CLIPBOARD | Whether the client can share the Agent clipboard |
| AccessControl.FileTransfer | CONFIG_ACCESS_CONTROL_FILE_TRANSFER | Whether the client can transfer files to and from the Agent |
| AccessControl.Exec | CONFIG_ACCESS_CONTROL_EXEC | Whether the client can execute scripts and programs on the Agent |
| AccessControl.Chat | CONFIG_ACCESS_CONTROL_CHAT | Whether the client can initiate a chat session with the Agent |

### Security

| Setting Name | MSI Name | Description | Values |
| :----------- | :------- | :---------: | -----: |
| AllowNoPassword | CONFIG_ALLOW_NO_PASSWORD | Allow the "Prompt for Permission" (passwordless) authentication type | `true` (*default*), `false` |
| AllowPersonalPassword | CONFIG_ALLOW_PERSONAL_PASSWORD | Allow the "Secure Remote Password" (SRP) authentication type | `true` (*default*), `false` |
| AllowSystemAuth | CONFIG_ALLOW_SYSTEM_AUTH | Allow the "Secure Remote Delegation" (SRD) authentication type. It is not recommended to disable this setting. | `true` (*default*), `false` |
| GeneratedPasswordAutoReset | CONFIG_GENERATED_PASSWORD_AUTO_RESET | Automatically reset the generated SRP password after it has been used | `true` (*default*), `false` |
| GeneratedPasswordCharSet | CONFIG_GENERATED_PASSWORD_CHAR_SET | The character set to use when generating SRP passwords. | `0` (numeric), `1` (alphanumeric) (*default*) |
| GeneratedPasswordLength | CONFIG_GENERATED_PASSWORD_LENGTH | The length (in characters) of generated SRP passwords. | Default is 6|

### User Interface

| Setting Name | MSI Name | Description | Values |
| :----------- | :------- | :---------: | -----: |
| AutoLaunchOnUserLogon | CONFIG_AUTO_LAUNCH_ON_USER_LOGON | Automatically launch the Wayk Agent application on user logon. Windows only. | `true`, `false` (*default*) |
| FriendlyName | CONFIG_FRIENDLY_NAME | The friendly name of the Agent for use in chat sessions and PFP authentication | Default is the machine network name |
| Language | CONFIG_LANGUAGE | The language of the user interface | Language code. Default is `en` (English) |
| MinimizeToNotificationArea | CONFIG_MINIMIZE_TO_NOTIFICATION_AREA | Minimize the Wayk Agent application to the system tray instead of the task bar or dock | `true`, `false` (*default*) |
| ShowMainWindowOnLaunch | CONFIG_SHOW_MAIN_WINDOW_ON_LAUNCH | Show the Wayk Agent main window when the application is launched | `true` (*default*), `false` |

### Miscellaneous

| Setting Name | MSI Name | Description | Values |
| :----------- | :------- | :---------: | -----: |
| AnalyticsEnabled | CONFIG_ANALYTICS_ENABLED | Report anonymous usage information to Devolutions | `true` (*default*), `false` |
| AutoUpdateEnabled |  CONFIG_AUTO_UPDATE_ENABLED| Automatically keep the application updated | `true` (*default*), `false` |
| ChatLogEnabled | | Log a history of all chat conversations | `true` (*default*), `false` |
| CrashReporterAutoUpload | CONFIG_CRASH_REPORTER_AUTO_UPLOAD | Automatically upload crash reports to Devolutions. Requires the crash reporter to be enabled. Windows only. | `true` (*default*), `false` |
| CrashReporterEnabled | CONFIG_CRASH_REPORTER_ENABLED | Automatically capture diagnostic information about application failures. Windows only. | `true` (*default*), `false` |
| DenUrl | CONFIG_DEN_URL | The Wayk Bastion URL to connect to. | Default is `wss://den.wayk.net`. |
| DxgiCaptureEnabled | | Use hardware accelerated screen capture. Windows only. | `true` (*default*), `false` |
| LoggingLevel | CONFIG_LOGGING_LEVEL | The diagnostic level to use for recording log messages | `0` (TRACE) to `5` (FATAL). `6` is OFF (no logging) |
| LoggingFilter | CONFIG_LOGGING_FILTER | A runtime filter for log messages | |
| PublishUniqueId | CONFIG_PUBLISH_UNIQUE_ID | Publish the Agent unique ID with the wayk.link bookmarking service | `true` (*default*), `false` |
| UpdateCheckInterval | | The duration between automated update checks | Duration in seconds between `3600` and `604800`. Default is `86400` (Daily) |
| UpdateRetryInterval | | The duration to wait after a failed update check to try again | Duration in seconds between `300` and `3600`. Default is `900` (15 minutes) |
