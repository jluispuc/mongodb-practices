# 1.- Pick 3 Points on Google Maps and store them in collection

**With the next command:**

~~~m
db.places.insertMany(
  [
    {
        "name": "My Home",
        "location": {
            "type": "Point",
            "coordinates": [
                -90.739854,
                18.601630
            ]
        }
    },
    {
        "name": "Iglesia a donde iban los abuelos paternos",
        "location": {
            "type": "Point",
            "coordinates": [
                -90.7402365,
                18.6018288
            ]
        }
    },
    {
        "name": "Moms home",
        "location": {
            "type": "Point",
            "coordinates": [
                -90.757534,
                18.616181
            ]
        }
    }
  ])
~~~
# 2.- Pick a point and find the nearest points within a min and max distance

**With the next command:**

~~~m
db.places.find({
    location:{
        $near:{
            $geometry:{
                type:"Point",
                coordinates:[
                    -90.7506614,18.6114385
                ]
            }, 
            $maxDistance: 1000, 
            $minDistance: 500
        }
    }
})
~~~

Al ejecturar el comando me lanzó el siguiente error:

~~~bash
Uncaught: MongoServerError: error processing query: ns=awesomeplaces.placesTree: GEONEAR field=location maxdist=1.79769e+308 isNearSphere=0
Sort: {}
Proj: {}
 planner returned error :: caused by :: unable to find index for $geoNear query
~~~

Entonces cree el index para $geoNear query y después me permitió buscar ubicaciones cerca del punto.

~~~m
db.places.createIndex({location: "2dsphere"})
~~~
# 3.- Pick an area and see which points (that are stored in your collection) it contains

**With the next command:**

~~~m
const p1 = [-90.744560, 18.604723]
const p2 = [-90.739517, 18.604213]
const p3 = [-90.740464, 18.597833]
const p4 = [-90.745481, 18.598197]

db.places.find({
    location:{
        $geoWithin:{
            $geometry:{
                type:"Polygon",
                coordinates:[
                    [
                        p1,
                        p2,
                        p3,
                        p4,
                        p1
                    ]
                ]
            }
        }
    }
})
~~~
# 4.- Store at least one area in a different collection

**With the next command:**

~~~m
db.areas.insertOne({
    "name": "Area 1",
    "area": {
        type:"Polygon",
        coordinates:[
            [
                p1,
                p2,
                p3,
                p4,
                p1
            ]
        ]
    }
})
~~~

# 5.- Pick a point and find out which areas in your collection contain that point

**With the next command:**

~~~m
db.areas.find({
    area:{
        $geoIntersects:{
            $geometry:{
                type:"Point",
                coordinates:[
                    -90.7402365,
                    18.6018288
                ]
            }
        }
    }
})
~~~