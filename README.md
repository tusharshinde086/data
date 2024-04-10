                                 Slip  1

Q1.Write the definition for a class Cylinder that contains data members radius and height. The class has the following member functions:

a. void setradius(float) to set the radius of data member.

b. void setheight(float) to set the height of data member.

c. float volume() to calculate and return the volume of the cylinder.

Write a C++ program to create cylinder object and display its volume.

ANS;

 
#include <iostream.h>
#include<conio.h>

class Cylinder {
private:
    float radius;
    float height;
public:
    void setradius(float r) {
	radius = r;
	  }

    void setheight(float h) {
	height = h;
    }

    float volume() {
	return 3.14* radius * radius * height;
    }
};

void main() {
    Cylinder cyl;
    cyl.setradius(5.0);
    cyl.setheight(10.0);
    cout << "Volume of the cylinder: " << cyl.volume() << endl;
    getch();
}

Q2. Write a C++ program to create a class Array that contains one float array as member. Overload the Unary ++ and -- operators to increase or decrease the value of each element of an array. Use friend function for operator function

ANS:

#include <iostream.h>
#include<conio.h>

class Array {
private:
    float arr[5];

public:
    Array(float values[]) {
	for (int i = 0; i < 5; ++i) {
            arr[i] = values[i];
        }
    }
    friend Array operator++(Array &a) {
        for (int i = 0; i < 5; ++i) {
	    ++a.arr[i];
	}
        return a;
    }
    friend Array operator--(Array &a) {
        for (int i = 0; i < 5; ++i) {
            --a.arr[i];
        }
        return a;
    }

    void display() {
        cout << "Array elements: ";
        for (int i = 0; i < 5; ++i) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
};

void main() {
    float values[] = {1.1, 2.2, 5.3, 4.4, 3.7};
       clrscr();
    Array arr(values);

    cout << "Original array:" << endl;
    arr.display();

    ++arr;
    cout << "After incrementing:" << endl;
    arr.display();

    --arr;
    cout << "After decrementing:" << endl;
    arr.display();
   getch();
}



Q2. Write a C++ program to create a class Shape with functions to find area of the shape and display the name of the shape and other essential components of the class. Create derived classes circle, rectangle and trapezoid each having overridden function area and display. Write a suitable program to illustrate Virtual Function.
ANS:

#include <iostream.h>
#include <conio.h>
#include <math.h>
#include<string.h>
class Shape {
protected:
    char name[20];
public:
    Shape(char* n) {
        strcpy(name, n);
    }
    virtual void display() {
        cout << "Shape: " << name << endl;
    }
    virtual float area() {
        return 0.0;
    }
};

class Circle : public Shape {
private:
    float radius;
public:
    Circle(char* n, float r) : Shape(n), radius(r) {}
    void display() {
        Shape::display();
        cout << "Radius: " << radius << endl;
    }
    float area() {
        return 3.1415 * radius * radius;
    }
};

class Rectangle : public Shape {
private:
    float length, width;
public:
    Rectangle(char* n, float l, float w) : Shape(n), length(l), width(w) {}
    void display() {
        Shape::display();
        cout << "Length: " << length << ", Width: " << width << endl;
    }
    float area() {
        return length * width;
    }
};

class Trapezoid : public Shape {
private:
    float base1, base2, height;
public:
    Trapezoid(char* n, float b1, float b2, float h) : Shape(n), base1(b1), base2(b2), height(h) {}
    void display() {
        Shape::display();
        cout << "Base1: " << base1 << ", Base2: " << base2 << ", Height: " << height << endl;
    }
    float area() {
        return 0.5 * (base1 + base2) * height;
    }
};

int main() {
    clrscr();
    Shape* shapes[3];
    shapes[0] = new Circle("Circle", 5.0);
    shapes[1] = new Rectangle("Rectangle", 4.0, 6.0);
    shapes[2] = new Trapezoid("Trapezoid", 3.0, 5.0, 4.0);

    for (int i = 0; i < 3; i++) {
        shapes[i]->display();
        cout << "Area: " << shapes[i]->area() << endl;
        cout << endl;
    }

    for ( i = 0; i < 3; i++) {
        delete shapes[i];
    }

    getch();
    return 0;
}

