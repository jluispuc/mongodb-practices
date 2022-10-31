# 1.- Relación Uno a Uno embebida

**With the next command:**

~~~m
mongoimport tv-shows.json -d movieData -c movies --jsonArray --drop
~~~

**Output:**

~~~console
2022-10-28T16:13:13.072-0500    connected to: mongodb://localhost/
2022-10-28T16:13:13.075-0500    dropping: movieData.movies
2022-10-28T16:13:13.136-0500    240 document(s) imported successfully. 0 document(s) failed to import.
~~~