# Assignment_03

### Create Database

```js
use codinggitadatabase
```

### Create Collection

```js

db.createCollection("students");
db.createCollection("courses");

```

### Task 1: Add more students to the students collection
- Add at least 5 new students to the students collection with unique names, roll numbers, and course enrollments.

```js
db.students.insertMany([
  {
    "name": "Priya",
    "rollNumber": "CS1006",
    "department": "IT",
    "year": 2,
    "coursesEnrolled": ["CS201", "MATH202"]
  },
  {
    "name": "Nina",
    "rollNumber": "CS1007",
    "department": "ECE",
    "year": 3,
    "coursesEnrolled": ["ECE301", "MATH303"]
  },
  {
    "name": "Karan",
    "rollNumber": "CS1008",
    "department": "CSE",
    "year": 1,
    "coursesEnrolled": ["CS101", "MATH101"]
  },
  {
    "name": "Anjali",
    "rollNumber": "CS1009",
    "department": "IT",
    "year": 2,
    "coursesEnrolled": ["CS202", "MATH202"]
  },
  {
    "name": "Sanjay",
    "rollNumber": "CS1010",
    "department": "ECE",
    "year": 1,
    "coursesEnrolled": ["ECE101", "MATH101"]
  },
  {
    "name": "Amit",
    "rollNumber": "CS1011",
    "department": "CSE",
    "year": 2,
    "coursesEnrolled": ["CS202", "MATH202", "PHY201"]
  },
  {
    "name": "Sita",
    "rollNumber": "CS1012",
    "department": "IT",
    "year": 3,
    "coursesEnrolled": ["CS301", "MATH303", "CS302"]
  },
  {
    "name": "Vikram",
    "rollNumber": "CS1013",
    "department": "ECE",
    "year": 2,
    "coursesEnrolled": ["ECE201", "MATH202", "PHY201"]
  },
  {
    "name": "Ravi",
    "rollNumber": "CS1014",
    "department": "CSE",
    "year": 3,
    "coursesEnrolled": ["CS401", "MATH404"]
  },
  {
    "name": "Isha",
    "rollNumber": "CS1015",
    "department": "IT",
    "year": 1,
    "coursesEnrolled": ["CS101", "MATH101", "ENG101"]
  }
]
)

```

### Task 2: Add more courses to the courses collection

```js
db.courses.insertOne({	
"courseCode": "CS202",
"name": "Data Structures",
"credits": "3",
"instructor": "Prof. Krishna"
})

```

### Task 3: Fetch a specific student's record by roll number
- Use find() to fetch a student's information using their roll number (CS1002).

```js
db.students.find({"rollNumber": "CS1002"})
```

### Task 4: Query all students who are enrolled in a particular course
- Retrieve all students who are enrolled in "MATH101".

```js
db.students.find({"coursesEnrolled": "MATH101"})
```

### Task 5: Update a student's courses
-Update the student with roll number CS1001 to enroll in an additional course "CS202".

```js
db.students.updateOne({ 
"rollNumber": "CS1001"},
{ $push: {"coursesEnrolled": "CS202"}}
);
```

### Task 6: Remove a course from a student's courses list
-Remove the course MATH101 from the student Mahir's list of enrolled courses.

```js
db.students.updateOne(
  { name: "Mahir" },
  { $pull: { coursesEnrolled: "MATH101" } }
);
```

### Task 7: Find all courses with 3 credits
- Query the courses collection to find all courses where the credits field equals 3.

```js
db.courses.find({ "credits": 3});
```

### Task 8: Find students who have enrolled in more than 2 courses
- Use $size operator to query students who are enrolled in more than 2 courses.

```js
db.students.find({ $expr: { $gt: [{ $size: "$coursesEnrolled"}, 2]}});
```

### Task 9: Use the $in operator to find students enrolled in multiple courses
- Use the $in operator to find students who are enrolled in either CS101 or MATH202.

```js
db.students.find({ coursesEnrolled: { $in: ["CS101", "MATH202"] } });
```

