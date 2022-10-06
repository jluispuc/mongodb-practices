
# 1.- Insert 2 patient with at least 1 history entry per patient

**With the next command:**

~~~m
db.patients.insertMany(
  [{
        "firstName": "John",
        "lastName": "Sarmiento",
        "age": 18,
        "history": [{
                "disease": "Chronic Repiratory",
                "treatment": "Antibiotics"
            }
        ]
    }, {
        "firstName": "Magnus",
        "lastName": "Sarmiento",
        "age": 13,
        "history": [{
                "disease": "Infectious bronchitis",
                "treatment": "None"
            }
        ]
    }, {
        "firstName": "Carlsen",
        "lastName": "López",
        "age": 29,
        "history": [{
                "disease": "Coccidiosis",
                "treatment": "Sulfas"
            }
        ]
    }
  ])
~~~

**Output:**

![Figure 1](https://raw.githubusercontent.com/jluispuc/mongodb-practices/main/basic-crud-operations/figure1.png)

# 2.- Update patient data of 1 patient with new age, name and history entry

**With the next command:**

~~~m
db.patients.updateOne(
	{ _id: ObjectId("633d6eddec3f4e626baec02e") }, 
	{ 
		$set: { age: 21, name: 'Louis John' }, 
		$push: { 
      history: { 
        disease: 'Infectious bursitins',
        treatment: 'Vaccination' 
      }
		} 
	}
)
~~~
**Data updated:**
~~~json
[
  {
    _id: ObjectId("633d6eddec3f4e626baec02e"),
    firstName: 'John',
    lastName: 'Sarmiento',
    age: 21,
    history: [
      { disease: 'Chronic Repiratory', treatment: 'Antibiotics' },
      { disease: 'Infectious bursitins', treatment: 'Vaccination' }
    ],
    name: 'Louis John'
  }
]
~~~

> **Note:** Use **the $push operator** to push a new disease in the history array, check the docs [here](https://www.mongodb.com/docs/manual/reference/operator/update/push/).

# 3.- Find all patients who are older than 30 (or value of your choice)

**From data:**

~~~json
[
  {
    _id: ObjectId("633d6eddec3f4e626baec02e"),
    firstName: 'John',
    lastName: 'Sarmiento',
    age: 21,
    history: [
      { disease: 'Chronic Repiratory', treatment: 'Antibiotics' },
      { disease: 'Infectious bursitins', treatment: 'Vaccination' }
    ],
    name: 'Louis John'
  },
  {
    _id: ObjectId("633d6eddec3f4e626baec02f"),
    firstName: 'Magnus',
    lastName: 'Sarmiento',
    age: 13,
    history: [ { disease: 'Infectious bronchitis', treatment: 'None' } ]
  },
  {
    _id: ObjectId("633d6eddec3f4e626baec030"),
    firstName: 'Carlsen',
    lastName: 'López',
    age: 29,
    history: [ { disease: 'Coccidiosis', treatment: 'Sulfas' } ]
  }
]
~~~

**Exec the next command:**

```m
db.patients.find({age: {$gt:18}})
```

**Output:**

~~~json
[
  {
    _id: ObjectId("633d6eddec3f4e626baec02e"),
    firstName: 'John',
    lastName: 'Sarmiento',
    age: 21,
    history: [
      { disease: 'Chronic Repiratory', treatment: 'Antibiotics' },
      { disease: 'Infectious bursitins', treatment: 'Vaccination' }
    ],
    name: 'Louis John'
  },
  {
    _id: ObjectId("633d6eddec3f4e626baec030"),
    firstName: 'Carlsen',
    lastName: 'López',
    age: 29,
    history: [ { disease: 'Coccidiosis', treatment: 'Sulfas' } ]
  }
]
~~~

# 4.- Delete all patients who got a cold as disease

**From data:**

~~~json
[
  {
    _id: ObjectId("633d6eddec3f4e626baec02e"),
    firstName: 'John',
    lastName: 'Sarmiento',
    age: 21,
    history: [
      { disease: 'Chronic Repiratory', treatment: 'Antibiotics' },
      { disease: 'Infectious bursitins', treatment: 'Vaccination' }
    ],
    name: 'Louis John'
  },
  {
    _id: ObjectId("633d6eddec3f4e626baec02f"),
    firstName: 'Magnus',
    lastName: 'Sarmiento',
    age: 13,
    history: [ { disease: 'Infectious bronchitis', treatment: 'None' } ]
  },
  {
    _id: ObjectId("633d6eddec3f4e626baec030"),
    firstName: 'Carlsen',
    lastName: 'López',
    age: 29,
    history: [ { disease: 'Coccidiosis', treatment: 'Sulfas' } ]
  }
]
~~~

**Exec the next command:**

```m
db.patients.deleteMany({"history.disease": { $eq: "Infectious bursitins"}})
```

**New collection data:**

~~~json
[
  {
    _id: ObjectId("633d6eddec3f4e626baec02f"),
    firstName: 'Magnus',
    lastName: 'Sarmiento',
    age: 13,
    history: [ { disease: 'Infectious bronchitis', treatment: 'None' } ]
  },
  {
    _id: ObjectId("633d6eddec3f4e626baec030"),
    firstName: 'Carlsen',
    lastName: 'López',
    age: 29,
    history: [ { disease: 'Coccidiosis', treatment: 'Sulfas' } ]
  }
]
~~~

## What did you find most challenging and how did you overcome the challenge?

The most challenge in this practice is the number 2: update patient data of 1 patient with new age, name and history entry, and i overcome this practice checking the MongoDB documetation where talk about push a new element in array, you can see [here](https://www.mongodb.com/docs/manual/reference/operator/update/push/).
