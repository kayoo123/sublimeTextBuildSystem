# sublimeTextBuildSystem

I'm sharing this project in order to group together build scripts for carrying out various tasks


## GitURLToClipboard

This first script copies the current project file to a clipboard and opens it in the browser.

#### 1. Create a PowerShell script : 

> C:\PATH\TO\SCRIPT\git_url_to_clipboard.ps1

```ps1
# Retrieve the URL from the git repository and convert it to HTTPS
$url = git config --get remote.origin.url
$httpsUrl = $url -replace 'git@([^:]*):(.*).git', 'https://$1/$2'

# Copy the transformed URL to the clipboard
$httpsUrl | Set-Clipboard

# Open the URL in the default browser
Start-Process $httpsUrl
```

#### 2. Create a Build System : 

`Tools` > `Build System` > `New Build System...`

> GitURLToClipboard.sublime-build

```json
{
    "cmd": ["powershell", "-ExecutionPolicy", "Bypass", "-File", "C:\\PATH\\TO\\SCRIPT\\git_url_to_clipboard.ps1"],
    "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
    "working_dir": "$file_path",
    "selector": "source.shell"
}
```

#### 3. Usage 

- Select :  `Tools` > `Build System` > `GitURLToClipboard`
- Press : `Ctrl + B` on any open file !
