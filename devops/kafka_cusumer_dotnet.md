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

