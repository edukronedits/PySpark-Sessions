# PySpark Learning History

## Day 1 - Getting Started with PySpark

### Topics Covered
- Installed and configured the PySpark environment
- Created a SparkSession
- Learned Spark fundamentals and local execution
- Understood the basic flow of working with DataFrames

### Practical Actions
- Started Spark with `SparkSession.builder`
- Checked the Spark version
- Created a sample dataset
- Converted data into a DataFrame
- Displayed the DataFrame using `show()`

### Example
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("PySpark Learning") \
    .master("local[*]") \
    .getOrCreate()

data = [("Alice", 25), ("Bob", 30), ("Charlie", 28)]
columns = ["name", "age"]

df = spark.createDataFrame(data, columns)
df.show()
```

### Actions Learned
Actions are operations that trigger execution and return results to the driver. Common examples:
- `show()`
- `collect()`
- `count()`
- `take(n)`
- `first()`

```python
print(df.count())
print(df.collect())
print(df.take(2))
```

---

## Day 2 - Transformations in PySpark

### Topics Covered
- Learned the difference between transformations and actions
- Practiced DataFrame transformations
- Worked with filtering, selecting, and adding columns

### Key Concepts
- Transformations are lazy and do not execute immediately
- A transformation returns a new DataFrame
- Actions are needed to trigger execution and produce output

### Common Transformations
- `select()`
- `filter()`
- `withColumn()`
- `drop()`
- `orderBy()`
- `groupBy()`

### Example
```python
from pyspark.sql import functions as F

filtered_df = df.filter(F.col("age") >= 25)
filtered_df.show()

selected_df = df.select("name", "age")
selected_df.show()

updated_df = df.withColumn("age_plus_1", F.col("age") + 1)
updated_df.show()
```

### Note
- Transformations build a logical plan first
- Spark executes only when an action like `show()` or `count()` is called

---

## Day 3 - DataFrame Operations and Basic Queries

### Topics Covered
- Sorting data with `orderBy()`
- Selecting columns and filtering rows
- Working with SQL-style queries in Spark

### Practice
```python
# Sort rows by age
sorted_df = df.orderBy("age")
sorted_df.show()

# Select specific columns
name_age_df = df.select("name", "age")
name_age_df.show()

# Create a temp view and query it using SQL
df.createOrReplaceTempView("people")
result = spark.sql("SELECT name, age FROM people WHERE age > 25 ORDER BY age")
result.show()
```

### Summary
- Day 1 focused on setup and actions
- Day 2 covered transformations and lazy evaluation
- Day 3 continued with DataFrame operations and SQL queries

This learning history tracks my early PySpark journey and progress.
