# Project work - week 9.

## a. A descriptive summary of the issue that I worked on

The task is to develop functionality to enable UNDAC team members to record operational information after a mission. 
This information is essential for the management of the team, as it will serve as a basis for planning and prioritising future actions. 
The aim is to capture relevant details of the mission, such as observations, challenges encountered, resources used, and any other information deemed crucial for subsequent analysis. 
In summary, this functionality aims to improve the collection and documentation of post-mission operational information for more informed decisions within the UNDAC team.

## b. Snippets from my code with commentary showing how I have used good software design practice.

<b>
Using classes to group related functionality
</b>

```
public class Mission
{
	[...]
}
```

The Mission and UNDACTeamMember classes are used to group together related functionality. 
This is good software design practice for organising code logically and making it easier to manage functionality.

<b>
Using properties to encapsulate data
</b>

```
    public int MissionId { get; }
    public string MissionName { get; }
    public List<string> OperationalIntelligence { get; }
```

Properties such as MissionId, MissionName, and OperationalIntelligence are used to encapsulate data within classes. 
This means that direct access to the data is limited, promoting consistency and data protection.

<b>
Using methods to perform specific actions
</b>

```
public void AddIntelligence(string intelligenceText)
    {
        OperationalIntelligence.Add(intelligenceText);
    }
```

Methods such as AddIntelligence and RecordIntelligence are used to perform specific actions. 
This promotes code modularity by breaking tasks down into smaller, reusable functions.

<b>
Representation of distinct entities with distinct classes
</b>

In the code snippet, each class represents a distinct entity. 
The Mission class represents an UNDAC mission, while the UNDACTeamMember class represents a member of the UNDAC team. 
This design approach allows real-world entities to be modelled separately and their functionality to be managed independently.

<b>
Use of a Main method to demonstrate the use of classes
</b>

```
 static void Main(string[] args)
    {
        Mission mission1 = new Mission(1, "Mission A");
        UNDACTeamMember teamMember1 = new UNDACTeamMember("John");
        UNDACTeamMember teamMember2 = new UNDACTeamMember("Alice");

        teamMember1.RecordIntelligence(mission1, "Completed assessment of local infrastructure.");
        teamMember2.RecordIntelligence(mission1, "Identified shortages in medical supplies.");

        Console.WriteLine($"Operational Intelligence for {mission1.MissionName}:");
        foreach (string entry in mission1.OperationalIntelligence)
        {
            Console.WriteLine(entry);
        }
    }
```

The Main method is used as the program's entry point. 
It demonstrates how the Mission and UNDACTeamMember classes are used in a concrete application scenario. 
This approach shows how the classes interact in a real-life context, helping to illustrate how they work and how useful they are.

## c. A descriptive summary of the test code that you have written.

<b>
Description of the test objectives
</b>

The aim of the tests is to check that the Mission and UNDACTeamMember classes function correctly in terms of recording and displaying operational intelligence.

<b>
Description of the unit tests
</b>

A unit test was written to check that the AddIntelligence method of the Mission class correctly adds an entry to the operational intelligence list.
Another unit test has been created to ensure that the RecordIntelligence method of the UNDACTeamMember class correctly records the operational intelligence by adding the team member's name to the intelligence text.

<b>
Mentioning assertions
</b>

In the test of the AddIntelligence method, an assertion was used to verify that the size of the operational intelligence list increases after an entry is added.
For the RecordIntelligence method test, an assertion was used to ensure that the recorded intelligence contains the team member's name.

<b>
Description of test execution
</b>

The tests were executed using the xUnit test framework, which enables automated and systematic test execution.

All the tests were run successfully, which means that the Mission and UNDACTeamMember classes work as specified. No errors were reported during test execution.


## d. A reflective summary of any changes that were requested during the code review along with your fixes.

Here are the changes that were suggested to me : 

<b>
Use of classes to group related functionalities
</b>

Fix: Comments describing the use of classes have been added.
Explanation: Comments help developers understand the purpose of classes, which facilitates maintenance and collaboration.

<b>
Use of properties for data encapsulation
</b>

Fix: Added comments to explain the use of properties.
Explanation: Comments help to understand why properties are used, which improves the clarity of the code.

<b>
Use of methods to perform specific actions
</b>