                       Slip 2

 
Q1.Write a C++ program to create two classes Rectanglel and Rectangle. Compare area of both the rectangles using friend function.

ANS:

#include <iostream.h>
#include<conio.h>
class Rectangle2;
class Rectangle1 {
private:
    float length;
    float width;

public:
    Rectangle1(float l, float w) : length(l), width(w) {}

    float area() {
	return length * width;
    }

    friend void compareAreas(Rectangle1 &r1, Rectangle2 &r2);
};

class Rectangle2 {
private:
    float length;
    float width;

public:
    Rectangle2(float l, float w) : length(l), width(w) {}

    float area() {
	return length * width;
    }

    friend void compareAreas(Rectangle1 &r1, Rectangle2 &r2);
};

void compareAreas(Rectangle1 &r1, Rectangle2 &r2) {
    float area1 = r1.area();
    float area2 = r2.area();

    if (area1 > area2) {
	cout << "Area of Rectangle1 is greater than Rectangle2." << endl;
    } else if (area1 < area2) {
	cout << "Area of Rectangle2 is greater than Rectangle1." << endl;
    } else {
	cout << "Both rectangles have equal area." << endl;
    }
}

void main() {
    Rectangle1 rect1(5, 4);
    Rectangle2 rect2(6, 3);

    compareAreas(rect1, rect2);
  getch();
}


Q2. A book (ISBN) and CD (data capacity) are both types of media (I'd title) objects. A person buys 10 media items each of which can be either book or CD. Display the list of all books and CD's bought. Define the classes and appropriate member functions to accept and display data. Use pointers and concept of polymorphism (Virtual Function)
ANS:
#include <iostream.h>
#include <string.h>
#include<conio.h>
const int MAX_ITEMS = 4;
class Media {
protected:
    char title[50];
public:
    virtual void accept() = 0;
    virtual void display() = 0;
};

class Book : public Media {
    char ISBN[14]; // Assuming ISBN is of length 13 + '\0'
public:
    void accept() {
	cout << "Enter title of the book: ";
	cin.getline(title, 50);
	cout << "Enter ISBN: ";
	cin.getline(ISBN, 14);
    }

    void display() {
	cout << "Title: " << title << endl;
	cout << "ISBN: " << ISBN << endl;
    }
};

class CD : public Media {
    int capacity;
public:
    void accept() {
	cout << "Enter title of the CD: ";
	cin.getline(title, 50);
	cout << "Enter data capacity (in MB): ";
	cin >> capacity;
	cin.ignore(); // Clear input buffer
    }

    void display() {
	cout << "Title: " << title << endl;
	cout << "Data Capacity: " << capacity << " MB" << endl;
    }
};

int main() {
    Media* items[MAX_ITEMS];

    cout << "Enter details for 4 media items:\n";
    for (int i = 0; i < MAX_ITEMS; ++i) {
	char choice;
	cout << "Is this item a book (b) or a CD (c)? ";
	cin >> choice;
	cin.ignore(); // Clear input buffer

	if (choice == 'b') {
	    items[i] = new Book();
	} else if (choice == 'c') {
	    items[i] = new CD();
	} else {
	    cout << "Invalid choice. Please enter 'b' for book or 'c' for CD." << endl;
	    --i; // Decrement i to re-enter the loop for the same item
	    continue;
	}
	items[i]->accept();
    }
    cout << "\nList of Books and CDs Bought:\n";
    for ( i = 0; i < MAX_ITEMS; ++i) {
	cout << "Item " << i + 1 << ":\n";
	items[i]->display();
	cout << endl;
	delete items[i]; // Free dynamically allocated memory
    }
    getch();
    return 0;
}


Q3.Write a C++ program to copy the contents of one file to another



Slip 3

Q1.Write a C++ program to overload function Volume and find Volume of Cube, Cylinder and
Sphere.
Ans

#include <iostream.h>
#include <conio.h>

// Inline function to calculate the area of a circle
inline float areaCircle(float radius) {
    return 3.14159 * radius * radius;
}

// Inline function to calculate the area of a square
inline float areaSquare(float side) {
    return side * side;
}

// Inline function to calculate the area of a rectangle
inline float areaRectangle(float length, float width) {
    return length * width;
}

int main() {
    clrscr(); // Clear the screen

    // Input data
    float radius = 5.0;
    float side = 4.0;
    float length = 6.0;
    float width = 3.0;

    // Calculate and display area of circle
    cout << "Area of Circle with radius " << radius << ": " << areaCircle(radius) << endl;

    // Calculate and display area of square
    cout << "Area of Square with side " << side << ": " << areaSquare(side) << endl;

    // Calculate and display area of rectangle
    cout << "Area of Rectangle with length " << length << " and width " << width << ": " << areaRectangle(length, width) << endl;

    getch(); // Wait for a key press before exiting
    return 0;
}


Q2.   Write a C++ program with Student as abstract class and create derive classes Engineering, 
Medicine and Science having data member rollno and name from base class Student. Create 
objects of the derived classes and access them using array of pointer of base class Student.
Ans

#include<iostream.h>
#include<conio.h>
#include<stdio.h>
#include<string.h>

class Student {
protected:
    int rollno;
    char name[50];
public:
    virtual void setData(int r, char n[]) = 0;
    virtual void displayData() = 0;
};

class Engineering : public Student {
public:
    void setData(int r, char n[]) {
        rollno = r;
        strcpy(name, n);
    }
    void displayData() {
        cout << "Engineering Student\n";
        cout << "Roll No: " << rollno << endl;
        cout << "Name: " << name << endl;
    }
};

class Medicine : public Student {
public:
    void setData(int r, char n[]) {
        rollno = r;
        strcpy(name, n);
    }
    void displayData() {
        cout << "Medicine Student\n";
        cout << "Roll No: " << rollno << endl;
        cout << "Name: " << name << endl;
    }
};

class Science : public Student {
public:
    void setData(int r, char n[]) {
        rollno = r;
        strcpy(name, n);
    }
    void displayData() {
        cout << "Science Student\n";
        cout << "Roll No: " << rollno << endl;
        cout << "Name: " << name << endl;
    }
};

int main() {
    clrscr();
    Student *students[3];
    Engineering eng;
    Medicine med;
    Science sci;

    eng.setData(101, "John");
    med.setData(102, "Emily");
    sci.setData(103, "Michael");

    students[0] = &eng;
    students[1] = &med;
    students[2] = &sci;

    for(int i = 0; i < 3; i++) {
        students[i]->displayData();
    }

    getch();
    return 0;
}




 Q3.        Create a class String which contains a character pointer (Use new and delete operator) 
Write a C++ program to overload following operators 
a. ! To reverse the case of each alphabet from given string. 
b. [ ] To print a character present at specified index



 #include<iostream.h>
#include<conio.h>
#include<string.h>

class String {
private:
    char *str;
public:
    String() {
        str = NULL;
    }

    String(const char *s) {
        int len = strlen(s);
        str = new char[len + 1];
        strcpy(str, s);
    }

    ~String() {
        if(str != NULL)
            delete[] str;
    }

    String(const String &s) {
        int len = strlen(s.str);
        str = new char[len + 1];
        strcpy(str, s.str);
    }

    void operator!() {
        for (int i = 0; str[i] != '\0'; i++) {
            if (isalpha(str[i])) {
                if (isupper(str[i]))
                    str[i] = tolower(str[i]);
                else
                    str[i] = toupper(str[i]);
            }
        }
    }

    char& operator[](int index) {
        return str[index];
    }

    void display() {
        cout << str;
    }
};

int main() {
    clrscr();
    String s("Hello World!");
    !s; // Reversing the case of each alphabet
    s.display(); // Displaying the modified string

    cout << endl;
    cout << "Character at index 6: " << s[6] << endl;

    getch();
    return 0;
}


slip 4        

    Q1.Write a C++ program to print area of circle, square and rectangle using inline function.

Ans

#include<iostream.h>
#include<conio.h>

#define PI 3.14159
#define AREA_CIRCLE(radius) (PI * radius * radius)
#define AREA_SQUARE(side) (side * side)
#define AREA_RECTANGLE(length, width) (length * width)

int main() {
    float radius, side, length, width;

    // Input for circle
    cout << "Enter radius of the circle: ";
    cin >> radius;
    cout << "Area of the circle: " << AREA_CIRCLE(radius) << endl;

    // Input for square
    cout << "Enter side of the square: ";
    cin >> side;
    cout << "Area of the square: " << AREA_SQUARE(side) << endl;

    // Input for rectangle
    cout << "Enter length of the rectangle: ";
    cin >> length;
    cout << "Enter width of the rectangle: ";
    cin >> width;
    cout << "Area of the rectangle: " << AREA_RECTANGLE(length, width) << endl;

    getch();
    return 0;
}



: Q2.      Write a C++ program to create a class which contains two dimensional integer array of size m*n 
Write a member function to display transpose of entered matrix.(Use Dynamic Constructor for 
allocating memory and Destructor to free memory of an object).
Ans

: #include <iostream.h>
#include <conio.h>

class Matrix {
private:
    int **data;
    int rows;
    int cols;

public:
    // Constructor to allocate memory for the matrix
    Matrix(int m, int n) {
        rows = m;
        cols = n;
        data = new int*[rows];
	for (int i = 0; i < rows; i++) {
            data[i] = new int[cols];
        }
    }

    // Destructor to free allocated memory
    ~Matrix() {
        for (int i = 0; i < rows; i++) {
            delete[] data[i];
        }
        delete[] data;
    }

    // Function to input values into the matrix
    void inputMatrix() {
        cout << "Enter the elements of the matrix:" << endl;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                cin >> data[i][j];
            }
        }
    }

