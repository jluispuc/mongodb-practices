# 1.- Import the attached data into a new database (e.g. boxOffice) and collection (e.g movieStarts)

**With the next command:**

~~~m
mongoimport boxoffice.json -d boxOffice -c movieStarts --jsonArray --drop
~~~

# 2.- Search all movies that have a rating higher than 9.2 and a runtime lower than 100 minutes

**With the nex command:**

~~~m
 db.movieStarts.find({$and: [{"meta.rating": {$gt: 9.2}}, {"meta.runtime": {$lt: 100}}]})
~~~

**Output:**

~~~json
[
  {
    _id: ObjectId("6368f88a991e6c305d4783ce"),
    title: 'Supercharged Teaching',
    meta: { rating: 9.3, aired: 2016, runtime: 60 },
    visitors: 370000,
    expectedVisitors: 1000000,
    genre: [ 'thriller', 'action' ]
  }
]
~~~

# 3.- Search all movies that have un genre of "drama" or "action"

**With the nex command:**

~~~m
 db.movieStarts.find({genre: {$in: ["drama", "action"]}})
~~~

**Output:**

~~~json
[
  {
    _id: ObjectId("6368f88a991e6c305d4783cc"),
    title: 'The Last Student Returns',
    meta: { rating: 9.5, aired: 2018, runtime: 100 },
    visitors: 1300000,
    expectedVisitors: 1550000,
    genre: [ 'thriller', 'drama', 'action' ]
  },
  {
    _id: ObjectId("6368f88a991e6c305d4783cd"),
    title: 'Teach me if you can',
    meta: { rating: 8.5, aired: 2014, runtime: 90 },
    visitors: 590378,
    expectedVisitors: 500000,
    genre: [ 'action', 'thriller' ]
  },
  {
    _id: ObjectId("6368f88a991e6c305d4783ce"),
    title: 'Supercharged Teaching',
    meta: { rating: 9.3, aired: 2016, runtime: 60 },
    visitors: 370000,
    expectedVisitors: 1000000,
    genre: [ 'thriller', 'action' ]
  }
]
~~~

# 4.- Search all movies where visitors exceeded expectedVisitors

**With the nex command:**

~~~m
 db.movieStarts.find({$expr: {$gt: ["$visitors", "$expectedVisitors"]}})
~~~

**Output:**

~~~json
[
  {
    _id: ObjectId("6368f88a991e6c305d4783cd"),
    title: 'Teach me if you can',
    meta: { rating: 8.5, aired: 2014, runtime: 90 },
    visitors: 590378,
    expectedVisitors: 500000,
    genre: [ 'action', 'thriller' ]
  }
]
~~~