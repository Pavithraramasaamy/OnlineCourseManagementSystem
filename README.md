### Objective:
Simulate a system design interview by applying core OOP concepts to design and implement an object-oriented 
model for a real-world use case.

## Task 1: UML Class Diagram:

<img width="1024" height="1536" alt="UML" src="https://github.com/user-attachments/assets/3ff54c9f-9ff3-44cd-ac9e-bf3ebfedb63f" />


## Task 2: JavaScript Code / Pseudocode:
```

class User {
  constructor(id, name, email) {
    this._id = id;
    this._name = name;
    this._email = email;
  }

  login() {
    console.log(`${this._name} logged in.`);
  }

  get email() {
    return this._email;
  }

  set email(newEmail) {
    this._email = newEmail;
  }
}

class Student extends User {
  constructor(id, name, email) {
    super(id, name, email);
    this.enrolledCourses = [];
    this.grades = [];
  }

  enroll(course) {
    course.addStudent(this);
    this.enrolledCourses.push(course);
  }

  uploadAssignment(course, assignmentId, file) {
    const assignment = course.getAssignmentById(assignmentId);
    assignment.submit(this, file);
  }

  viewGrades() {
    return this.grades;
  }

  login() {
    console.log(`Student ${this._name} logged in.`);
  }
}

class Instructor extends User {
  constructor(id, name, email) {
    super(id, name, email);
    this.teachingCourses = [];
  }

  createCourse(courseId, title) {
    const course = new Course(courseId, title, this);
    this.teachingCourses.push(course);
    return course;
  }

  gradeAssignment(course, assignmentId, student, grade) {
    const assignment = course.getAssignmentById(assignmentId);
    assignment.grade(student, grade);
  }

  login() {
    console.log(`Instructor ${this._name} logged in.`);
  }
}

class Course {
  constructor(courseId, title, instructor) {
    this.courseId = courseId;
    this.title = title;
    this.instructor = instructor;
    this.students = [];
    this.assignments = [];
  }

  addStudent(student) {
    this.students.push(student);
  }

  addAssignment(assignment) {
    this.assignments.push(assignment);
  }

  getAssignmentById(id) {
    return this.assignments.find(a => a.assignmentId === id);
  }
}

class Assignment {
  constructor(assignmentId, title) {
    this.assignmentId = assignmentId;
    this.title = title;
    this.submissions = new Map(); 
    this.grades = new Map(); 
  }

  submit(student, file) {
    this.submissions.set(student, file);
  }

  grade(student, score) {
    this.grades.set(student, score);
    student.grades.push({ assignment: this, score });
  }
}

```

## Task 3: OOP Design Explanation:

## Abstraction:
We modeled real-world entities like User, Student, Instructor, Course, and Assignment with meaningful behaviors (methods) and data (properties).

## Encapsulation:
We used private properties (e.g., _email) and public getter/setter methods to control access.

## Inheritance:
Student and Instructor inherit from the User class to reuse common properties and methods.

## Polymorphism:
Method overriding is shown in the login() method of Student and Instructor, providing role-specific behavior.

## SOLID Principles Followed

S: Single Responsibility Principle – Each class has a clear and single responsibility.

O: Open/Closed Principle – You can add more user types (e.g., Admin) without changing existing code.

L: Liskov Substitution Principle – Subclasses can be used wherever the superclass is expected.

I: Interface Segregation – Not explicitly used in JS, but behavior is role-specific.

D: Dependency Inversion – Could be enhanced by injecting dependencies (e.g., course repository), but for simplicity, not applied here.

