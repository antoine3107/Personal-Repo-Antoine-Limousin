# Week 11 - 2nd week as blue team member.

## Introduction.

This week marked my 2nd week in the Blue Team. 
Last week we had set up our entire workspace to get off to a good start.

This week we each had to select one of the 'issues' for week 3. 
Personally, I chose to tackle the task "As a system administrator, I want to maintain reference values for skills", as I felt comfortable doing this task specifically.


## The completion of the task.

Here are the steps I followed to complete this task: 


1. Create a "Skill.cs" class in the "Models" folder to model each person's skills, which allows skill-related data to be organised and manipulated in a more structured way.

```
public class Skill
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

2. Create an "AppDbContext.cs" class in the context of an application using the Entity Framework Core, which is an ORM (Object-Relational Mapping) for .NET. 
The main purpose of the AppDbContext class is to represent the database context in which entities (such as the Skill class) will be persisted.

```
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public DbSet<Skill> Skills { get; set; }

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        // Configure your database connection here
        // optionsBuilder.UseSqlServer("YourConnectionString");
    }
}
```

3. Implement the main part of the "skill" functionality, in a new "Services" folder, which corresponds to the "SkillService.cs" file.
The "SkillService" class has been created to encapsulate the business logic linked to skills and to provide an interface between the manipulation of Skill entities and the rest of the application.

```
using Microsoft.EntityFrameworkCore;
using System.Collections.Generic;
using System.Linq;

public class SkillService
{
    private readonly AppDbContext _dbContext;

    public SkillService(AppDbContext dbContext)
    {
        _dbContext = dbContext;
    }

    public List<Skill> GetAllSkills()
    {
        return _dbContext.Skills.ToList();
    }

    public Skill GetSkillById(int skillId)
    {
        return _dbContext.Skills.Find(skillId);
    }

    public void AddSkill(Skill skill)
    {
        _dbContext.Skills.Add(skill);
        _dbContext.SaveChanges();
    }

    public void UpdateSkill(Skill skill)
    {
        _dbContext.Entry(skill).State = EntityState.Modified;
        _dbContext.SaveChanges();
    }

    public void DeleteSkill(int skillId)
    {
        var skill = _dbContext.Skills.Find(skillId);
        if (skill != null)
        {
            _dbContext.Skills.Remove(skill);
            _dbContext.SaveChanges();
        }
    }
}
```

4. Add the new services to the .NET MAUI application, in the code-behind the "MainPage.xaml" page.

```
using Microsoft.Maui.Controls;

public partial class MainPage : ContentPage
{
    private readonly SkillService _skillService;

    public MainPage()
    {
        InitializeComponent();
        _skillService = new SkillService(new AppDbContext());
    }

    // Utilisez les méthodes du service ici pour effectuer les opérations CRUD
    // Exemple : _skillService.AddSkill(new Skill { Name = "Programming" });
}
```

## Difficulties encountered.

1. I encountered error CS1061 because the compiler could not find a definition for the SaveChanges method in the AppDbContext class, and no accessible SaveChanges extension method accepting a first argument of type AppDbContext was found.

This error probably occurs because the compiler cannot resolve the SaveChanges method in the current context. 
To solve this problem, I checked the following points:

I've ensured that I've imported the correct namespace (using Microsoft.EntityFrameworkCore;) at the top of the file where I'm using AppDbContext.
I've confirmed that my AppDbContext class does indeed derive from DbContext, because that's where the SaveChanges method is found.
I took care to use the correct instance of AppDbContext in my SkillService. 
If I created a new instance, I made sure I used the same instance to load and save the data.
I checked which version of Entity Framework Core I was using. 
If I'm using an older or newer version, I've made sure that the code is compatible with the version in question, as newer versions can introduce changes to the API.


2. I have encountered error CS0051 due to an accessibility inconsistency: the parameter type 'Class1.Skill' is less accessible than the method 'SkillService.UpdateSkill(Class1.Skill)'.

This error generally occurs when the accessibility level of the Skill class or type used as a parameter for the UpdateSkill method in the SkillService class is more restricted than the accessibility level of the method itself.
Here's how I solved the problem:

I checked the accessibility level of the Skill class in the Class1 source file. 
If the Skill class is declared with a specific access modifier such as private or internal, this may cause an inconsistency with the UpdateSkill method, which may have a wider accessibility level.
To resolve this error, I have adjusted the accessibility level of the Skill class in the Class1 source file so that it is at least as accessible as the UpdateSkill method in the SkillService class. 
This may involve changing the access modifier of the class to public or an equivalent level of accessibility.

## Code review.

For this week I've reviewed Josh's code. 
His task was: "As a system administrator, I want to maintain reference values for rota types". 

His work was very rich in content and very complete. 
The construction of his code across the different elements of the project was successful. 


Here are the main comments I made during my code review: 

<b>1. RotaPage.xaml" file</b>

a. Using styles to make the code more readable and reusable would have been relevant. 
Styles can be defined for buttons, the editor, etc. An example that could have been done : 

```
<ContentPage.Resources>
    <ResourceDictionary>
        <Style x:Key="ButtonStyle" TargetType="Button">
            <Setter Property="TextColor" Value="White" />
            <!-- Autres propriétés de style -->
        </Style>
    </ResourceDictionary>
