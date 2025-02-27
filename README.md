# COSC 3380 Team 4 Project - Theme Park

This is the group project by Team 4 of COSC 3380, Fall 2022 semester at the University of Houston.

# App Dependencies

The app can be built on Windows, macOS (both Intel and Apple Silicon), or Linux. In each case, you will need:

* [Microsoft .NET 6 with ASP.NET Core Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) This is included in Visual Studio and Visual Studio for Mac, but Visual Studio is not required to build the app. The SDK installer bundles the ASP.NET Core Runtime and is preferred.

# Database Installation

## Platform options

The database used for this project was Microsoft SQL Server 2019 Developer Edition, as packaged for Docker Engine for running on Ubuntu Linux hosts. However, any other available deployment of SQL Server 2019 Developer Edition will work.

Regardless of platform, the machine or VM guest which is hosting SQL server requires at least 2 GB of RAM.

## Windows

Microsoft provides a free installer for the Windows version of SQL Server 2019 Developer Edition [here](https://www.microsoft.com/en-IN/sql-server/sql-server-downloads). TEST THIS

## Linux (bare-metal)

For bare-metal installations on Linux, Microsoft provides documentation for Red Hat Enterprise Linux (RHEL) 7.3, Ubuntu Linux 16.04, and SUSE Linux Enterprise Server (SLES) v12 SP.

## Docker

The easiest (in my experience) way to deploy is using Docker Engine. Besides the typical Docker Engine on Linux, Docker for Windows also works. Although we have not tested it, Docker for Mac will work on Intel Macs, but Microsoft SQL Server does not support Apple Silicon Macs.

* Install Docker Engine, Docker for Windows, or Docker for Mac
* Verify that Docker is running and that it has been allocated at least 2 GB of RAM
* In a terminal or command prompt, run `docker pull mcr.microsoft.com/mssql/server:2019-latest` to fetch the latest updated version of SQL Server 2019.
* Run `docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=yourStrong(!)Password" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest` to quickly create a new container running Microsoft SQL Server 2019 MAYBE ELABORATE?

Further documentation regarding running Microsoft SQL Server 2019 on Docker can be found on [DockerHub](https://hub.docker.com/_/microsoft-mssql-server)

# Database Deployment

The included BACPAC file includes a full database dump. Before using the app, it will be necessary to restore the database schema and data from the dump.

The easiest means to do this is using Microsoft's SqlPackage.exe utility. ELABORATE

# Configuration

The app is configured to connect to the database using a configuration read from `db.json`. This file is not included in the repository for security reasons, but a copy of `db.json` relevant to our Docker-based deployment is included in the project submission. For usage of a different SQL database server, the file must be modified appropriately with the hostname, username, and password appropriate to that database.

For debug testing on localhost, the app configuration here is sufficient; however, for production deployment using Docker it was necessary to modify Kestrel's configuration to accept an external SSL certificate and key in order for HTTPS hosting to be successful. For the sake of completion, the requisite files have been included in the project submission.

# Building and testing the app

For localhost testing, it is possible to build and run the app from the command line, or through Visual Studio:

## Command-line

From the root directory of the repository, in the terminal enter:

* `dotnet build`
* `dotnet run --project cosc3380-group4-themepark`

This will fetch the NuGet library dependencies, build the app, and start a Kestrel server hosting the app locally at `localhost:7035`.

## Visual Studio

* Open the `cosc3380-group4-themepark.sln` file from the root directory in Visual Studio
* From the menu, ...
* Build and run the application using the menu

The server should start automatically and a new browser tab will open to `localhost:7035`.