Correction: Comments added to explain why methods are used.
Explanation: The comments explain the purpose of the methods, making the code more understandable.

<b>
Representation of distinct entities with distinct classes
</b>

Correction: No correction necessary, as the representation of entities with distinct classes is correct.

<b>
Use of a Main method to demonstrate the use of classes:
</b>

Correction: Added comments to explain the role of the Main method.
Explanation: The comments help you to understand the reason for using the Main method, which clarifies the purpose of the program's entry point.


## e. A descriptive summary of any issues you found with the code that you were asked to review

Here is the code that I asked to review : 

```
using System;
using System.Collections.Generic;

public class SecurityAlert
{
    public int AlertId { get; }
    public string AlertMessage { get; }
    public DateTime AlertTimestamp { get; }

    public SecurityAlert(int alertId, string alertMessage)
    {
        AlertId = alertId;
        AlertMessage = alertMessage;
        AlertTimestamp = DateTime.Now;
    }
}

public class UNDACTeamLeader
{
    public string Name { get; }
    public List<SecurityAlert> SecurityAlerts { get; }

    public UNDACTeamLeader(string name)
    {
        Name = name;
        SecurityAlerts = new List<SecurityAlert>();
    }

    public void ViewSecurityAlerts()
    {
        Console.WriteLine($"Security Alerts for {Name}:");
        foreach (var alert in SecurityAlerts)
        {
            Console.WriteLine($"Alert ID: {alert.AlertId}, Message: {alert.AlertMessage}, Timestamp: {alert.AlertTimestamp}");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        UNDACTeamLeader teamLeader = new UNDACTeamLeader("Team Leader A");

        teamLeader.SecurityAlerts.Add(new SecurityAlert(1, "Security breach detected at site A."));
        teamLeader.SecurityAlerts.Add(new SecurityAlert(2, "Suspicious activity reported at site B."));

        teamLeader.ViewSecurityAlerts();
    }
}
```

And here are the things that I suggested to correct : 

<b>
Using comments to explain the code
</b>

Comments have been added to explain certain parts of the code, such as the use of classes and methods. 
This makes the code easier to understand for developers reading it.
By adding these comments, the code becomes more explicit and easier to understand for other developers, which facilitates maintenance and collaboration on the project.

<b>
Use of meaningful class and variable names
</b>

Class and variable names are meaningful and reflect their role. 
For example, SecurityAlert, UNDACTeamLeader, AlertId, AlertMessage, AlertTimestamp, Name, and SecurityAlerts are explicit names that make the code easier to understand.

<b>
Indentation and formatting
</b>

The code is correctly indented and formatted, which improves readability. 
Each block of code is indented appropriately, making it easier to distinguish between control structures.

In short, by using comments, meaningful names and appropriate formatting, the code is clearer, more understandable and easier for developers to maintain. 
It also respects coding conventions, which is essential for collaboration within a development team.


## f. Conclusion

<b>
New learning this week :
</b>

This week I gained a better understanding of the importance of communication within a development team. 
I realised that regular meetings to discuss progress, obstacles and priorities can greatly improve collaboration. 
What's more, I learnt new project management techniques, such as backlog management and iteration planning, which help to keep development on track.

<b>
Common problems in team development :
</b>

Among the common problems I've identified in team development, managing code conflicts and differences in coding style can be a challenge. 
Establishing clear coding standards and code review processes is essential to address this issue. 
In addition, uneven distribution of tasks can occur, requiring open communication to ensure that each team member has a balanced workload.

<b>
Comparing my practice to others :
</b>

In comparing my practice to that of other developers, I've found that adopting good software design practices and coding standards is something I hold dear. 
It ensures that the code is clean, readable and maintainable. 
However, I've also realised that I can improve my communication within the team and my time management for greater efficiency.

<b>
Possible improvements :
</b>

To improve, I plan to strengthen my ability to resolve conflicts and facilitate team collaboration. 
I'll also continue to learn about best practice in software development and project management. 
Finally, I'll be looking to expand my technical skills so that I'm more versatile and able to take on a wider variety of tasks within the team.

Ultimately, every week brings new lessons and opportunities for improvement. 
The key is to keep learning, adapting and improving in an ever-changing team development environment.