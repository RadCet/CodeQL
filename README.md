# CodeQL
## Install as VS code plugin (the full official doc in https://help.semmle.com/codeql/how-does-codeql-work.html)
 - Install VS code (of course)
 - Install CodeQL plugin (https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-codeql)
 - Download CodeQL CLI (https://github.com/github/codeql-cli-binaries/releases/latest/download/codeql.zip)
 - Extract codeql.zip then check if codeql CLI run normally ```codeql resolve languages```
 - Config CodeQL:CLI Executable path or add to $PATH variable
 - Recommend using starter workspace from CodeQL by clone https://github.com/github/vscode-codeql-starter/ 
 - You can create ur own workspace by adding CodeQL libraries and queries to existing workspace
## Create database
 - Get in your root folder of your project
 - Cmd: ```codeql database create <database-folder> --language=<cpp/python/go/java..>```
## First query
 - Add database by using command palette > CodeQL:Choose Database or using UI in CodeQL tab in sidebar
 - Add your query (.ql) in workspace and run using command palette or right click and choose run query
 
