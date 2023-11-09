import java.util.ArrayList;
import java.util.Scanner;

class Person {
    protected String name;
    protected int age;
    protected String address;
    protected String phoneNumber;
    protected String email;

    public Person(String name, int age, String address, String phoneNumber, String email) {
        this.name = name;
        this.age = age;
        this.address = address;
        this.phoneNumber = phoneNumber;
        this.email = email;
    }

    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Address: " + address);
        System.out.println("Phone Number: " + phoneNumber);
        System.out.println("Email: " + email);
        System.out.println("Department: Software");
    }
}
class MyThread extends Thread {
    private String threadName;

    public MyThread(String name) {
        this.threadName = name;
    }

    @Override
    public void run() {
        System.out.println(" Page for Marksheep "  + " is being genrated");
        // Add the task you want this thread to perform here.
        // For example, you can add a delay to simulate some work.
        try {
            Thread.sleep(2000); // Sleep for 2 seconds
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(" page genrate fill the information" );
    }
}
class Student extends Person {
    private int studentId;
    private String department;
    private ArrayList<Course> courses;
    private int oopMarks;
    private int iseMarks;
    private int ppMarks;
    int totalMarks;

    public Student(String name, int age, String address, String phoneNumber, String email, int studentId) {
        super(name, age, address, phoneNumber, email);
        this.studentId = studentId;
        this.department = "";
        this.courses = new ArrayList<>();
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

    public void setOopMarks(int oopMarks) {
        this.oopMarks = oopMarks;
    }

    public void setIseMarks(int iseMarks) {
        this.iseMarks = iseMarks;
    }

    public void setPpMarks(int ppMarks) {
        this.ppMarks = ppMarks;
    }

    public void addCourse(Course course) {
        courses.add(course);
    }

    public void displayCourses() {
        System.out.println("Courses enrolled:");
        for (Course course : courses) {
            System.out.println("- " + course.getCourseName());
        }
    }

    public double calculatePercentage() {
        int totalMarks = 300; // 100 (OOP) + 100 (ISE) + 100 (PP)
        int obtainedMarks = oopMarks + iseMarks + ppMarks;

        return (obtainedMarks / (double) totalMarks) * 100;
    }
}

class Teacher extends Person {
    private String employeeId;
    private ArrayList<Course> coursesTaught;

    public Teacher(String name, int age, String address, String phoneNumber, String email, String employeeId) {
        super(name, age, address, phoneNumber, email);
        this.employeeId = employeeId;
        this.coursesTaught = new ArrayList<>();
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public void addCourseTaught(Course course) {
        coursesTaught.add(course);
    }

    public void displayCoursesTaught() {
        System.out.println("Courses taught:");
        for (Course course : coursesTaught) {
            System.out.println("- " + course.getCourseName());
        }
    }
}

class Course {
    private String courseCode;
    private String courseName;

    public Course(String courseCode, String courseName) {
        this.courseCode = courseCode;
        this.courseName = courseName;
    }

    public String getCourseCode() {
        return courseCode;
    }

    public String getCourseName() {
        return courseName;
    }
}

public class MarkSheetProject {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

            
            
        MyThread thread1 = new MyThread("Thread 1");
        

        thread1.start();
       

        // Your existing code...

        // Wait for both threads to finish before closing the scanner
        try {
            thread1.join();
            
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

    
    

        Student[] students = new Student[1];
        Teacher[] teachers = new Teacher[1];
        Course[] courses = new Course[1];

        for (int i = 0; i < 1; i++) {
            System.out.println("Enter information for Student " + (i + 1) + ":");
            students[i] = createStudentFromUserInput(scanner);

            System.out.println("Enter department for Student " + (i + 1) + ":");
            students[i].setDepartment(scanner.next());

            System.out.println("Enter marks for three subjects for Student " + (i + 1) + ":");
            students[i].setOopMarks(getSubjectMarks(scanner, "OOP"));
            students[i].setIseMarks(getSubjectMarks(scanner, "ISE"));
            students[i].setPpMarks(getSubjectMarks(scanner, "PP"));
        }
        for (int i = 0; i < 1; i++) {
            System.out.println("Enter information for Teacher " + (i + 1) + ":");
            teachers[i] = createTeacherFromUserInput(scanner);

            System.out.println("Enter information for Course " + (i + 1) + ":");
            courses[i] = createCourseFromUserInput(scanner);

            students[i].addCourse(courses[i]);
            teachers[i].addCourseTaught(courses[i]);
        }

        for (int i = 0; i < 1; i++) {
            System.out.println("\nStudent Information " + (i + 1) + ":");
            students[i].displayInfo();
            students[i].displayCourses();
            students[i].getDepartment();

            System.out.println("\nTeacher Information " + (i + 1) + ":");
            teachers[i].displayInfo();
            teachers[i].displayCoursesTaught();

            double percentage = students[i].calculatePercentage();
            System.out.println("out of 300 marks you have got "+"Percentage: " + percentage + "%");
        }

        scanner.close();
    }

    private static Student createStudentFromUserInput(Scanner scanner) {
        System.out.print("Enter student name: ");
        String name = scanner.next();

        System.out.print("Enter student age: ");
        int age = scanner.nextInt();

        System.out.print("Enter student address: ");
        String address = scanner.next();

        System.out.print("Enter student phone number: ");
        String phoneNumber = scanner.next();

        System.out.print("Enter student email: ");
        String email = scanner.next();

        System.out.print("Enter student ID: ");
        int studentId = scanner.nextInt();

        return new Student(name, age, address, phoneNumber, email, studentId);
    }

    private static Teacher createTeacherFromUserInput(Scanner scanner) {
        System.out.print("Enter teacher name: ");
        String name = scanner.next();

        System.out.print("Enter teacher age: ");
        int age = scanner.nextInt();

        System.out.print("Enter teacher address: ");
        String address = scanner.next();

        System.out.print("Enter teacher phone number: ");
        String phoneNumber = scanner.next();

        System.out.print("Enter teacher email: ");
        String email = scanner.next();

        System.out.print("Enter teacher employee ID: ");
        String employeeId = scanner.next();

        return new Teacher(name, age, address, phoneNumber, email, employeeId);
    }

    private static Course createCourseFromUserInput(Scanner scanner) {
        System.out.print("Enter course code: ");
        String courseCode = scanner.next();

        System.out.print("Enter course name: ");
        String courseName = scanner.next();

        return new Course(courseCode, courseName);
    }

    private static int getSubjectMarks(Scanner scanner, String subject) {
        System.out.print("Enter marks for " + subject + ": ");
       
        return scanner.nextInt();
    }

    private static double calculatePercentage(int mathMarks, int englishMarks, int scienceMarks) {
        int totalMarks = 300; // 100 (OOP) + 100 (ISE) + 100 (PP)
        int obtainedMarks = mathMarks + englishMarks + scienceMarks;

        return (obtainedMarks / (double) totalMarks) * 100;
    }
}
