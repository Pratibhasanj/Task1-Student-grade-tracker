# Task1-Student-grade-tracker
import java.util.ArrayList;
import java.util.Scanner;

public class Task1 
{
    public static void main(String[] args) 
    {
        ArrayList<String> grades = new ArrayList<>();
        Scanner scanner = new Scanner(System.in);
        
        while (true) 
        {
            System.out.println("\n1. Enter grades");
            System.out.println("2. Display results");
            System.out.println("3. View all grades");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            
            int choice = scanner.nextInt();
            scanner.nextLine(); 
            
            switch (choice) 
            {
                case 1:
                    inputGrades(grades, scanner);
                    break;
                case 2:
                    if (!grades.isEmpty())
                    {
                        displayResults(grades);
                    } 
                    else 
                    {
                        System.out.println("No grades entered yet.");
                    }
                    break;
                case 3:
                    displayAllGrades(grades);
                    break;
                case 4:
                    System.out.println("Exiting program. Goodbye!");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }

    public static void inputGrades(ArrayList<String> grades, Scanner scanner)
    {
        while (true) 
        {
            System.out.print("Enter a grade (A, B, C, D, F, or Z to finish): ");
            String grade = scanner.nextLine().toUpperCase();
            
            if (grade.equals("Z"))  
            {
                break;
            }
            
            if (grade.matches("[ABCDF]")) 
            {
                grades.add(grade);
            } 
            else 
            {
                System.out.println("Invalid grade. Please enter A, B, C, D, or F.");
            }
        }
    }

    public static void displayResults(ArrayList<String> grades) 
    {
        int sum = 0;
        String highest = grades.get(0);
        String lowest = grades.get(0);
        
        for (String grade : grades) 
        {
            sum += gradeToPoints(grade);
            if (gradeToPoints(grade) > gradeToPoints(highest)) 
            {
                highest = grade;
            }
            if (gradeToPoints(grade) < gradeToPoints(lowest)) 
            {
                lowest = grade;
            }
        }
        
        double average = (double) sum / grades.size();
        
        System.out.printf("Average score: %.2f\n", average);
        System.out.println("Highest grade: " + highest);
        System.out.println("Lowest grade: " + lowest);
    }

    public static int gradeToPoints(String grade)
    {
        switch (grade) 
        {
            case "A": return 4;
            case "B": return 3;
            case "C": return 2;
            case "D": return 1;
            case "F": return 0;
            default: return -1;
        }
    }

    public static void displayAllGrades(ArrayList<String> grades) 
    {
        if (grades.isEmpty()) 
        {
            System.out.println("No grades entered yet.");
        } else 
        {
            System.out.println("\nAll Grades:");
            for (int i = 0; i < grades.size(); i++) 
            {
                System.out.println("Student " + (i + 1) + ": " + grades.get(i));
            }
        }
    }
}