    // Function to display the transpose of the matrix
    void displayTranspose() {
        cout << "Transpose of the matrix:" << endl;
        for (int j = 0; j < cols; j++) {
            for (int i = 0; i < rows; i++) {
                cout << data[i][j] << "\t";
            }
            cout << endl;
        }
    }
};

int main() {
    clrscr(); // Clear the screen

    int m, n;
    cout << "Enter the number of rows and columns of the matrix: ";
    cin >> m >> n;

    // Create a Matrix object with dynamic memory allocation
    Matrix mat(m, n);

    // Input values into the matrix
    mat.inputMatrix();

    // Display the transpose of the matrix
    mat.displayTranspose();

    getch(); // Wait for a key press before exiting
    return 0;
}



: Q3.     Create a base class Flight containing protected data members as Flight_no, Flight_Name. Derive 
a class Route(Source, Destination) from class Flight. Also derive a class Reservation (no_seats, 
class, fare, travel_date) from Route. Write a C++ program to perform the following necessary 
functions. 
a. Enter details of n reservations. 
b. Display reservation details of Business class.
ans
: #include <iostream.h>
#include <conio.h>

class Flight {
protected:
    int Flight_no;
    char Flight_Name[50];

public:
    // Function to input flight details
    void inputFlightDetails() {
        cout << "Enter Flight Number: ";
        cin >> Flight_no;
        cout << "Enter Flight Name: ";
        cin.ignore(); // Ignore newline character
        cin.getline(Flight_Name, 50);
    }
};

