# CSCI 1250 – File I/O Lab: Student Grade Tracker

## Introduction
This lab expands on the basic file I/O concepts introduced in the Data Lab (Part 6). You'll create a program that manages student grades using file operations, building on your knowledge of lists, methods, and string manipulation.

---

## Learning Objectives
By the end of this lab, you will be able to:
- Read data from CSV files using `File.ReadAllLines()`
- Parse CSV data using `.Split()`
- Append data to files using `File.AppendAllText()`
- Create backup copies of files using `File.Copy()`
- Write formatted text to files using `StreamWriter`

---

## Part 0: Setup

1. Create a new C# **console project**, using **".Net"** (not ".Net Framework"). Use **.NET version 8** or higher.
2. In your project directory (where your `.csproj` file is located), create a text file named **`students.csv`**.
3. Add the following content to `students.csv`:

```
Alice Johnson,85,92,88
Bob Smith,78,85,91
Charlie Davis,95,88,93
Diana Martinez,82,79,86
```

**Format:** Each line represents: `Name,Quiz1,Quiz2,Quiz3`

---

## Part 1: Reading and Displaying Student Data

Create a method called `DisplayAllStudents` that reads the CSV file and displays each student's information with their calculated average.

### Your Task:

1. Create a `static void` method named `DisplayAllStudents()` with no parameters.
2. Use `File.ReadAllLines("students.csv")` to read the file into a string array.
3. Use a `foreach` loop to process each line.
4. For each line:
   - Use `.Split(',')` to separate the data
   - Parse the three quiz grades as integers
   - Calculate the average of the three quizzes
   - Display the student's name, individual quiz grades, and average

**Starter Code:**

```csharp
static void DisplayAllStudents()
{
    string[] lines = File.ReadAllLines("students.csv");
    
    Console.WriteLine("=== Current Student Data ===");
    
    foreach (string line in lines)
    {
        // TODO: Split the line by commas
        string[] parts = line.Split(',');
        
        // TODO: Extract name and parse the three quiz grades as integers
        string name = parts[0];
        
        // TODO: Calculate the average (remember to use 3.0 for double division)
        
        // TODO: Display formatted output
        // Example: Alice Johnson: Quiz1=85, Quiz2=92, Quiz3=88, Average=88.33
    }
}
```

**Call this method from your `Main()` method and test it.**

**Expected Output:**
```
=== Current Student Data ===
Alice Johnson: Quiz1=85, Quiz2=92, Quiz3=88, Average=88.33
Bob Smith: Quiz1=78, Quiz2=85, Quiz3=91, Average=84.67
Charlie Davis: Quiz1=95, Quiz2=88, Quiz3=93, Average=92.00
Diana Martinez: Quiz1=82, Quiz2=79, Quiz3=86, Average=82.33
```

---

## Part 2: Adding New Students to the File

Create a method called `AddNewStudent` that prompts the user for a new student's information and **appends** it to the CSV file.

### Your Task:

1. Create a `static void` method named `AddNewStudent()` with no parameters.
2. Prompt the user to enter the student's name and three quiz grades.
3. Format the data as a CSV line: `Name,Quiz1,Quiz2,Quiz3`
4. Use `File.AppendAllText()` to add the new line to the file.
5. Display a confirmation message.

**Starter Code:**

```csharp
static void AddNewStudent()
{
    Console.WriteLine("\n=== Add New Student ===");
    
    // TODO: Prompt for student name
    Console.Write("Enter student name: ");
    string name = Console.ReadLine();
    
    // TODO: Prompt for Quiz 1 grade
    Console.Write("Enter Quiz 1 grade: ");
    string quiz1 = Console.ReadLine();
    
    // TODO: Prompt for Quiz 2 grade
    
    // TODO: Prompt for Quiz 3 grade
    
    // TODO: Create the CSV line (format: name,quiz1,quiz2,quiz3)
    // Don't forget to add "\n" at the beginning so it goes on a new line!
    string newLine = $"\n{name},{quiz1},{quiz2},{quiz3}";
    
    // TODO: Use File.AppendAllText() to add the line to students.csv
    
    Console.WriteLine("Student added successfully!");
}
```

**Test your method:**
1. Call `AddNewStudent()` from `Main()`
2. Add a student (e.g., "Eve Wilson" with grades 90, 87, 94)
3. Call `DisplayAllStudents()` again to verify the student was added

---

## Part 3: Creating a Backup File

Create a method called `CreateBackup` that creates a backup copy of the students file.

### Your Task:

1. Create a `static void` method named `CreateBackup()` with no parameters.
2. Use `File.Copy()` to create a backup file named `students_backup.csv`.
3. Display a success message.

**Starter Code:**

```csharp
static void CreateBackup()
{
    // TODO: Use File.Copy() to copy students.csv to students_backup.csv
    // Hint: File.Copy(source, destination, overwrite);
    // Set overwrite to true so you can create multiple backups
    
    Console.WriteLine("\nBackup created: students_backup.csv");
}
```

**Test your method** by calling it from `Main()` and checking that `students_backup.csv` was created in your project directory.

---

## Part 4: Finding the Highest and Lowest Averages

Create a method called `FindExtremeAverages` that determines which student has the highest and lowest quiz average.

### Your Task:

1. Create a `static void` method named `FindExtremeAverages()` with no parameters.
2. Read all lines from `students.csv`.
3. Loop through each student and calculate their average.
4. Track the highest and lowest averages along with the student names.
5. Display the results.

**Starter Code:**

```csharp
static void FindExtremeAverages()
{
    string[] lines = File.ReadAllLines("students.csv");
    
    string highestStudent = "";
    double highestAverage = 0.0;
    string lowestStudent = "";
    double lowestAverage = 100.0;
    
    foreach (string line in lines)
    {
        // TODO: Split the line and parse the data
        string[] parts = line.Split(',');
        string name = parts[0];
        
        // TODO: Calculate the average for this student
        
        // TODO: Check if this is the highest average so far
        // Hint: if (average > highestAverage) { ... }
        
        // TODO: Check if this is the lowest average so far
        // Hint: if (average < lowestAverage) { ... }
    }
    
    Console.WriteLine($"\nHighest Average: {highestStudent} with {highestAverage:F2}");
    Console.WriteLine($"Lowest Average: {lowestStudent} with {lowestAverage:F2}");
}
```

**Test your method** by calling it from `Main()` after `DisplayAllStudents()`.

---

## Part 5: Writing a Formatted Report with StreamWriter

Create a method called `GenerateReport` that uses `StreamWriter` to create a nicely formatted report file.

### Your Task:

1. Create a `static void` method named `GenerateReport()` with no parameters.
2. Use `StreamWriter` to create a new file called `report.txt`.
3. Write a formatted header.
4. For each student, write their name, quiz grades, and average.
5. Write a footer with the report generation timestamp.

**Starter Code:**

```csharp
static void GenerateReport()
{
    string[] lines = File.ReadAllLines("students.csv");
    
    using (StreamWriter writer = new StreamWriter("report.txt"))
    {
        // Write header
        writer.WriteLine("==========================================");
        writer.WriteLine("        STUDENT GRADE REPORT");
        writer.WriteLine("==========================================");
        writer.WriteLine();
        
        // TODO: Loop through each student
        foreach (string line in lines)
        {
            // TODO: Split and parse the data
            string[] parts = line.Split(',');
            string name = parts[0];
            int quiz1 = int.Parse(parts[1]);
            
            // TODO: Parse quiz2 and quiz3
            
            // TODO: Calculate average
            
            // TODO: Write student information using writer.WriteLine()
            // Example format:
            writer.WriteLine($"Student: {name}");
            writer.WriteLine($"  Quiz 1: {quiz1}");
            // Write Quiz 2 and Quiz 3
            // Write Average
            writer.WriteLine(); // Blank line between students
        }
        
        writer.WriteLine("==========================================");
        writer.WriteLine($"Report generated on: {DateTime.Now}");
    }
    
    Console.WriteLine("\nReport written to report.txt");
}
```

**Test your method** by calling it from `Main()` and opening `report.txt` to view the formatted report.

---

## Your Main Method

In your `Main()` method, call all of your methods in a logical order to demonstrate all functionality:

```csharp
static void Main(string[] args)
{
    Console.WriteLine("=== Student Grade Management System ===\n");
    
    // Display initial data
    DisplayAllStudents();
    FindExtremeAverages();
    
    // Create backup before making changes
    CreateBackup();
    
    // Add a new student
    AddNewStudent();
    
    // Display updated data
    Console.WriteLine("\n--- After Adding New Student ---");
    DisplayAllStudents();
    FindExtremeAverages();
    
    // Generate report
    GenerateReport();
    
    Console.WriteLine("\n=== Program Complete ===");
    Console.WriteLine("Check your project folder for students_backup.csv and report.txt");
}
```

---

## Testing Checklist

Make sure your program does the following:

- [ ] Displays all students with their quiz grades and averages
- [ ] Creates a backup file (students_backup.csv)
- [ ] Adds a new student when prompted
- [ ] Displays updated information after adding the student
- [ ] Identifies the student with the highest average
- [ ] Identifies the student with the lowest average
- [ ] Generates a formatted report (report.txt) using StreamWriter

---

## Submission

Zip up all of your code. Be sure to include the following:
* All **`.cs`** files
* **`students.csv`** (with your test data including the added student)
* **`students_backup.csv`** (the backup file your program created)
* **`report.txt`** (the report your program generated)
* All **`.csproj`** files
* Any **`.sln`** files if your editor generated one or more for you

Submit your zipped file to the dropbox.

**If D2L rejects your submission**, you can delete the folders **"obj"** and **"bin"**. They are unnecessary.

---

## Summary of File I/O Methods Used

In this lab, you practiced:

| Method | Purpose | Example |
|--------|---------|---------|
| `File.ReadAllLines()` | Read entire file into string array | `string[] lines = File.ReadAllLines("file.csv");` |
| `File.AppendAllText()` | Add text to end of file | `File.AppendAllText("file.csv", "\nNew line");` |
| `File.Copy()` | Create a copy of a file | `File.Copy("source.csv", "backup.csv", true);` |
| `StreamWriter` | Write formatted text to files | `using (StreamWriter writer = new StreamWriter("file.txt"))` |
| `.Split(',')` | Parse CSV data | `string[] parts = line.Split(',');` |

These file I/O skills are essential for creating programs that save and load data!

---

*Adapted from ETSU CSCI 1250 curriculum*
