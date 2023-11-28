```
# Eligibility for admission
using System;
namespace EngineeringAdmission
{
    class Program
    {
        static void Main(string[] args)
        {
            int maths, physics, chemistry;
            Console.WriteLine("Welcome to Engineering Admission Eligibility Checker");
            Console.Write("Enter Math marks: ");
            maths = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter Physics marks: ");
            physics = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter Chemistry marks: ");
            chemistry = Convert.ToInt32(Console.ReadLine());
            int totalMarks = maths + physics + chemistry;
            if (maths >= 65 && physics >= 55 && chemistry >= 50)
            {
                if (totalMarks >= 180)
                {
                    Console.WriteLine("Congratulations! You are eligible for admission.");
                }
                else
                {
                    Console.WriteLine("Sorry, you are not eligible for admission.");
                }
            }
        }
    }
}

# Palindrome
using System;
namespace palindrome
{
    class Program
    {
        static void Main(string[] args)
        {
            string s, revs = "";
            Console.WriteLine("Enter string");
            s = Console.ReadLine();
            for (int i = s.Length - 1; i >= 0; i--) //String Reverse  
            {
                revs += s[i].ToString();
            }
            if (revs == s) // Checking whether string is palindrome or not  
            {
                Console.WriteLine("String is Palindrome\nEntered String Was {0} and reverse string is {1}", s, revs);
            }
            else
            {
                Console.WriteLine("String is not Palindrome\nEntered String Was {0} and reverse string is {1}", s, revs);
            }
            Console.ReadKey();
        }
    }
}

# Pattern
using System;
public class pattern
{
    public static void Main()
    {
        int rows, c = 1, a, i, j;
        Console.Write("rows: ");
        rows = Convert.ToInt32(Console.ReadLine());
        for (i = 0; i < rows; i++)
        {
            for (a = 1; a <= rows - i; a++)
            {
                Console.Write(" ");
            }
            for (j = 0; j <= i; j++)
            {
                if (j == 0 || i == 0)
                {
                    c = 1;
                }
                else
                {
                    c = c * (i - j + 1) / j;
                }
                Console.Write("{0} ", c);
            }
            Console.Write("\n");
        }
    }
}

# Constructor
using System;
public class Employee
{
   public String designation;
   public String employee_name;
   public int exp, insurance,bs;
   double hra, ta, salaryam;
   public Employee(String employee_name, String designation, int exp, int bs, int i)
   {
       this.employee_name = employee_name;
       this.designation = designation;
       this.exp = exp;
       this.bs = bs;
       this.insurance = i;
   }
   public void salary()
   {
       hra = this.bs * 0.2;
       ta = this.bs * 0.1;
       salaryam = this.bs + hra + ta - this.insurance;
   }
   public void display()
   {
       Console.WriteLine("Name of the employee is {0} having {1} of experience,working as {2}", this.employee_name, this.exp, this.designation);
       Console.WriteLine("Receives {0} of salary.", salaryam);
   }
}
class TestEmployee
{
   public static void Main(string[] args)
   {
       Employee e1 = new Employee("Leann","Tester", 5, 40000, 1000);
       e1.salary();
       Employee e2 = new Employee("Adhiradhan", "Developer", 5, 55000, 1000);
       e2.salary();
       e1.display();
       e2.display();
   }
}


# Jagged array
using System;
class jaggedarray
{
    public static void Main(String[] args)
    {
        int[][] array = new int[4][];
        array[0] = new int[3];
        array[1] = new int[5];
        array[2] = new int[6];
        array[3] = new int[4];
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < array[i].Length; j++)
            {
                array[i][j] = i * j + 70;
            }
        }
        for (int i = 0; i < array.Length; i++)
        {
            for (int j = 0; j < array[i].Length; j++)
            {
                Console.WriteLine("CPU usage {0} is {1} %" , i + 1, array[i][j]);
            }
            Console.WriteLine();
        }
    }
}

# Operator overloading
using System;
namespace ConsoleApp8
{
   class example
   {
       public int length;
       public example()
       {
           length = 10;
       }
       public example(int i)
       {
           length = i;
       }
       public static bool operator ==(example obj1, example obj2)
       {
           return obj1.Equals(obj2);
       }
       public static bool operator !=(example obj1, example obj2)
       {
           return !obj1.Equals(obj2);
       }
       public static void Main()
       {
           example e1 = new example();
           example e2 = new example(20);
           example e3 = new example();
           example e4 = e3;
           if (e3 == e4)
           {
               Console.WriteLine("Equal");
           }
           else if (e3 != e4)
           {
               Console.WriteLine("Not equal");
           }
       }
   }
}


# Recursive fun
using System;
namespace rec
{
    class Program
    {
        int rem = 0, rev = 0;
        public int reverse(int n)
        {
            rem = n % 10;
            if (rem == 0)
            {
                return rev;
            }
            else
            {
                rev = rev * 10 + rem;
                return reverse(n / 10);
            }
        }
        static void Main(string[] args)
        {
            int n;
            Console.WriteLine("Enter a Number to reverse: ");
            n = Convert.ToInt32(Console.ReadLine());
            Program p1 = new Program();
            Console.WriteLine("Reversed Number is " + p1.reverse(n));
        }
    }
}
# Inheritance
using System;
namespace inheri
{
    public class tyre
    {
        public virtual void display()
        {
            Console.Write("Tyre has been inserted:");
        }
    }
    class Scooter : tyre
    {
        public override void display()
        {
            base.display(); 
            Console.WriteLine("scooter ");
        }
    }
    class Car : tyre
    {
        public override void display()
        {
            base.display();
            Console.WriteLine("car ");
        }
    }
    class program
    {
        static void Main()
        {
            Scooter s = new Scooter();
            s.display();
            Car c = new Car();
            c.display();
        }
    }
}

# Interface
using System;
public interface Bank
{
    void deposit();
    void withdrawal();
}
class Program : Bank
{
    int amount, ch, balance = 2000;
    public Program()
    {
        Console.WriteLine("1.Deposit\n2.Withdrawal");
        ch = Convert.ToInt32(Console.ReadLine());
        if (ch == 1)
        {
            deposit();
        }
        else
        {
            withdrawal();
        }
    }
    public void withdrawal()
    {
        int amount = Convert.ToInt32(Console.ReadLine());
        balance -= amount;
        Console.WriteLine(balance);
    }
    public void deposit()
    {
        int amount = Convert.ToInt32(Console.ReadLine());
        balance += amount;
        Console.WriteLine(balance);
    }
}
class example
{
    public static void Main()
    {
        Program c = new Program();
        c.deposit();
        c.withdrawal();
    }
}

# file
using System;
using System.IO;
struct student
{
    public string name;
    public int age;
    public string department;
    public int percentage;
};
class HelloWorld
{

    void writer(string name, int age, string department, int percentage, int i)
    {
        FileStream fs = new FileStream("file.txt", FileMode.Append, FileAccess.Write);
        StreamWriter sw = new StreamWriter(fs);
        sw.WriteLine("Name of the student {0} is {1}", i, name);
        sw.WriteLine("Age of the student {0} is {1}", i, age);
        sw.WriteLine("Department of the student {0} is {1}", i, department);
        sw.WriteLine("percentage of the student {0} is {1}", i, percentage);

        sw.Close();
        fs.Close();
    }
    static void Main()
    {
        int n, i;
        FileStream fs = new FileStream("file.txt", FileMode.Create, FileAccess.Write);
        fs.Close();
        Console.WriteLine("Enter the number of Students");
        n = Convert.ToInt32(Console.ReadLine());
        student[] s = new student[n];
        for (i = 0; i < n; i++)
        {
            Console.WriteLine("Enter the name");
            s[i].name = Console.ReadLine();
            Console.WriteLine("Enter the age");
            s[i].age = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("Enter the department");
            s[i].department = Console.ReadLine();
            Console.WriteLine("Enter the percentage");
            s[i].percentage = Convert.ToInt32(Console.ReadLine());
            HelloWorld hw = new HelloWorld();
            hw.writer(s[i].name, s[i].age, s[i].department, s[i].percentage, i + 1);
            Console.WriteLine();
        }
    }
}
