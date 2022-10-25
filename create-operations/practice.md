# 1.- Insert multiple companies (company data of your choice) into a collection (use insertOne() and insertMany())

**With the next command:**

~~~m
db.companies.insertMany(
[
    {
        "name": "Sofware house Mérida",
        "address": "Calle 18 #192H Col, entre 13 y 15, García Ginerés, 97070 Mérida, Yuc.",
        "telephone": "9994065457",
        "website": "https://www.shmerida.mx/"
    },
    {
        "name": "Aluxoft Research & Development",
        "address": "Calle 25 No. 384-K x 40 y 42, Nivel 2 depto. 210, Montejo, 97109 Mérida, Yuc.",
        "telephone": "9992855005"
    }
])
~~~

**Output:**

~~~json
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("6357c35a37cd89ebe761d230"),
    '1': ObjectId("6357c35a37cd89ebe761d231")
  }
}
~~~

**Use insertOne()**

~~~m
db.companies.insertOne(
    {
        "name": "Software Connex",
        "address": "Calle 7B #306E, entre 12A y 12B, Santa Gertrudis Copo, 97305 Mérida, Yuc.",
        "telephone": "9994224561"
    }
)
~~~

**Output:**

~~~json
{
  acknowledged: true,
  insertedId: ObjectId("6357c37737cd89ebe761d232")
}
~~~

# 2.- Deliberately insert duplicate ID data and "fix" failing additions with unordered inserts.

**With the next command:**

~~~m
db.companies.insertMany(
[
    {
        _id: ObjectId("6357c37737cd89ebe761d232"),
        "name": "Nova-Develop",
        "address": "62 Nº529A, entre 187D y 189, 97290 Mérida, Yuc.",
        "telephone": "999 605 6475"
    },
    {
        "name": "Dev Design Apps & Software",
        "address": "Calle 21 S/N x 18 y 20, Cholul, 97305 Mérida, Yuc.",
        "telephone": "999 287 7618"
    },
    {
        "name": "Lighthouse Technologies",
        "address": "Calle 72 487 Centro, segundo piso, 97000 Mérida, Yuc.",
        "telephone": "55 7210 5171"
    }
])
~~~

**Output:**

~~~console
Uncaught:
MongoBulkWriteError: E11000 duplicate key error collection: companyDirectory.companies index: _id_ dup key: { _id: ObjectId('6357c37737cd89ebe761d232') }
Result: BulkWriteResult {
  result: {
    ok: 1,
    writeErrors: [
      WriteError {
        err: {
          index: 0,
          code: 11000,
          errmsg: "E11000 duplicate key error collection: companyDirectory.companies index: _id_ dup key: { _id: ObjectId('6357c37737cd89ebe761d232') }",
          errInfo: undefined,
          op: {
            _id: ObjectId("6357c37737cd89ebe761d232"),
            name: 'Nova-Develop',
            address: '62 Nº529A, entre 187D y 189, 97290 Mérida, Yuc.',
            telephone: '999 605 6475'
          }
        }
      }
    ],
    writeConcernErrors: [],
    insertedIds: [
      { index: 0, _id: ObjectId("6357c37737cd89ebe761d232") },
      { index: 1, _id: ObjectId("6357c69737cd89ebe761d233") },
      { index: 2, _id: ObjectId("6357c69737cd89ebe761d234") }
    ],
    nInserted: 0,
    nUpserted: 0,
    nMatched: 0,
    nModified: 0,
    nRemoved: 0,
    upserted: []
  }
}
~~~

**Fix with unordered inserts:**

~~~m
db.companies.insertMany(
    ...,
    {
        ordered: false
    }
)
~~~

This trigger the same error but now in the data "nInserted" should show "2".

# 2.- Write data for a new company with both journaling being aguaranteed and not being guaranteed.

**With the next command to being aguaranteed:**

~~~m
db.companies.insertOne(
    {
        "name": "Yucaweb",
        "address": "999 331 9831",
        "website": "https://yucaweb.mx/"
    },
    {
        writeConcern: {
            j: true
        }
    }
)
~~~

**Output:**

~~~console
{
  acknowledged: true,
  insertedId: ObjectId("6357c9b837cd89ebe761d237")
}
~~~

**With the next command to being aguaranteed:**

~~~m
db.companies.insertOne(
    {
        "name": "Yabodev",
        "address": "C. 53-B 325, entre 52 y 54, Francisco de Montejo, 97203 Mérida, Yuc.",
        "website": "https://www.yabodev.com/"
    },
    {
        writeConcern: {
            j: false
        }
    }
)
~~~

**Output:**

~~~console
{
  acknowledged: true,
  insertedId: ObjectId("6357ca1a37cd89ebe761d238")
}
~~~

## What did you find most challenging and how did you overcome the challenge?

All is fine, i really feel like i'm learning!