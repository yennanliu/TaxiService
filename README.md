# TaxiService
> A taxi service built via `Scala finatra` framework
- Use `MVC` model
    - model : prepare data schema
    - view  : parse data structure for user interface
    - controller : handles interaction between user interface and backend
- Functionality :
  - car booking
  - car status checks
  - car status reset
  - time processing

## 1) File structure

<details>
<summary>File structure</summary>

```
├── README.md
├── build.sbt : build file
├── script : test py script
├── src    : main source file


src
├── main
│   └── scala
│       └── com
│           └── yen
│               └── TaxiService
│                   ├── common   : common funcs
│                   ├── controller : service controller handles REST request
│                   ├── model  : data model (case class)
│                   ├── service  : service handles taxi booking logic
│                   └── serviceApp.scala : main service app
└── test
    └── scala
        └── com
            └── yen
                └── TaxiService
                    ├── common : common funcs unit test
                    ├── model : model unit test
                    └── service : service unit test
```

</details>

## 2) Run

<details>
<summary>Run</summary>

```bash
#---------------------------
# method 1 : intellJ
#---------------------------
# build, and run via intellJ (via build.sbt)

#---------------------------
# method 2 : sbt
#---------------------------
sbt build
sbt run

#---------------------------
# method 3 : java cmd
#---------------------------
# compile
sbt assembly
# run
java -cp \
target/scala-2.11/taxiservice_2.11-1.0.jar \
com.yen.TaxiService.App

# run test
sbt test
```

</details>

## 4) API endpoints

#### 4-1) `POST /api/book`
- ervice offers nearest available car to the customer location and return the total time taken to travel from the current car location to customer location then to customer destination.

```bash
curl -X POST -H "Content-Type: application/json" \
    -d '{
          "source": {
            "x": 1,
            "y": 1
          },
          "destination": {
            "x": 2,
            "y": 2
          }
        }' \
http://localhost:8888/api/book
```

#### 4-2) `POST /api/tick`
- Service offers `/api/tick` REST endpoint, when called should advance your service time stamp by 1 time unit.

```bash
curl http://localhost:8080/api/tick
```

#### 4-3) `PUT /api/reset`
- Service offers `/api/reset` REST endpoint, when called will reset all cars data back to the initial state regardless of cars that are currently booked.

Run the test cases via below py script check whether your API works correctly

```bash
curl http://localhost:8080/api/reset
```

```python
python3 basic_solution_checker.py
```

#### 4-4) `Other endpoints`

- http://localhost:8080/api/all  : list all cars status
- http://localhost:8080/api/reset : reset all cars status
- http://localhost:9990/admin : service admin UI

## 5) Dependency
- Java 1.8
- scala 2.11.8
- finatra 21.1.0