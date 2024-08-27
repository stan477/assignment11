# assignment11

# The Student class represents a student with an ID, name, age, and major
class Student:
    # The __init__ method is the constructor that initializes the student's attributes
    def __init__(self, id: int, name: str, age: int, major: str):
        self.id = id
        self.name = name
        self.age = age
        self.major = major

    # The update method allows you to update the student's name, age, and major
    def update(self, name=None, age=None, major=None):
        if name:
            self.name = name
        if age:
            self.age = age
        if major:
            self.major = major

    # The display method prints the student's information
    def display(self):
        print(f"ID: {self.id}, Name: {self.name}, Age: {self.age}, Major: {self.major}")

# The StudentDatabase class manages a list of students
class StudentDatabase:
    # The __init__ method initializes an empty list of students
    def __init__(self):
        self.students = []

    # The add_student method adds a new student to the database
    def add_student(self, student: Student):
        self.students.append(student)

    # The remove_student method removes a student from the database by their ID
    def remove_student(self, student_id: int):
        self.students = [s for s in self.students if s.id != student_id]

    # The display_all method prints the information of all students in the database
    def display_all(self):
        for student in self.students:
            student.display()

# The StudentManagementSystem class provides an interface for managing students
class StudentManagementSystem:
    # The __init__ method initializes an empty list of students and a StudentDatabase instance
    def __init__(self):
        self.students = []
        self.database = StudentDatabase()

    # The add_student method creates a new Student object and adds it to the database
    def add_student(self, id: int, name: str, age: int, major: str):
        student = Student(id, name, age, major)
        self.students.append(student)
        self.database.add_student(student)

    # The update_student method finds the student with the given ID and updates their information
    def update_student(self, student_id: int, name: str = None, age: int = None, major: str = None):
        for student in self.students:
            if student.id == student_id:
                student.update(name, age, major)
                self.database.add_student(student)
                break

    # The delete_student method removes the student with the given ID from the system and the database
    def delete_student(self, student_id: int):
        for student in self.students:
            if student.id == student_id:
                self.students.remove(student)
                self.database.remove_student(student_id)
                break

    # The show_all_students method displays the information of all students in the database
    def show_all_students(self):
        self.database.display_all()

# The main function provides a simple command-line interface for the student management system
def main():
    system = StudentManagementSystem()

    while True:
        print("Student Management System")
        print("1. Add Student")
        print("2. Update Student")
        print("3. Delete Student")
        print("4. View All Students")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == "1":
            id = int(input("Enter student ID: "))
            name = input("Enter student name: ")
            age = int(input("Enter student age: "))
            major = input("Enter student major: ")
            system.add_student(id, name, age, major)
            print("Student added successfully.")

        elif choice == "2":
            id = int(input("Enter student ID: "))
            name = input("Enter new name (or leave blank): ")
            age = input("Enter new age (or leave blank): ")
            major = input("Enter new major (or leave blank): ")
            system.update_student(id, name or None, int(age) if age else None, major or None)
            print("Student information updated.")

        elif choice == "3":
            id = int(input("Enter student ID: "))
            system.delete_student(id)
            print("Student deleted.")

        elif choice == "4":
            system.show_all_students()

        elif choice == "5":
            print("Exiting Student Management System...")
            break

        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
