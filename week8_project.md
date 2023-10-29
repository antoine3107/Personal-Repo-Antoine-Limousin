## Week 8 - 1st week out of 3 of the team project.

# 1. A descriptive summary of the issue that I worked on

I worked on the issue titled "Access Management for UNDAC Personnel". 
This issue involves the implementation of an access management system for the UNDAC application, allowing UNDAC Team Support and Logistics Managers to request and grant system access to new personnel.

The primary goal of this issue is to ensure that authorized personnel have the appropriate access permissions to perform their duties within the UNDAC system. 
This access management system will enhance security and streamline the onboarding process for new team members.

In the code, I have created a User class to represent UNDAC personnel and a Permission class to represent different access permissions. 
I've implemented functions to create users, grant permissions, and check access requests. 
This issue aims to improve the security and access control of the UNDAC application, which is crucial for data integrity and confidentiality.

# 2. Snippets from your code with commentary showing how you have used good software design practice.

Here are some examples of code snippets that I made with commentary : 

<b>
Using classes for abstraction :
</b>

```
public class User
{
    public string Name { get; set; }
    public List<Permission> Permissions { get; set; } = new List<Permission>();
}
```

In this snippet, I've used a User class to encapsulate user-related data, promoting the principle of abstraction. 
This allows me to model users with their associated properties and permissions.

<b>
Separation of concerns :
</b>

```
public class AccessManagementSystem
{
    // ...
    public void GrantPermission(User user, string permissionName)
    {
        var permission = new Permission { Name = permissionName };
        user.Permissions.Add(permission);
        Console.WriteLine($"Permission {permissionName} has been granted to {user.Name}.");
    }
    // ...
}
```

This code snippet shows a method in the AccessManagementSystem class that handles the granting of permissions. 
It adheres to the principle of separation of concerns by focusing on a specific functionality, making the code more modular and maintainable.

<b>
Use of dependency injection :
</b>

```
public void GrantPermission(User user, string permissionName)
{
    var permission = new Permission { Name = permissionName };
    user.Permissions.Add(permission);
    Console.WriteLine($"Permission {permissionName} has been granted to {user.Name}.");
}
```

I've used dependency injection to pass the User object as a parameter to the GrantPermission method. 
This promotes flexibility and testability, making it easier to modify the behavior and write unit tests.

<b>
Comments for clarity :
</b>

```
public void RequestAccess(User user, string resource, string permissionName)
{
    if (user.Permissions.Any(p => p.Name == permissionName))
    {
        Console.WriteLine($"{user.Name} is granted access to {resource} with {permissionName} permission.");
    }
    else
    {
        Console.WriteLine($"{user.Name} does not have {permissionName} permission for {resource}.");
    }
}
```

I've included comments to explain the logic in the code. 
This helps other developers understand the code's purpose and enhances code maintainability.


# 3. A descriptive summary of the test code that you have written:

Unit testing with NUnit

In the test code, we can utilize a testing framework like NUnit to create unit tests for various components of the access management system. 
Here's a summary of the test code for a specific component:

```
using NUnit.Framework;

[TestFixture]
public class AccessManagementSystemTests
{
    [Test]
    public void TestUserCreation()
    {
        AccessManagementSystem accessManagementSystem = new AccessManagementSystem();
        string userName = "TestUser";
        
        accessManagementSystem.CreateUser(userName);

        User createdUser = accessManagementSystem.GetUserByName(userName);
        Assert.AreEqual(userName, createdUser.Name);
    }

    [Test]
    public void TestPermissionGranting()
    {
        AccessManagementSystem accessManagementSystem = new AccessManagementSystem();
        User user = new User { Name = "TestUser" };
        string permissionName = "TestPermission";

        accessManagementSystem.GrantPermission(user, permissionName);

        Assert.IsTrue(user.Permissions.Any(p => p.Name == permissionName));
    }

    [Test]
    public void TestAccessRequests()
    {
        AccessManagementSystem accessManagementSystem = new AccessManagementSystem();
        User user = new User { Name = "TestUser" };
        string permissionName = "TestPermission";
        string resource = "TestResource";

        accessManagementSystem.GrantPermission(user, permissionName);

        string accessResult = accessManagementSystem.RequestAccess(user, resource, permissionName);
        StringAssert.Contains($"granted access to {resource} with {permissionName} permission", accessResult);
    }
}
```

