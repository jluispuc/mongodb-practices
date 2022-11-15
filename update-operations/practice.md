# 1.- Create a new collection ("Sports") and upsert two new documents into it (with these fields: "title", "requiresTeam")

**With the next command:**

~~~m
db.sports.updateOne({title: "Basketball"}, {$set: {requiresTeam: true}}, {upsert: true})
db.sports.updateOne({title: "Box"}, {$set: {requiresTeam: false}}, {upsert: true})
~~~

# 2.- Update all documents which do require a team by adding a new field with the minimum amount of players required

**With the nex command:**

~~~m
db.sports.updateMany({requiresTeam: true}, {$set: {minimumPlayers: 6}})
~~~

# 3.- Update all documents that require a team by incresing the numbers of players by 10

**With the nex command:**

~~~m
db.sports.updateOne({requiresTeam: true}, {$inc: {minimumPlayers: 10}})
~~~