### Task 10: Fetch all students from a specific department (e.g., CSE)
- Use a query to find all students in the CSE department.

```js
db.students.find({"department": "CSE"});
```

### Task 11: Query students who are in their 3rd year
- Retrieve students who are in the 3rd year using the year field.

```js
db.students.find({"year": 3});
```

### Task 12: Query students using a range for their year
- Find all students who are in 2nd or 3rd year by using the $gte operator.

```js
db.students.find({ year: { $gte: 2, $lte: 3 } });
```

### Task 13: Count the total number of students in each department
- Use the $group stage of aggregation to group students by department and count them.

```js
db.students.aggregate([
  {
    $group: {
      _id: "$department",  
      studentCount: { $sum: 1 }  
  }
  }
]);
```

### Task 14: Group courses by credits
- Group courses by their credit value and count how many courses there are for each credit value.

```js
db.courses.aggregate([
  { $group: {
    _id: "$credits",
    coursesCount: { $sum: 1}
  }
}
])
```

### Task 15: Find the highest credit course
- Query for the course with the highest number of credits using the $sort operator.

```js
db.courses.find().sort({ credits: -1 }).limit(1);
```

### Task 16: Use the $and operator for filtering students
- Find all students who belong to the CSE department and are enrolled in more than 2 courses.

```js
db.students.find({
  $expr: {
    $and: [
      { $eq: ["$department", "CSE"] },
      { $gt: [{ $size: "$coursesEnrolled" }, 2] }
    ]
  }
});
```

### Task 17: Add a new field to all documents in the students collection
- Add a new field activeStatus and set it to true for all students.

```js
db.students.updateMany(
  {},
  { $set: { activeStatus: true } }
);
```

###  Task 18: Use $rename to rename a field
- Rename the coursesEnrolled field in the students collection to enrolledCourses.

```js
db.students.updateMany(
  {},
  { $rename: { "coursesEnrolled": "enrolledCourses" } }
);
```

### Task 19: Set default values for new fields in all student documents
- Add a field graduationYear with a default value for all students.

```js
db.students.updateMany(
  {},
  { $set: { graduationYear: 2025 } }
);
```

### Task 20: Use the $push operator to add a new course to a student’s course list
- Add the course "CS303" to Mahir’s coursesEnrolled list.

```js
db.students.updateOne(
  { name: "Mahir" },
  { $push: { enrolledCourses: "CS303" } }
);
```

### Task 21: Use $pull to remove a course from a student's courses list
- Remove the course CS101 from Jenil’s list.

```js
db.students.updateOne(
  { name: "Jenil" },
  { $pull: { enrolledCourses: "CS101" } }
);
```

### Task 22: Remove a student from the students collection
- Delete the student record with roll number CS1004.

```js
db.students.deleteOne({ rollNumber: "CS1004" });
```

### Task 23: Find students who are enrolled in both CS101 and MATH202
- Use $all operator to find students who are enrolled in both courses.

```js
db.students.find({
  enrolledCourses: { $all: ["CS101", "MATH202"] }
});
```

### Task 24: Use $regex to search for students whose name starts with "A"
- Use regular expressions to search for students whose names begin with the letter "A".

```js
db.students.find({
  name: { $regex: "^A" }
});

```

### Task 25: Use $exists to find students with enrolled courses
- Query students who have an entry in the coursesEnrolled array.

```js
db.students.find({
 enrolledCourses: { $exists: true }
});

```

### Task 26: Add a field to store students' grades for each course
- Add a new field grades to the students collection and store an array of grades for each course.

```js
  db.students.updateOne(
  {name: "Jenil"},
  {$set: {grades: ["A","B","C","D"]}}
);
```
- same for other students

### Task 27: Use $elemMatch to query students enrolled in specific courses
- Find students enrolled in CS101 and have the grade A.

```js
  db.students.find({
  $and: [
    { enrolledCourses: "CS202" }, 
    { grades: "A" }             
  ]
});
```

