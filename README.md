# sublimeTextBuildSystem

I'm sharing this project in order to group together build scripts for carrying out various tasks


## GitURLToClipboard

#### 1. Create a PowerShell script : `git_url_to_clipboard.ps1`
```ps1
# Récupérer l'URL du dépôt git et la transformer en HTTPS
$url = git config --get remote.origin.url
$httpsUrl = $url -replace 'git@([^:]*):(.*).git', 'https://$1/$2'

# Copier l'URL transformée dans le presse-papiers
$httpsUrl | Set-Clipboard

# Ouvrir l'URL dans le navigateur par défaut
Start-Process $httpsUrl
```

#### 2. Create a Build System : `GitURLToClipboard.sublime-build`

 `Tools` > `Build System` > `New Build System...`
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
