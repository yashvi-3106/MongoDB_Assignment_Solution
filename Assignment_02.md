# Creating Database
```javascript
 Use CodingGitaDB  
 ```

## Creating Collection
``` javascript 
db.createCollection("students");
```

``` javascript 
db.createCollection("subjects");
```

### Inserting data in student collection
```javascript
db.students.insertMany([
  { 
    "name": "Jenil",
    "rollNumber": 101,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS", "MongoDB"]
  },
  { 
    "name": "Mahir",
    "rollNumber": 102,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS"]
  },
  { 
    "name": "Arjun",
    "rollNumber": 103,
    "department": "Electrical Engineering",
    "year": 3,
    "subjectsEnrolled": ["Circuit Theory", "Electrical Machines"]
  }
]);
```

### Inserting data in subject collection
```javascript 
 db.subjects.insertMany([
  { 
    "subjectName": "React",
    "topics": [
      "JSX", 
      "Components", 
      "State", 
      "Props", 
      "Hooks"
    ]
  },
  { 
    "subjectName": "NodeJS", 
    "topics": [
      "Modules", 
      "Express", 
      "File System", 
      "Asynchronous Programming"
    ]
  },
  { 
    "subjectName": "MongoDB", 
    "topics": [
      "Database Design", 
      "CRUD Operations", 
      "Aggregation", 
      "Indexes"
    ]
  }
]);
```

### finding all students in the Computer Science department:
```javascript  
db.students.find({ "department": "Computer Science" });
```

### finding all the students who are in year 2:
```javascript
db.students.find({ "year": 2 });
```

### finding all students enrolled in the React subject:
```javascript
db.students.find({ "subjectsEnrolled": "React" });
```

### finding the subject which contains the topic "Hooks":
```javascript
db.subjects.find({ "topics": "Hooks" });
```

### Add a subject, MongoDB, for Mahir:
```javascript
db.students.updateOne(
  { "name": "Mahir" },
  { $push: { "subjectsEnrolled": "MongoDB" } }
);
```

### Updating Arjun's student year
```javascript
db.students.updateOne(
  { "name": "Arjun" },
  { $set: { "year": 4 } }
);
```

### Adding new topic to a subject
```javascript
db.subjects.updateOne(
  { "subjectName": "React" },
  { $push: { "topics": "Advanced Hooks" } }
);
```

### Delete a student record
```javascript
db.students.deleteOne({ "name": "Arjun" });
```

### Delete a MongoDB subject
```javascript
db.subjects.deleteOne({ "subjectName": "MongoDB" });
```

### Task 1: Add multiple students
#### Insert at least 5 students into the students collection with unique roll numbers, names, departments, years, and subjects enrolled.

```javascript
db.students.insertMany([
  { 
    "name": "Yashvi",
    "rollNumber": 104,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS", "MongoDB","Angular"]
  },
  { 
    "name": "Veer",
    "rollNumber": 105,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS"]
  },
  { 
    "name": "Kalpan",
    "rollNumber": 106,
    "department": "Electrical Engineering",
    "year": 3,
    "subjectsEnrolled": ["Circuit Theory", "Electrical Machines"]
  },
 { 
    "name": "Ishita",
    "rollNumber": 107,
    "department": "Electrical Engineering",
    "year": 3,
    "subjectsEnrolled": ["Circuit Theory", "Electrical Machines"]
  },
    { 
    "name": "Isha",
    "rollNumber": 108,
    "department": "Computer Science",
    "year": 2,
    "subjectsEnrolled": ["React", "NodeJS", "MongoDB","Angular"]
  }
]);
```

### Task 2: Add multiple subjects
#### Insert 4 subjects into the subjects collection, each with 3 to 5 topics.

```javascript
db.subjects.insertMany([
  {
    subjectName: "C Programming",
    topics: ["Operators", "Conditional Statement", "Loops", "Arrays"]
  },
  {
    subjectName: "JavaScript",
    topics: ["Operators", "Loops", "Arrays", "Asynchronous"]
  },
  {
    subjectName: "HTML",
    topics: ["Tags", "Elements", "Tables", "Forms"]
  },
  {
    subjectName: "C++",
    topics: ["Function", "Structure", "Algorithm", "Vector"]
  }
]);
```

### Task 3: Query students based on subject enrollment
#### Query the students collection to find all students who are enrolled in NodeJS.

```javascript
db.students.find({ "subjectsEnrolled:" "NodeJS" });
```

### Task 4: Add a new topic to a subject
#### Add a new topic to the NodeJS subject.

```javascript
db.subjects.updateOne(
  { "subjectName": "NodeJS" },
  { $push: { "topics": "WebSockets" } }
);
```

### Task 5: Query subjects with multiple topics
#### Query the subjects collection to find subjects that contain at least 4 topics.

```javascript
db.subjects.find({ "topics.3": { $exists: true } });

db.subjects.find({
  $expr: { $gte: [{ $size: "$topics" }, 4] }
})
```

### Task 6: Update student enrollment
#### Add the subject "React Native" to Jenil's subjects.

```javascript
db.students.updateOne(
  { name: "Jenil" },
  { $push: { subjectsEnrolled: "C++" } }
);
```

### Task 7: Query all students
#### Query all students in the database and print out their names and enrolled subjects.

```javascript
db.students.find({}, { name: 1, subjectsEnrolled: 1 });
```

### Task 8: Update multiple students' year
#### Update the year for all students in the Computer Science department to year 3.

```javascript
db.students.updateMany(
  { department: "Computer Science" },
  { $set: { year: 3 } }
);
```

### Task 9: Add new topics to multiple subjects
#### Add new topics to React, NodeJS, and MongoDB subjects. Ensure each subject gets at least one new topic.

```javascript
db.subjects.updateMany(
  { subjectName: { $in: ["React", "NodeJS", "MongoDB"] } },
  {
    $push: {
      topics: {
        $each: [
          "Context API",  // Topic for React
          "WebSockets",    // Topic for NodeJS
          "Replication"    // Topic for MongoDB
        ]
      }
    }
  }
);
```

### Task 10: Remove a topic from a subject
#### Remove the topic "Express" from the NodeJS subject.

```javascript
db.subjects.updateOne(
  { subjectName: "NodeJS" },
  { $pull: { topics: "Express" } }
);

```
### Task 11: Query all students in a specific year
#### Query and return all students in year 2 or year 3.

```javascript
db.students.find({ year: { $in: [2, 3] } });
```

### Task 12: Delete a student by roll number
#### Delete a student from the database using their roll number.

```javascript
db.students.deleteOne({ rollNumber: "101" });
```

### Task 13: Delete all students from a department
#### Delete all students who belong to the Electrical Engineering department.

```javascript
db.students.deleteMany({ department: "Electrical Engineering" });
```

### Task 14: Retrieve all topics for a subject
#### Query the NodeJS subject and retrieve all topics listed for it.

```javascript
db.subjects.findOne({ subjectName: "NodeJS" }, { topics: 1 });
```

### Task 15: Count the number of subjects in which a student is enrolled
#### Write a query that returns the number of subjects each student is enrolled in.

```javascript
db.students.aggregate([
  {
    $project: {
      name: 1,  
      subjectsCount: { $size: "$subjectsEnrolled" }  
    }
  }
]);
```