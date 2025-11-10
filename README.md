File Handling*/
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

class File1{
	public static void main(String args[]) {
	File inf=new File("A:\\jayu\\a.txt\\");
	File outf=new File("A:\\jayu\\b.txt\\");
	
	FileReader ins=null;
	FileWriter outs=null;
	
	try {
		ins=new FileReader(inf);
		outs=new FileWriter(outf);
		
		int ch;
		while((ch=ins.read())!=-1) {
			outs.write(ch);
		}
	}
		catch(IOException e) {
			System.out.println(e);
			System.exit(-1);
		}
	finally {
		try {
			ins.close();
			outs.close();
		}
		catch(IOException e) {}
	}
		System.out.println("File Copied");
	}
} 
/* MATRICS*/
import java.util.Scanner;
public class Matrics{
	
	public static void main(String[] args){
		Scanner S=new Scanner(System.in);
		int row,col;
		System.out.println("Enter no. of rows & columns: ");
		row=S.nextInt();
		col=S.nextInt();
		
		int a[][]=new int[row][col];
		int b[][]=new int[row][col];
		int c[][]=new int[row][col];
		System.out.println("Enter matrix a: ");
		for(int i=0;i<row;i++)
		{
			for(int j=0;j<col;j++)
			{
				a[i][j]=S.nextInt();
			}
		}
		System.out.println("Enter matrix b: ");
		for(int i=0;i<row;i++)
		{
			for(int j=0;j<col;j++)
			{
				b[i][j]=S.nextInt();
			}
		}
		
		for(int i=0;i<row;i++)
		{
			for(int j=0;j<col;j++)
			{
				c[i][j]=a[i][j]+b[i][j];
			}
		}
		System.out.println("Addition is:\t ");
		for(int i=0;i<row;i++)
		{
			for(int j=0;j<col;j++)
			{
				System.out.println(c[i][j]+"\t");
			}
			System.out.println();
		}
	}
/* playerclass*/
import java.util.Scanner;
public class Playerdetail {
	public static void main(String[]args){
		cricket ck=new cricket();
		hockey hk=new hockey();
		football fb=new football();
		Scanner read=new Scanner(System.in);
		int op1,op2;
		while(true)
		{
			System.out.println("1.Enter details 2.Display 3.Exit");
			System.out.println("Enter your option");
			op1=read.nextInt();
			switch(op1)
			{
			case 1:
			System.out.println("1.Football player 2.Hockey player 3.cricket player");
		    System.out.append("Enter your option");
		    op2=read.nextInt();
		    switch(op2)
		    {
		    case 1:
		    	System.out.println("Enter name:");
		    	fb.name=read.next();
		    	System.out.println("Enter skill:");
		    	fb.skill=read.next();
		    	System.out.println("Enter age:");
		    	fb.age=read.nextInt();
		    	break;
		    case 2:
		    	System.out.println("Enter name:");
		    	hk.name=read.next();
		    	System.out.println("Enter skill:");
		        hk.skill=read.next();
		    	System.out.println("Enter age:");
		    	hk.age=read.nextInt();
		    	break;
		    case 3:
		    	System.out.println("Enter name:");
		    	ck.name=read.next();
		    	System.out.println("Enter skill:");
		    	ck.skill=read.next();
		    	System.out.println("Enter age:");
		    	ck.age=read.nextInt();
		    	break;
		    		    	
		    	}
		    break;
			case 2:
				System.out.println("1.Football player 2.Hockey plyer 3.Cricket plyer");
				System.out.append("Enter your option");
				op2=read.nextInt();
				switch(op2)
				{
				case 1:
					System.out.println("Name"+fb.name);
					System.out.println("skill"+fb.skill);
					System.out.println("Age"+fb.age);
					break;
				case 2:
					System.out.println("Name"+hk.name);
					System.out.println("Skill"+hk.skill);
					System.out.println("Age"+hk.age);
					break;
				case 3:
					System.out.println("Name"+ck.name);
					System.out.println("Skill"+ck.skill);
					System.out.println("Age"+ck.age);
					break;
					}
		    break;
			case 3:
				System.exit(0);
				
			}
		}
	}

}
class players
{
	String name;
	int age;
	String skill;
	
}
class football extends players
{
}
class cricket extends players
{
}
class hockey extends players
{
}
/* to sort list of integer*/
import java.util.Arrays;
import java.util.Scanner;
public class SortInt {
	public static void main (String[] args)
	{
		Scanner read=new Scanner(System.in);
		int count,b,temp,c;
		int a[]=new int[10];
		 System.out.println("How many Integers  You want to enter ?");
		 count=read.nextInt();
		 for(b=0;b<count;b++)
		 {
			 System.out.println("Enter values");
			 temp=read.nextInt();
			 a[b]=temp;
		 }
		 System.out.println("The array before sorting:");
		 for(b=0;b<count;b++){
			 System.out.println(a[b]+" ");
		 }
		 System.out.println("The araay after sort:");
		 for(b=0;b<count;b++)
		 {
			 for(c=0;c<count-b-1;c++)
			 {
				 if(a[c]>a[c+1]){
					 temp=a[c];
					 a[c]=a[c+1];
					 a[c+1]=temp;
				 }
		 }
	}
	for(b=0;b<count;b++)
	{
		System.out.println(a[b]+" ");
	}
	
			 }
		 
	}
/* to sort list of names*/
import java.util.Scanner;
public class SortName {
	public static void main (String[] args) 
	{
		int i,j,n;
		Scanner ip=new Scanner(System.in);
		System.out.println("How many string You want to Enter?");
		n=ip.nextInt();
		String name[]=new String[n+1];
		System.out.println("Enter sting:");
		for(i=0;i<n;i++)
			name[i]=ip.next();
		for(i=0;i<n;i++)
		{
			for(j=i+1;j<n;j++)
			{
				if(name [i].trim().compareTo(name[j].trim())>0)
				{
					String temp=name[i];
					name[i]=name[j];
					name[j]=temp;
				}
			}
		}
		System.out.println("Sorted list is: ");
		for(i=0;i<n;i++)
			System.out.println(" "+name[i]);
	}
}
/* method overloading*/
package SapJava;

public class MethodOverload {