</ContentPage.Resources>

<!-- Utilisation du style pour les boutons -->
<Button Text="Save" Clicked="OnSaveButtonClicked" Style="{StaticResource ButtonStyle}" />
<Button Grid.Column="1" Text="Delete" Clicked="OnDeleteButtonClicked" Style="{StaticResource ButtonStyle}" />
```

b. Instead of manipulating clicked events, commands could be used. 
Commands provide a cleaner separation between the user interface logic and the underlying logic.

```
<Button Text="Save" Command="{Binding SaveCommand}" Style="{StaticResource ButtonStyle}" />
<Button Grid.Column="1" Text="Delete" Command="{Binding DeleteCommand}" Style="{StaticResource ButtonStyle}" />
```


<b>2. RotaPage.xaml.cs" file</b>

a. Rather than instantiating RotaService directly in the constructor, inject dependencies to make the class more testable and to allow different services to be injected.
This can be particularly useful for unit tests.

```
public RotaPage(IRotaService rotaService)
{
    InitializeComponent();
    BindingContext = new Rota();
    this._rotaService = rotaService ?? throw new ArgumentNullException(nameof(rotaService));

    Task.Run(async () => await LoadRotas());
    RotaNameEditor.Text = "";
}
```

b. Add appropriate exception handling in the code, particularly around asynchronous operations such as LoadRotas and DeleteRota.
This ensures that the application is more robust.

c. Use Binded Properties in XAML instead of accessing controls directly in the code-behind.
This is more in line with the MVVM model.

```
<Editor x:Name="RotaNameEditor" Placeholder="Add a Rota" HeightRequest="100" Text="{Binding Name, Mode=TwoWay}" />
```

<b>3. Rota.cs" file</b>

a. Continue to use the XML documentation to comment out the code. 
Add comments to explain the purpose of each property and method, and to describe the overall operation of the Rota class. 
This will make it easier for other developers to understand the code.

b. The ID property already has appropriate SQLite annotations. 
However, adding a comment to explain that it is the primary key and that it is auto-incremented would have been relevant.

```
/// <summary>
/// Gets or sets the unique identifier for the Rota. This is the primary key and is auto-incremented.
/// </summary>
[PrimaryKey, AutoIncrement]
public int ID { get; set; }
```

c. In the SetProperty method, add a validation to ensure that the propertyName parameter is not null before calling OnPropertyChanged. 
This can help avoid potential errors.

```
protected bool SetProperty<T>(ref T storage, T value, [CallerMemberName] string propertyName = null)
{
    if (propertyName == null)
    {
        throw new ArgumentNullException(nameof(propertyName));
    }

    if (EqualityComparer<T>.Default.Equals(storage, value))
    {
        return false;
    }

    storage = value;
    OnPropertyChanged(propertyName);
    return true;
}
```

d. In some cases, such as for the Name property, consider using auto-implemented properties to simplify the code, unless you don't need the event triggering logic in the setter.

```
public string Name { get; set; }
```

## Conclusion

I'm proud of my work and I have a much better understanding of how .NET MAUI applications are developed in C#. 
I'm also happy to see that everyone works well in this blue team and that communication is good.