class Route : public Flight {
protected:
    char Source[50];
    char Destination[50];

public:
    // Function to input route details
    void inputRouteDetails() {
        cout << "Enter Source: ";
        cin.ignore(); // Ignore newline character
        cin.getline(Source, 50);
        cout << "Enter Destination: ";
        cin.getline(Destination, 50);
    }
};

class Reservation : public Route {
private:
    int no_seats;
    char class_type[20];
    float fare;
    char travel_date[20];

public:
    // Function to input reservation details
    void inputReservationDetails() {
        cout << "Enter number of seats: ";
        cin >> no_seats;
        cout << "Enter class (Business/Economy): ";
        cin >> class_type;
        cout << "Enter fare: ";
        cin >> fare;
        cout << "Enter travel date: ";
        cin >> travel_date;
    }

    // Function to display reservation details of Business class
    void displayBusinessClass() {
        if (strcmp(class_type, "Business") == 0) {
            cout << "Flight Number: " << Flight_no << endl;
            cout << "Flight Name: " << Flight_Name << endl;
            cout << "Source: " << Source << endl;
            cout << "Destination: " << Destination << endl;
            cout << "Number of Seats: " << no_seats << endl;
            cout << "Class: " << class_type << endl;
            cout << "Fare: " << fare << endl;
            cout << "Travel Date: " << travel_date << endl;
        }
    }
};