### Task 28: Use $size operator to query students with exactly 2 courses enrolled
- Query students who have enrolled in exactly two courses.

```js
  db.students.find({
  enrolledCourses: { $size: 2 }
});
```

### Task 29: Perform a text search for a course title
- Use text indexing to search for the course Digital Electronics in the courses collection.

```js
db.courses.createIndex({name: "text"});
            
db.courses.find({$text: {$search: "Digital Electronics"}} );
```

### Task 30: Create a compound index on department and year
- Create a compound index on the fields department and year for better querying performance.

```js
db.students.createIndex({department: 1, year: 1}  );

db.students.find(
                  {department: "CSE", year: 2}
                 );
```

### Task 31: Use $sort to order students by their roll number
- Sort the students in ascending order of their roll number.

```js
  db.students.find().sort({rollNumber: 1});
```

### Task 32: Create a unique index on the roll number
- Create a unique index to ensure that the roll numbers in the students collection are unique.

```js
db.students.createIndex( {rollNumber: 1} , {unique: true} );
```

### Task 33: Update the course name in the courses collection
- Update the name of the course CS101 to Intro to Programming.

```js
db.courses.updateOne( { name: "CS101"}, { $set: {name: "Intro to Programing"}});
```

### Task 34: Create a backup of the CodingGitaStudents database
- Use mongodump to back up the entire CodingGitaStudents database.

```js

```

### Task 35: Restore the CodingGitaStudents database from the backup
- Use mongorestore to restore the database after a backup.

```js

```

### Task 36: Use $project to reshape data in aggregation
- Project only the name and department of students using an aggregation query.

```js
db.students.aggregate([
{ $project: { name: 1, department: 1, _id: 0 } }
]);
```

### Task 37: Use $unwind to deconstruct the courses array
- Use $unwind to split the coursesEnrolled array into individual documents.

```js
db.students.aggregate([
{ $unwind: "$enrolledCourses" }
]);
```

### Task 38: Use $limit to retrieve only the first 3 students
- Use $limit to limit the result to the first 3 students in the students collection.

```js
db.students.find().limit(3);
```

### Task 39: Use $skip to skip the first 2 students and get the rest
- Use $skip to fetch all students except the first two.

```js
db.students.find().skip(2);
```

### Task 40: Use $lookup to join student data with courses
- Use $lookup to fetch the course information for students.

```js
db.students.aggregate([
{
  $lookup: {
    from: "courses",
    localField: "enrolledCourses",
    foreignField: "courseCode",
    as: "courseDetails"
  }
}
]);
```

### Task 41: Create a new collection for storing studentFeedback
- Create a collection studentFeedback with fields: studentRollNumber, feedbackText, date.

```js
db.createCollection("studentFeedback");
db.studentFeedback.insertMany([
{ studentRollNumber: "CS1001", feedbackText: "Can do Better", date: new Date() },
{ studentRollNumber: "CS1002", feedbackText: "Excellent", date: new Date() },
{ studentRollNumber: "CS1003", feedbackText: "Needs Improvement", date: new Date() },
{ studentRollNumber: "CS1004", feedbackText: "Outstanding", date: new Date() }
]);
```

### Task 42: Query the studentFeedback collection to find feedback from a specific student
- Use find() to retrieve feedback from Jenil.

```js
db.studentFeedback.find({ studentRollNumber: "CS1001" });
```

### Task 43: Use $set to update multiple fields at once
- Use the $set operator to update the department and coursesEnrolled fields for Arjun.

```js
db.students.updateOne(
{ name: "Arjun" },
{ $set: { department: "ECE", enrolledCourses: ["CS202", "MATH303"] } }
);
```

### Task 44: Create a custom index on the coursesEnrolled field
- Create an index on the coursesEnrolled array for faster querying.

```js
db.students.createIndex({ coursesEnrolled: 1 });
```

### Task 45: Perform a query on nested documents in students collection
- Query for students who have grades A in their courses.

```js
db.students.find({ grades: { $elemMatch: { grade: "A" } } });
```