    // Method to add two integers
    void sum(int a, int b) {
        System.out.println("Sum is " + (a + b));
    }

    // Method to add three integers
    void sum(int a, int b, int c) {
        System.out.println("Sum is " + (a + b + c));
    }

    // Method to add two double numbers
    void sum(double a, double b) {
        System.out.println("Sum is " + (a + b));
    }

    public static void main(String[] args) {
        MethodOverload cal = new MethodOverload();
        System.out.println("Method Overloading");

        cal.sum(8, 5);        // Calls sum(int a, int b)
        cal.sum(5, 5, 5);     // Calls sum(int a, int b, int c)
        cal.sum(4.6, 3.8);    // Calls sum(double a, double b)
    }
}
/* constructor overloading*/
package SapJava;

public class Student {
    int id;        // Instance variable
    String name;   // Instance variable

    // Default constructor
    Student() {
        System.out.println("This is a default constructor");
    }

    // Parameterized constructor
    Student(int i, String n) {
        id = i;
        name = n;
    }

    public static void main(String[] args) {
        // Using default constructor
        Student s = new Student();
        System.out.println("\nDefault Constructor values:\n");
        System.out.println("Student Id: " + s.id + "\nStudent Name: " + s.name);

        // Using parameterized constructor
        Student student = new Student(10, "Parth");
        System.out.println("\nParameterized Constructor values:\n");
        System.out.println("Student Id: " + student.id + "\nStudent Name: " + student.name);
    }
}
/*matching and non matching rectangle*/
package FJP;
import java.util.Scanner;

public class Rectangle {
    double length, width, area;
    String colour;
    Scanner scanner = new Scanner(System.in);

    // Method to get length
    void get_length() {
        System.out.println("Enter the Length of Rectangle: ");
        length = scanner.nextDouble();
    }

    // Method to get width
    void get_width() {
        System.out.println("Enter the Width of Rectangle: ");
        width = scanner.nextDouble();
    }

    // Method to get colour
    void get_Colour() {
        System.out.println("Enter the Colour of Rectangle: ");
        colour = scanner.next();
    }

    // Method to calculate area
    double find_area() {
        area = length * width;
        return area;
    }

