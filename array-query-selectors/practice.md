# 1.- Import the attached data file into a new collection (e.g exmoviestarts) in the boxOffice database

**With the next command:**

~~~m
mongoimport boxoffice-extended.json -d boxOffice -c exMovieStarts --jsonArray
~~~

**Output:**

~~~console
2022-11-08T21:16:52.324-0600    connected to: mongodb://localhost/
2022-11-08T21:16:52.421-0600    3 document(s) imported successfully. 0 document(s) failed to import.
~~~

# 2.- Find all movies with exactly two genres

**With the nex command:**

~~~m
db.exMovieStarts.find({genre: {$size: 2}})
~~~

**Output:**

~~~json
[
  {
    _id: ObjectId("636b1ba44365eecadb6ce043"),
    title: 'Teach me if you can',
    meta: { rating: 8, aired: 2014, runtime: 90 },
    visitors: 590378,
    expectedVisitors: 500000,
    genre: [ 'action', 'thriller' ],
    ratings: [ 8, 8 ]
  },
  {
    _id: ObjectId("636b1ba44365eecadb6ce044"),
    title: 'Supercharged Teaching',
    meta: { rating: 9.3, aired: 2016, runtime: 60 },
    visitors: 370000,
    expectedVisitors: 1000000,
    genre: [ 'thriller', 'action' ],
    ratings: [ 10, 9, 9 ]
  }
]
~~~

# 3.- Find all movies which aired in 2018

**With the nex command:**

~~~m
db.exMovieStarts.find({"meta.aired": 2018})
~~~

**Output:**

~~~json
[
  {
    _id: ObjectId("636b1ba44365eecadb6ce042"),
    title: 'The Last Student Returns',
    meta: { rating: 9.5, aired: 2018, runtime: 100 },
    visitors: 1300000,
    expectedVisitors: 1550000,
    genre: [ 'thriller', 'drama', 'action' ],
    ratings: [ 10, 9 ]
  }
]
~~~

# 4.- Find all movies which have ratings greater than 8 but lower than 10

**With the nex command:**

~~~m
db.exMovieStarts.find({ratings: {$elemMatch: {$gt: 8, $lt: 10}}})
~~~

**Output:**

~~~json
[
  {
    _id: ObjectId("636b1ba44365eecadb6ce042"),
    title: 'The Last Student Returns',
    meta: { rating: 9.5, aired: 2018, runtime: 100 },
    visitors: 1300000,
    expectedVisitors: 1550000,
    genre: [ 'thriller', 'drama', 'action' ],
    ratings: [ 10, 9 ]
  },
  {
    _id: ObjectId("636b1ba44365eecadb6ce044"),
    title: 'Supercharged Teaching',
    meta: { rating: 9.3, aired: 2016, runtime: 60 },
    visitors: 370000,
    expectedVisitors: 1000000,
    genre: [ 'thriller', 'action' ],
    ratings: [ 10, 9, 9 ]
  }
]
~~~

## What did you find most challenging and how did you overcome the challenge?

The most challenge in this practice is the number 4 and i overcome this practice checking the [MongoDB documetation](https://www.mongodb.com/docs/manual/reference/operator/query/elemMatch/) about $elemMatch operator.