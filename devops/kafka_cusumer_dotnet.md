# Consuming messages on a kafka server

these last days i had a problem with my dotnet kafka consumer using Mediator to call services :

````---> System.InvalidOperationException: Cannot resolve 'MediatR.IRequestHandler`2[OneXperience.Application.Employees.CreateEmployee.CreateEmployeeCommand,System.Guid]' from root provider because it requires scoped service 'OneXperience.Infrastructure.Repositories.Employees.IWriteEmployeeRepository'.````

i stopped investigating when i understood the problem looks like a not normal behavior and found this issue  :

````https://github.com/jbogard/MediatR/issues/465````

confirming that the problem was strange.

in my case, when using the Environment variable ``ASPNETCORE_ENVIRONMENT`` :

````
- name: ASPNETCORE_ENVIRONMENT
value: Development
````

i had this error but changing this value to anything else caused the error, finally i ended in changing the value to ``Dev`` and sending a mail to matt.krebs waiting for his answer.

## compiling with dotnet

### set the current default sdk version (to run with)

````bat
C:\git\xperience\xperience-onexperience-api\OneXperience\API\OneXperience.API>dotnet new global.json --sdk-version 5.0.408
Getting ready...
Creating this template will make changes to existing files:
  Overwrite   ./global.json

Rerun the command and pass --force to accept and create.

C:\git\xperience\xperience-onexperience-api\OneXperience\API\OneXperience.API>dotnet --version
5.0.408

C:\git\xperience\xperience-onexperience-api\OneXperience\API\OneXperience.API>

C:\git\xperience\xperience-onexperience-api\OneXperience\API\OneXperience.API>type global.json
{
  "sdk": {
    "version": "5.0.408"
  }
}

````

### build using sln file

````bat
dotnet build "OneXperience.sln" -c Release -o /app/build
dotnet publish "OneXperience.sln" -c Release -o /app/publish
````

to not build all projects customize in visual studio (for exemple the release build in this case)