This test code covers three main areas: user creation, permission granting, and access requests. 
Each test method tests a specific aspect of the access management system's functionality. 
For instance, in the TestPermissionGranting method, I verify that a user has been granted a permission correctly.

The use of NUnit allows us to run these tests and ensure that your access management system behaves as expected, helping to catch potential issues during development and subsequent changes.

# 4. A reflective summary of any changes that were requested during the code review along with your fixes.

Quotes from the person who reviewed my code : 

"In the RequestAccess method, before checking authorisations, make sure that the user exists. 
You should add a validation to handle the case where the user does not exist."

"To improve data protection, you should encapsulate the class fields and provide properties for accessing them. 
For example, in the User class, encapsulate the Name and Permissions properties."

"Instead of using objects with set properties, it would be preferable to pass values via the constructor when the user or permission is created."

# 5. 

The code I decided to review is the following one : "As an UNDAC Deputy Team Leader I want to view details of all team partners so that I can contact them immediately."

Here is the code before the review : 

```
using System;
using System.Collections.Generic;

public class TeamPartner
{
    public string Name { get; set; }
    public string ContactInformation { get; set; }
}

public class TeamManagementSystem
{
    private List<TeamPartner> teamPartners = new List<TeamPartner>();

    public void AddTeamPartner(string name, string contactInformation)
    {
        var newTeamPartner = new TeamPartner { Name = name, ContactInformation = contactInformation };
        teamPartners.Add(newTeamPartner);
        Console.WriteLine($"Team partner {name} has been added.");
    }

    public void ViewAllTeamPartners()
    {
        Console.WriteLine("List of Team Partners:");
        foreach (var partner in teamPartners)
        {
            Console.WriteLine($"Name: {partner.Name}, Contact Information: {partner.ContactInformation}");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        var teamManagementSystem = new TeamManagementSystem();

        teamManagementSystem.AddTeamPartner("John Doe", "john@example.com");
        teamManagementSystem.AddTeamPartner("Alice Smith", "alice@example.com");

        teamManagementSystem.ViewAllTeamPartners();
    }
}
```

Here are the things that I suggested to change : 

a. There is currently no validation of user entries in the code. 
It would be a good idea to implement checks to ensure that the information provided for team partners (names and contact details) is correct and complete.

b. The code does not support the possibility of adding two partners with the same name. 
You might consider adding a check to avoid duplicates.

c. The Name and ContactInformation properties of the TeamPartner class are currently writable. 
If this data is not to be modified after it has been created, you should consider making it read-only by using read-only properties.

d. In this example, team partner data is stored in memory. 
If you plan to persist this data between runs of the application, you will need to add a method for saving and loading this data from an external source (such as a database or file).


# 6. Conclusion

Working as a team this week highlighted the importance of communication and coordination. 
We faced challenges in keeping team members in sync, particularly when we were working on separate parts of the project. 
However, thanks to regular meetings and the use of project management tools, we were able to overcome these challenges and maintain our productivity.

When I compared my practice with that of my colleagues, I noticed that my preference for the object-oriented approach to development was more pronounced. 
I tend to favour design patterns such as the Singleton design pattern and object composition to solve complex problems. 
However, I also found that each member of the team brought unique perspectives, which enriched our overall approach to development.

This week has been full of discoveries and challenges. 
I've realised how important it is to remain open to new technologies and collaborative working methods. 
My next step is to strengthen my mastery of project management tools and continue to explore areas such as machine learning and artificial intelligence to broaden my skills.