## Clean code rules

Here are six "clean code" rules, and explanations for each of them: 

I] Meaningful names :

Rule: Choose variable, function and class names that are descriptive and meaningful. 
Avoid short or obscure names.

Explanation: Clear, explicit names make the code easier to understand, which in turn makes it more readable and maintainable.

```
using System;

namespace MyApplication
{
  class Program
  {
    static bool check(Int i) 
    {
        if (i % 2 == 0)
        {
            return true;
        }
        return false;
    }

    static void Main(string[] args)
    {
        //... Code not shown - ignore this line
    }  
  }
}
```

For this code extract, the most relevant of the six 'clean code' rules would be the significant name rule. 
The name of the check function could be more descriptive to clearly reflect its purpose. 
For example, by using isEven, the name becomes more explicit, which improves the readability and understanding of the code without requiring any additional comments.

II] Short functions :

Rule: Functions should be short and do just one thing. 
Ideally, they should be no longer than a few lines.

Explanation: Short functions are easier to understand and test. They encourage code reuse and make bugs easier to spot.

In this extract, the Register and Login methods are relatively short and don't do much, which is good practice in itself. 
However, it is always possible to go further in breaking down the functions to make them even shorter and more focused. 
This approach can make the code easier to understand and maintain.

```
public void Register(string username, string password)
{
  var salt = CreateSalt();
  var hashedPassword = HashPassword(password, salt);
  SaveToDatabase(username, hashedPassword, salt);
}

public bool Login(string username, string password)
{
  var user = GetUserFromDatabase(username);
  var hashedPassword = HashPassword(password, user.Salt);
  return IsPasswordValid(user.HashedPassword, hashedPassword);
}

private string CreateSalt()
{
  // Logique de cr�ation du sel
}

private string HashPassword(string password, string salt)
{
  // Logique de hachage du mot de passe
}

private bool IsPasswordValid(string savedHashedPassword, string inputHashedPassword)
{
  return savedHashedPassword == inputHashedPassword;
}

private User GetUserFromDatabase(string username)
{
  // Logique de r�cup�ration de l'utilisateur depuis la base de donn�es
}

private void SaveToDatabase(string username, string hashedPassword, string salt)
{
  // Logique de sauvegarde des donn�es dans la base de donn�es
}
```

Here is a modified version to illustrate this:

```
public void Register(string username, string password)
{
  var salt = CreateSalt();
  var hashedPassword = HashPassword(password, salt);
  SaveToDatabase(username, hashedPassword, salt);
}

public bool Login(string username, string password)
{
  var user = GetUserFromDatabase(username);
  var hashedPassword = HashPassword(password, user.Salt);
  return IsPasswordValid(user.HashedPassword, hashedPassword);
}

private string CreateSalt()
{
  // Logique de cr�ation du sel
}

private string HashPassword(string password, string salt)
{
  // Logique de hachage du mot de passe
}

private bool IsPasswordValid(string savedHashedPassword, string inputHashedPassword)
{
  return savedHashedPassword == inputHashedPassword;
}

private User GetUserFromDatabase(string username)
{
  // Logique de r�cup�ration de l'utilisateur depuis la base de donn�es
}

private void SaveToDatabase(string username, string hashedPassword, string salt)
{
  // Logique de sauvegarde des donn�es dans la base de donn�es
}
```

By breaking down the functions further, each function now has a very specific task, which makes them shorter and easier to understand, in line with the rule of short functions.

III] Relevant comments :

Rule: Use comments to explain the why, not the how. 
Comments should provide useful information, not just repeat code.

Explanation: Relevant comments help developers to understand the context and logic behind the code, which is particularly useful for subsequent maintenance.

IV] Avoid duplicating code:

Rule: Don't duplicate code. Identify repeated parts and abstract them into reusable functions or classes.

Explanation: Duplicating code makes the source code more difficult to maintain, as changes have to be made in several places. 
By avoiding duplication, you reduce potential errors.

V] Separation of concerns :

Rule: Each component (function, class, module) should focus on a single task or concern. 
Avoid components that do too many things.

Explanation: Separating concerns makes code easier to understand, maintain and reuse. 
Each component has a clear purpose.

```
class Car
{
  public string carModel;

  // Constructeur de la classe
  public Car()
  {
    carModel = "Mustang"; // D�finir la valeur initiale pour carModel
  }

  static void Main(string[] args)
  {
    Car Ford = new Car();
    Console.WriteLine(Ford.carModel);
  }
}
```

For this code extract, another relevant rule among the six "clean code" rules would be the separation of concerns rule. 
In this extract, the Car class manages both the class definition and the display of a specific car model.

It would be preferable to separate these concerns by using a separate method to display the car model. 
Here is a modified version that respects this rule:

```
class Car
{
  public string model;

  public Car()
  {
    model = "Mustang";
  }

  public void DisplayModel()
  {
    Console.WriteLine(model);
  }

  static void Main(string[] args)
  {
    Car Ford = new Car();
    Ford.DisplayModel();
  }
}
```

With this modification, the Car class now focuses on the definition of the class itself, while the DisplayModel function manages the display of the car model. 
This separates the concerns and makes the code more modular and easier to understand.

VI] Unit testing :

Rule: Write unit tests for each function or method. The tests should be automated and able to detect bugs.

Explanation: Unit tests ensure that your code works properly and continues to do so when changes are made. 
They improve confidence in the code.
By following these "clean code" rules, you can make your code more readable, maintainable and robust. 
Each of these rules contributes to the overall quality of your code and makes it easier to collaborate with other developers.