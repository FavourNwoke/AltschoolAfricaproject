# AltschoolAfricaproject
Data Engineering Project work


# Definition of the Person class
# Attributes are :
# Name 
# idnumber 

class Person:
    def __init__(self, name, id_number):
        self.name = name
        self.id_number = id_number

    def __str__(self):
        return f"{self.name} ({self.id_number})"
    

# Definition of the Student class
# Attributes are :
# Name 
# id number
# Major

class Student(Person):
    def __init__(self, name, id_number, major):
        super().__init__(name, id_number)
        self.major = major

    def __str__(self):
        return f"{super().__str__()}, Major: {self.major}"
    
    
# Definition of the Instructor class
# Attributes are :
# Name 
# idnumber
# Department

class Instructor(Person):
    def __init__(self, name, id_number, department):
        super().__init__(name, id_number)
        self.department = department

    def __str__(self):
        return f"{super().__str__()}, Department: {self.department}"
    

# Definition of the Course class
#Attributes are :
# Course name
# Course id
# Enrolled Students

class Course:
    def __init__(self, course_name, course_id):
        self.course_name = course_name
        self.course_id = course_id
        self.enrolled_students = []

    def add_student(self, student):
        self.enrolled_students.append(student)
        
    def remove_student(self, student):
        self.enrolled_students.remove(student)

    def __str__(self):
        return f"{self.course_name} ({self.course_id}) - {len(self.enrolled_students)} students enrolled"
    

# Definition of the Enrollment class
# Attributes are :
# Student
# Course
# Grade

class Enrollment:
    def __init__(self, student, course):
        self.student = student
        self.course = course
        self.grade = None
        
    def assign_grade(self, grade):
        self.grade = grade

    def __str__(self):
        return f"{self.student.name} in {self.course.course_name} - Grade: {self.grade}"
    

# Definition of the StudentManagementSystem class
class StudentManagementSystem:
    def __init__(self):
        self.students = []
        self.instructors = []
        self.courses = []
        self.enrollments = []

    def add_student(self, student):
        self.students.append(student)

    def remove_student(self, student):
        self.students.remove(student)

    def add_instructor(self, instructor):
        self.instructors.append(instructor)

    def remove_instructor(self, instructor):
        self.instructors.remove(instructor)
        
    def add_course(self, course):
        self.courses.append(course)

    def remove_course(self, course):
        self.courses.remove(course)

    def enroll_student(self, student, course):
        self.enrollments.append(Enrollment(student, course))
        course.add_student(student)

    def assign_grade(self, student, course, grade):
     for enrollment in self.enrollments:
        if enrollment.student == student and enrollment.course == course:
            enrollment.assign_grade(grade)
            break


    def get_enrolled_students(self, course):
        return [enrollment.student for enrollment in self.enrollments if enrollment.course == course]

    def get_courses(self, student):
        return [enrollment.course for enrollment in self.enrollments if enrollment.student == student]
    

# Example
sms = StudentManagementSystem()

# Adding students, instructors, and courses
sms.add_student(Student("Sunkanmi Moses", "S12345", "DE"))
sms.add_student(Student("Favour Nwoke", "S67890", "Math"))
sms.add_instructor(Instructor("Professor Emmanuel", "I12345", "DE"))
sms.add_course(Course("Introduction to DE", "DE101"))

# Enrollment of students in courses
sms.enroll_student(sms.students[0], sms.courses[0])
sms.enroll_student(sms.students[1], sms.courses[0])

# Assigning grades
sms.assign_grade(sms.students[0], sms.courses[0], "B")
sms.assign_grade(sms.students[1], sms.courses[0], "A")

# Retrieving enrolled students and courses
print("Enrolled Students:")
for student in sms.get_enrolled_students(sms.courses[0]):
    print(student)

print("\nCourses for Student:")
for course in sms.get_courses(sms.students[0]):
    print(course)
