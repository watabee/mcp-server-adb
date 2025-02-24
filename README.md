# ADB MCP Server

MCP Server for Android Debug Bridge (ADB), enabling Claude to interact with Android devices.

## Tools

1. `get-devices`
   * List connected Android devices
   * Optional inputs:
     * `showDetails` (boolean, default: true): Show device details (-l)
   * Returns: List of connected devices with their details

2. `list-packages`
   * List installed packages on the device
   * Optional inputs:
     * `showPath` (boolean, default: false): Show the APK file path (-f)
     * `showDisabled` (boolean, default: false): Show only disabled packages (-d)
     * `showEnabled` (boolean, default: false): Show only enabled packages (-e)
     * `showSystem` (boolean, default: false): Show only system packages (-s)
     * `showThirdParty` (boolean, default: false): Show only third party packages (-3)
     * `showInstaller` (boolean, default: false): Show package installer (-i)
     * `includeUninstalled` (boolean, default: false): Include uninstalled packages (-u)
   * Returns: List of packages based on specified filters

3. `input-text`
   * Input text to the device
   * Required inputs:
     * `text` (string): Text to input
   * Returns: Text input confirmation

4. `install-apk`
   * Install an APK file to the device
   * Required inputs:
     * `apkPath` (string): Path to the APK file
   * Optional inputs:
     * `allowReinstall` (boolean, default: true): Allow reinstalling (-r)
     * `allowTestPackages` (boolean, default: true): Allow test packages (-t)
     * `allowDowngrade` (boolean, default: true): Allow downgrade (-d)
     * `grantPermissions` (boolean, default: false): Grant all permissions (-g)
   * Returns: Installation result

5. `uninstall-apk`
   * Uninstall an application
   * Required inputs:
     * `packageName` (string): Package name to uninstall
   * Optional inputs:
     * `keepData` (boolean, default: false): Keep app data and cache (-k)
   * Returns: Uninstallation result

6. `clear-app-data`
   * Clear application data
   * Required inputs:
     * `packageName` (string): Package name to clear data
   * Returns: Operation result

7. `pull`
   * Pull a file from device
   * Required inputs:
     * `remotePath` (string): Path to file on device
   * Optional inputs:
     * `localPath` (string): Local destination path
   * Returns: File transfer result

8. `push`
   * Push a file to device
   * Required inputs:
     * `localPath` (string): Path to local file
     * `remotePath` (string): Destination path on device
   * Returns: File transfer result

9. `screencap`
   * Take a screenshot
   * Required inputs:
     * `remotePath` (string): Path on device where to save the screenshot (e.g., /sdcard/screenshot.png)
   * Optional inputs:
     * `usePng` (boolean, default: true): Save as PNG (-p)
   * Returns: Screenshot capture result

10. `rm`
    * Remove a file from the Android device
    * Required inputs:
      * `path` (string): Path to the file on device to remove
    * Optional inputs:
      * `force` (boolean, default: false): Force removal (-f)
      * `recursive` (boolean, default: false): Recursive removal (-r)
    * Returns: File removal result

11. `reset-permissions`
    * Reset all permissions for an app
    * Required inputs:
      * `packageName` (string): Target package name
    * Returns: Permission reset result

12. `grant-permission`
    * Grant a specific permission
    * Required inputs:
      * `packageName` (string): Target package name
      * `permission` (string): Permission to grant
    * Returns: Permission grant result

13. `revoke-permission`
    * Revoke a specific permission
    * Required inputs:
      * `packageName` (string): Target package name
      * `permission` (string): Permission to revoke
    * Returns: Permission revocation result

14. `start-activity`
    * Start an activity using am start
    * Optional inputs:
      * `component` (string): Component name
      * `action` (string): Intent action
      * `data` (string): Intent data URI
      * `mimeType` (string): MIME type
      * `category` (string[]): Intent categories
      * `extras` (array): Intent extras
      * `flags` (string[]): Intent flags
      * `waitForLaunch` (boolean, default: false): Wait for launch (-W)
      * `debuggable` (boolean, default: false): Debug mode (-D)
      * `stopApp` (boolean, default: false): Force stop app (-S)
    * Returns: Activity start result

All tools support these device selection parameters:
* `deviceId` (string, optional): Target specific device by ID
* `useUsb` (boolean, default: false): Target USB device (-d)
* `useEmulator` (boolean, default: false): Target emulator (-e)

## Setup

1. Install ADB:
   * Download Android SDK Platform Tools
   * Add ADB to your system PATH
   * Verify installation with `adb version`

2. Enable USB Debugging:
   * On Android device, go to Settings > About phone
   * Tap Build number 7 times to enable Developer options
   * Enable USB debugging in Developer options

### Install the Server

```:shell
# Clone the repository
git clone [repository-url]
cd mcp-server-adb

# Install dependencies
npm install

# Build the project
npm run build
```

### Usage with Claude Desktop

Add the following to your `claude_desktop_config.json`:

```:json
{
  "mcpServers": {
    "adb": {
      "command": "node",
      "args": [
        "-y",
        "/path/to/mcp-server-adb/build/index.js",
        "/path/to/adb"
      ]
    }
  }
}
```

Replace /path/to/adb with the actual path to your ADB executable.

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.
