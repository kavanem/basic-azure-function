Notes on getting Azure functions running locally through vscode:
- Setup local.settings.json file with the following contents locally

```
{
  "IsEncrypted": false,
  "Values": {    
    "AzureWebJobsStorage": "UseDevelopmentStorage=true"
  }
}
```


- Install Azurite extension
- Setup launch.json

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [        
        {
            "name": ".NET Core Attach",
            "type": "coreclr",
            "request": "attach"
        },
        {
            "name": "Attach to .NET Functions",
            "type": "coreclr",
            "request": "attach",
            "processId": "${command:azureFunctions.pickProcess}"
        }
    ]
}
```

- Setup tasks.json

```
{
	"version": "2.0.0",
	"tasks": [
		{
			"label": "clean (functions)",
			"command": "dotnet",
			"args": [
				"clean",
				"/property:GenerateFullPaths=true",
				"/consoleloggerparameters:NoSummary"
			],
			"type": "process",
			"problemMatcher": "$msCompile",
			"options": {
				"cwd": "${workspaceFolder}/aspnet-core/usgcamdatabaseconverter"
			}
		},
		{
			"label": "build (functions)",
			"command": "dotnet",
			"args": [
				"build",
				"/property:GenerateFullPaths=true",
				"/consoleloggerparameters:NoSummary"
			],
			"type": "process",
			"problemMatcher": "$msCompile",
			"options": {
				"cwd": "${workspaceFolder}/aspnet-core/usgcamdatabaseconverter"
			}
		}		
	]
}
```

- Run Azurite through the command pallet ctrl+alt+P
- Run task `Attach to .NET Functions` through the debug pane OR run `func host start`
