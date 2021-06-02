<img src="DynamicQuery/Images/DynamicSelect.jpg" width="200" height="160">

# DynamicSelect

DynamicSelect is a library aimed at allowing developers to easily shape thier data at run time by specifying the
fields that they want. It would then automatically perform the neccessary joins for you through `EntityFramework Core`.

# Example

```cs
    public static class DynamicSelectExample
    {
        public static void Run()
        {
            SeedDbContext seedDbContext = SeedDbContext.Create();

            
            dynamic result = seedDbContext.Persons.ProjectToDynamic(
                "Id", "Gender", "MyName.Name", "Departments[Name]", "Departments[Sections[Name]]"
                );

            string json = JsonConvert.SerializeObject(result, Formatting.Indented);

            Console.WriteLine(json);
        }
    }
```

# Result

```json
[
  {
    "Id": 1,
    "Gender": "F",
    "MyName": {
      "Name": "Jane Doe"
    },
    "Departments": [
      {
        "Name": "IT",
        "Sections": [
          {
            "Name": "IT-A"
          },
          {
            "Name": "IT-B"
          }
        ]
      },
      {
        "Name": "HR",
        "Sections": [
          {
            "Name": "HR-A"
          },
          {
            "Name": "HR-B"
          },
          {
            "Name": "HR-C"
          }
        ]
      }
    ]
  }]
```
