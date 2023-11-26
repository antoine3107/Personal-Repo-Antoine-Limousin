# Task Summary - Resource Management for UNDAC in C# - Week 12.

In this task, as the support and logistics manager for the UNDAC team, I developed a solution in C# to facilitate the request of specialist staff from partner agencies. 

## Summary

Here's a summary of the key points:


<b>Data Model:</b>

A PersonnelRequest class was created to encapsulate the details of a request, including skills required, number of staff required, start and end dates, and approval date.

<b>Request List Management:</b>

A list was used to store multiple staffing requests, allowing efficient management of all requests within the system.

<b>Displaying Requests:</b>

A DisplayPersonnelRequests method has been implemented to clearly display the details of each request, including the approval date if the request has been approved.

<b>Approval simulation:</b>

An ApproveRequest method has been created to simulate the approval process for a personnel request, updating the approval date in the PersonnelRequest class.

<b>Flexibility and extensibility:</b>

The code provided provides a flexible and extensible basis for managing multiple requests, and can be adapted to incorporate additional functionality, such as data persistence, integration with other parts of the system, etc.
This summary highlights how the C# solution meets the requirements of the task, providing a structured and modular way of managing specialist staff requests to ensure the successful operation of the UNDAC team.

## Code snippets - good software design practice

<b>Using Classes for Abstraction :</b>

```
class PersonnelRequest
{
    // Properties and methods encapsulating the details of a personnel request
}
```

A PersonnelRequest class is created to encapsulate the details of a personnel request, following the principle of abstraction.

<b>Explicit and Significant Variable Names</b>

```
DateTime confirmationDate = DateTime.Now.AddDays(1);
```

The name of the confirmationDate variable is self-explanatory, clearly indicating its purpose.

<b>Using Methods to Encapsulate Logic :</b>

```
public void MarkAsApproved(DateTime confirmationDate)
{
    ApprovalDate = confirmationDate;
    // Other logic encapsulated here
}
```

The approval logic is encapsulated in a MarkAsApproved method, making the code easier to read and reuse.

<b>Using Self-implementing Properties :</b>

```
public DateTime? ApprovalDate { get; private set; }
```

Auto-implemented properties are used, simplifying the syntax while maintaining readability.

<b>Relevant Comments:</b>

```
// Simulation of an approved response
DateTime confirmationDate = DateTime.Now.AddDays(1);
```

Comments are used to explain the purpose of certain parts of the code, improving understanding.

<b>Structured Organisation of the Code :</b>

```
static void DisplayPersonnelRequests(List<PersonnelRequest> requests)
{
    // Display logic organised in a separate method
}
```

The display logic is organised in a separate method, making it easier to maintain and understand.

<b>Consistent Variable Name Management :</b>

```
foreach (var request in requests)
```

The iteration variable is given a concise name (request), but is explicit enough to understand its role.

## Test code descriptive summary.

To test the program, I was able to use test frameworks such as NUnit, MSTest and Xunit. 


This NUnit test code includes two tests:

<b>MarkAsApproved_ShouldSetApprovalDate:</b>
Checks that the call to the MarkAsApproved method sets the approval date (ApprovalDate) to non-null.

<b>MarkAsApproved_ShouldSetCorrectApprovalDate :</b>
Checks that the call to the MarkAsApproved method sets the approval date (ApprovalDate) to the date provided.


Here is an example of simple test code using NUnit to test the PersonnelRequest class:

```
using NUnit.Framework;
using System;

[TestFixture]
public class PersonnelRequestTests
{
    [Test]
    public void MarkAsApproved_ShouldSetApprovalDate()
    {
        // Arrange
        PersonnelRequest request = new PersonnelRequest();

        // Act
        request.MarkAsApproved(DateTime.Now);

        // Assert
        Assert.IsNotNull(request.ApprovalDate);
    }

    [Test]
    public void MarkAsApproved_ShouldSetCorrectApprovalDate()
    {
        // Arrange
        PersonnelRequest request = new PersonnelRequest();
        DateTime approvalDate = DateTime.Now;

        // Act
        request.MarkAsApproved(approvalDate);

        // Assert
        Assert.AreEqual(approvalDate, request.ApprovalDate);
    }
}
```

## Code review.

Here's a summary of the positive aspects I identified and the changes suggested to me by the person who produced my code review: 

<b>File "Data/Database.cs"</b>

Positive Aspects:
Good use of asynchronous programming for database initialization.
Appropriate exception handling for database initialization errors.

