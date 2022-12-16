The template uses [FAKE](https://fake.build/) to build the application.

Generated FAKE script contains a number of useful build targets:

## **"Run"** target
```powershell
dotnet fake build --target run
```

This target is used for development purposes, and provides a great live-reload experience. It pulls down any dependencies required for both the client and server, before running both the client and server in a "watch" mode, so any changes you make on either side will be automatically applied without you needing to restart the application.

> Navigating to `http://localhost:8080/` will load the application.

## **"Bundle"** target
```powershell
dotnet fake build
```

> As Bundle is the default target, you do not need to supply any arguments to FAKE.

This target is used to both build and package up your application in a production fashion, ready for deployment. It will restore all dependencies and build both the client and server in a production and release mode respectively, and correctly copy the outputs into the `deploy` folder in the root of the application. Once your build has completed, you can launch the entire application locally to test it as follows:

```powershell
cd deploy
Server
```

> Navigating to `http://localhost:8085/` will load the application.

## **"Azure"** target
```powershell
dotnet fake build --target azure
```

This target will deploy your application to Azure with a fully configured Application Insights instance. **You do not need to pre-create any resources in Azure** - the template will create everything needed, using free SKUs so you can test without any costs.

> You must already have an Azure account and will be prompted to log into it during the deployment process.

This build step uses both the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) and [Farmer](https://compositionalit.github.io/farmer/) projects to create all resources in just a few lines of code.

> The name of resources will be generated based on the folder in which you created the application. These may be incompatible with Azure naming rules, or may already be in use (Azure web applications must be globally unique) so you may have to modify the name of the webapp to pick one that is acceptable.

## **"RunTests"** target
```powershell
dotnet fake build --target runtests
```

This target behaves similarly to the standard Run target, except that it launches the unit tests for both client and server.

* The server tests will run immediately in the console, using watch mode to allow you to rapidly iterate on your tests.
* The client tests run *in the browser*. Again, they use a watch mode so you can make changes to your client code and see the results in the browser.

> Launch the client tests on `http://localhost:8081/`