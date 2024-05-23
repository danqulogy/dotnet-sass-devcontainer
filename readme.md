### Running the containers

```
cd .\docker\
docker compose up
```

This command will start up the services that are described in the ```docker-compose``` file. Namely a SQL Server instance, and he developer environment that we configured with .NET Core and Entity Framework 

#### Interacting with the dev-env
```
docker exec -it dev-env /bin/bash

<!-- Check environment works as expected -->

dotnet –-version
dotnet-ef --version

```


#### Interacting with the sqlserver
```
docker exec -it sqlserver /bin/bash


/opt/mssql-tools/bin/sqlcmd -S localhost -U SA

<!-- when prompted, enter the password from the sqlserver.env file (Password1) -->

```


### Configuring deb containers in VSCode
Install the extension ```Remote Containers```

This will allow us to open an instance of VSCode that makes use of the Docker containers that we have set up previously. This will require a
little bit of additional configuration, but once set up, it will “just work” for the remainder of the project!

- Start by creating a folder called ```.devcontainer``` in the project root

```
.devcontainer
```

This is where VSCode will look to get the configuration.

- Add ```devcontainer.json``` in the ```.devcontainer``` folder


```
{
    "name": "SaaS Book",
    "dockerComposeFile": ["../docker/docker-compose.yaml"],
    "service": "dev-env",
    "workspaceFolder": "/workspace",
    "customizations": {
        "vscode": {
            "extensions": [
                "ms-dotnettools.csharp",
                "shardulm94.trailing-spaces",
                "mikestead.dotenv",
                "fernandoescolar.vscode-solution-explorer",
                "jmrog.vscode-nuget-package-manager",
                "patcx.vscode-nuget-gallery",
                "pkief.material-icon-theme",
                "ms-mssql.mssql",
                "humao.rest-client",
                "rangav.vscode-thunder-client",
                "formulahendry.dotnet-test-explorer",
                "kevin-chatham.aspnetcorerazor-html-cssclass-completion",
                "syncfusioninc.blazor-vscode-extensions",
                "ms-dotnettools.vscode-dotnet-runtime",
                "ms-dotnettools.blazorwasm-companion"
            ]
        }
    },
    "remoteUser": "root"
}
```