    public static void main(String[] args) {
        Rectangle rectangle1 = new Rectangle();
        Rectangle rectangle2 = new Rectangle();

        System.out.println("THIS IS FOR RECTANGLE 1\n");
        rectangle1.get_length();
        rectangle
/* calculator*/
import java.util.Scanner;

public class Calculator {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int choice;
        int no1, no2, result;

        do {
            System.out.println("\n--- Simple Calculator ---");
            System.out.println("1. Add");
            System.out.println("2. Subtract");
            System.out.println("3. Multiply");
            System.out.println("4. Divide");
            System.out.println("5. Factorial");
            System.out.println("6. Exit");

            System.out.print("Enter your choice: ");
            choice = in.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter First Number: ");
                    no1 = in.nextInt();
                    System.out.print("Enter Second Number: ");
                    no2 = in.nextInt();
                    result = no1 + no2;
                    System.out.println("Addition: " + result);
                    break;

                case 2:
                    System.out.print("Enter First Number: ");
                    no1 = in.nextInt();
                    System.out.print("Enter Second Number: ");
                    no2 = in.nextInt();
                    result = no1 - no2;
                    System.out.println("Subtraction: " + result);
                    break;

                case 3:
                    System.out.print("Enter First Number: ");
                    no1 = in.nextInt();
                    System.out.print("Enter Second Number: ");
                    no2 = in.nextInt();
                    result = no1 * no2;
                    System.out.println("Multiplication: " + result);
                    break;

                case 4:
                    System.out.print("Enter First Number: ");
                    no1 = in.nextInt();
                    System.out.print("Enter Second Number: ");
                    no2 = in.nextInt();
                    if (no2 != 0) {
                        result = no1 / no2;
                        System.out.println("Division: " + result);
                    } else {
                        System.out.println("Error: Cannot divide by zero!");
                    }
                    break;

                case 5:
                    System.out.print("Enter Number: ");
                    no1 = in.nextInt();
                    result = 1;
                    for (int i = 1; i <= no1; ++i) {
                        result *= i;
                    }
                    System.out.println("Factorial of " + no1 + " is " + result);
                    break;

                case 6:
                    System.out.println("Terminating program...");
                    break;

                default:
                    System.out.println("Invalid Choice! Please try again.");
                    break;
            }

        } while (choice != 6);

        in.close();
    }
}
/* display first 50 number; factorial*/
import java.util.Scanner;

class Exp1 {
    public static void main(String args[]) {
        Scanner sc = new Scanner(System.in);
        int ch, i, num, n, sum, cnt, flag, fact;

        do {
            System.out.println("\n1 : Find Factorial");
            System.out.println("2 : Display First 50 Prime Numbers");
            System.out.println("3 : Find Sum and Average of N Numbers");
            System.out.println("4 : Exit");
            System.out.print("Enter Choice = ");
            ch = sc.nextInt();

            switch (ch) {
                case 1:
                    System.out.print("Enter number = ");
                    n = sc.nextInt();
                    fact = 1;
                    for (i = 1; i <= n; i++)
                        fact = fact * i;
                    System.out.println("Factorial = " + fact);
                    break;

                case 2:
                    cnt = 1;
                    n = 1;
                    System.out.println("First 50 Prime Numbers:");
                    while (cnt <= 50) {
                        flag = 1;
                        for (i = 2; i <= n / 2; i++) {
                            if (n % i == 0) {
                                flag = 0;
                                break;
                            }
                        }
                        if (flag == 1 && n > 1) {
                            System.out.print(n + " ");
                            cnt++;
                        }
                        n++;
                    }
                    System.out.println();
                    break;

                case 3:
                    System.out.print("Enter limit = ");
                    n = sc.nextInt();
                    sum = 0;
                    for (i = 1; i <= n; i++) {
                        System.out.print("Enter number  = ");
                        num = sc.nextInt();
                        sum = sum + num;
                    }
                    System.out.println("Sum = " + sum);
                    System.out.println("Average = " + (float) sum / n);
                    break;

                case 4:
                    System.out.println("Exiting program...");
                    break;

                default:
                    System.out.println("Invalid choice!");
            }
        } while (ch != 4);

        sc.close();
    }
}



