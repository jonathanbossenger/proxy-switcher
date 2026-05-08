proxy-switcher
==============

A Gnome Shell Extension to switch the proxy mode between the pre-defined modes "none", "manual" and "automatic". The extension adds a button with dropdown to select the proxy mode to the Quick Menu like so:

![Screenshot](screenshot.png)

The gnome extensions page is [here](https://extensions.gnome.org/extension/771/proxy-switcher/). Install using the [extensions website](https://extensions.gnome.org/extension/771/proxy-switcher/) or alternatively follow the manual installation instructions below.

Any contributions are very welcome (e.g. new features, translations, bug fixes etc) and I will consider all feature requests. Please submit an issue/pull request or email me at `tomflannaghan@gmail.com`.

## Installation

I recommend using the gnome extensions site but this is not always up to date. To get the latest version, do

    git clone https://github.com/tomflannaghan/proxy-switcher.git
    cd proxy-switcher
    make build
    make install

## Older Gnome versions

Current master branch only supports versions >= 45. There have been breaking changes to the Gnome Shell API. The best way to download the appropriate version for your Gnome is via the [extensions website](https://extensions.gnome.org/extension/771/proxy-switcher/), where
you can select the shell version you would like.

There are branches for some older versions of Gnome, e.g. `gnome44` branch for Gnome 44.

## Shell Command Execution

The extension supports executing custom shell commands when switching between proxy modes. This allows you to automate tasks that should happen when your proxy configuration changes.

### Configuration

Configure commands using `gsettings`:

```bash
# Command to execute when proxy is disabled (none mode)
gsettings set org.gnome.shell.extensions.com-flannaghan-ProxySwitcher command-none 'your-command-here'

# Command to execute when switching to manual proxy
gsettings set org.gnome.shell.extensions.com-flannaghan-ProxySwitcher command-manual 'your-command-here'

# Command to execute when switching to automatic proxy
gsettings set org.gnome.shell.extensions.com-flannaghan-ProxySwitcher command-auto 'your-command-here'
```

### Example Use Cases

**Log proxy changes:**
```bash
gsettings set org.gnome.shell.extensions.com-flannaghan-ProxySwitcher command-none 'echo "$(date): Proxy disabled" >> ~/.proxy-changes.log'
```

**Send notifications:**
```bash
gsettings set org.gnome.shell.extensions.com-flannaghan-ProxySwitcher command-auto 'notify-send "Proxy" "Automatic proxy enabled"'
```

**Restart services:**
```bash
gsettings set org.gnome.shell.extensions.com-flannaghan-ProxySwitcher command-manual 'systemctl --user restart my-vpn-service'
```

**Run custom scripts:**
```bash
gsettings set org.gnome.shell.extensions.com-flannaghan-ProxySwitcher command-none '/home/user/scripts/proxy-disabled.sh'
```

### Notes

- Commands are executed asynchronously and will not block the proxy switching operation
- If a command fails, an error will be logged but will not prevent the proxy mode from changing
- Commands are only executed if configured (non-empty strings)
- Leave a command empty to disable execution for that mode

## Translations

I have added the translations I found in the [`gnome-control-center`](https://git.gnome.org/browse/gnome-control-center) project to the extension (these are the translations used in the "Network Settings" menu). I've also used the "Network Settings" desktop shortcut to translate that phrase.