int main() {
    clrscr(); // Clear the screen

    int n;
    cout << "Enter the number of reservations: ";
    cin >> n;

    // Create an array of Reservation objects
    Reservation* reservations = new Reservation[n];

    // Input details of reservations
    for (int i = 0; i < n; i++) {
        cout << "\nEnter details of reservation " << i + 1 << ":" << endl;
        reservations[i].inputFlightDetails();
        reservations[i].inputRouteDetails();
        reservations[i].inputReservationDetails();
    }

    // Display reservation details of Business class
    cout << "\nReservation details of Business class:" << endl;
    for (int i = 0; i < n; i++) {
        reservations[i].displayBusinessClass();
    }

    delete[] reservations; // Free allocated memory

    getch(); // Wait for a key press before exiting
    return 0;
}

                  Slip 5

Q1.Write a C++ program to create a class Mobile which contains data members as Mobile_Id,
Mobile_Name, Mobile_Price. Create and Initialize all values of Mobile object by using
parameterized constructor. Display the values of Mobile object.

#include<iostream.h>
#include<conio.h>
#include<string.h>

class Mobile {
private:
    int Mobile_Id;
    char Mobile_Name[50];
    float Mobile_Price;

public:
    // Parameterized constructor
    Mobile(int id, char name[], float price) {
        Mobile_Id = id;
        strcpy(Mobile_Name, name);
        Mobile_Price = price;
    }

    // Function to display Mobile details
    void displayMobileDetails() {
        cout << "Mobile ID: " << Mobile_Id << endl;
        cout << "Mobile Name: " << Mobile_Name << endl;
        cout << "Mobile Price: " << Mobile_Price << endl;
    }
};

void main() {
    clrscr();
    // Creating a Mobile object and initializing it using parameterized constructor
    Mobile mobile1(101, "iPhone 12", 999.99);

    // Displaying the values of the Mobile object
    mobile1.displayMobileDetails();

    getch();
}

Q2.Create a base class Student (Roll_No, Name) which derives two classes Theory and Practical.
Theory class contains marks of five Subjects and Practical class contains marks of two practical
subjects. Class Result (Total_Marks, Class) inherits both Theory and Practical classes. (Use
concept of Virtual Base Class) Write a menu driven program to perform the following functions:
a. Build a master table.
b. Display master table.



#include<iostream.h>
#include<conio.h>
#include<string.h>

class Student {
protected:
    int Roll_No;
    char Name[50];

public:
    void getData() {
        cout << "Enter Roll No: ";
        cin >> Roll_No;
        cout << "Enter Name: ";
        cin >> Name;
    }
};

class Theory : virtual public Student {
protected:
    float marks_theory[5];

public:
    void getTheoryMarks() {
        cout << "Enter Marks for 5 Theory Subjects: ";
        for (int i = 0; i < 5; i++) {
            cin >> marks_theory[i];
        }
    }
};

class P