Suggestions:
The InitializeDatabaseAsync method could be marked as private since it's not intended to be used outside of the class.
Maybe uncomment the CreateTablesAsync method with proper table creation code.


<b>File "Data/DatabaseSettings.cs"</b>

Positive Aspects:
Clear and concise settings for the database.

Suggestions:
Ensure that Path and FileSystem are properly imported


<b>File "PersonnelRequestManager.cs"</b>

Positive Aspects:
Well-structured and easy to understand console application.
Good use of class and method encapsulation.

Suggestions:
Ensure that Console.ReadLine(); is not used to keep the console open indefinitely. It's a good practice to use Console.ReadKey(); instead.


<b>UndacBlue.csproj</b>

Positive Aspects:
Multi-targeting setup for different platforms.
Proper handling of target frameworks.

Suggestions:
Consider organizing the ItemGroup elements more consistently.


______________________________________________________________________________


Here are some areas for improvement in the code I reviewed this week: 

<b>1. "Views/RoomPage.xaml.cs" file</b>

a. Use of async void : 
Avoid using async void except in event handlers. 
Instead, use async Task for asynchronous methods, as async void can cause error handling problems.

b. Dependency injection : 
Rather than instantiating BaseService<Room> directly in your constructor, consider using dependency injection. 
This will make the code more testable and flexible.

c. List data source assignment redundancy: 
The RoomListView.ItemsSource data source is assigned twice, once in the constructor and once in LoadRooms(). 
This can be simplified by doing it once in the constructor.

d. Code repetition : 
The logic for loading rooms (LoadRooms()) is repeated in several places. 
This logic could be grouped together to avoid redundancy.

e. Method naming: 
The names of methods such as OnSaveButtonClicked and OnDeleteButtonClicked are good, but it might have been possible to rename them to reflect their purpose more clearly, for example SaveRoom and DeleteRoom.

f. Error handling: 
Add appropriate error handling, such as error messages or logging, to inform the user of potential problems.

g. User interface consideration: 
Consider adding visual feedback, such as confirmation or error messages, to improve the user experience.


<b>2. "Models/Room.cs" file</b>

a. Handling validation errors : 
Use the [Required] attribute to indicate that RoomName cannot be null. 
Also ensure that validation errors are managed, particularly when creating or updating the Room object. 
Use the validation mechanisms provided by ASP.NET Core to do this.

b. XML documentation : 
Add XML comments to document the class and its members, in particular to explain the use of RoomName and any other properties in the context of your application.

c. Encapsulation and automatic read-only properties: 
If possible, consider making properties read-only and use automatic read-only properties ({ get; }) to ensure better encapsulation. 
For example, if BaseEntity contains properties that should not be modified after the object has been created, they could be defined as read-only.


<b>3. "Views/RoomPage.xaml" file</b>

a. Spacing attributes (Spacing, Margin) : 
The spacing values (Spacing and Margin) are currently hard-coded (Spacing="10" and Margin="5"). 
Consider defining these values in resource files or constants for more centralised management.

b. Using resources : 
Use resources to define colours, fonts, dimensions, etc. centrally. 
This makes maintenance and appearance changes easier.

c. Using styles: 
If there are several pages with a similar style, consider creating a style for these page elements and reusing them.

d. Calling event methods: 
Clicked and ItemSelected events currently call specific methods in the code-behind. 
Consider binding these events to controls in your view model to improve separation of concerns.


## Conclusion

This concludes the Software Engineering module. 
I imagine I'll have the opportunity to talk about it in the Interview, but here's my personal assessment: 

First of all, a bit of context. As an international student, I had chosen to study 3 subjects in particular for my semester here. 
Unfortunately, one of the 3 subjects I had selected was dropped at the last minute, and we were forced to take the 'Software Engineering' module. 
Despite my disappointment, I was pleased with the professionalism of the two teachers of this module (Mr. Davison and Mr. Bamgboye), as well as the fact that I was able to learn a new programming language (C#), so I told myself that I would continue studying this module.

I still had a lot of difficulties in this module throughout the semester. 
Unlike most of the students in the class, not knowing how to program in C# handicapped me a lot, especially during the group project period. 
But at least I learned about good working practices as a developer, and I realised that here, code quality is 200% more important than quantity. 
What's more, I was able to understand how a software development environment works in all its aspects, and also learn how to work in a group made up of many people. 

These last two points had an effect especially after making the decision to join the Blue team at the end of the module, something I am proud of. 

Thanks again to Mr. Davison and Mr. Bamgboye for learning all these new concepts and for accompanying us in the best way during this module.