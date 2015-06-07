# Pyrebase

A simple python interface for the Firebase REST API.

## Installation

pip install pyrebase

## Usage

### Initialising your Firebase

```
ref = pyrebase.Firebase('https://yourfirebaseurl.firebaseio.com', 'yourfirebasesecret')
```

### Saving Data

#### POST

To save data with an autogenerated, unique, timestamp-based key, use the POST method.

Example of an autogenerated key: -JqSjGteC4SRzNJ2hH52

```
data = '{"name": "Marty Mcfly", "date_created": "05-11-1955"}'
post_this = ref.post("users", data, None)
print(post_this) # 200
```

#### PUT

To create your own keys you can use the PUT method. The key in the example below is "Marty".

```
data = '{"Marty": {"name": "Marty Mcfly", "date_created":"05-11-1955"}}'
put_this = ref.put("users", data, None)
print(put_this) # 200
```

### Reading Data

There are four methods for retrieving data with Pyrebase: all, sort_by, sort_by_first, and sort_by_last.

#### Simple Queries

##### all

All takes a child and an optional callback function, returning all unsorted data under the child.

```
def my_callback():
    print("Working while we wait...")

gimme_all = ref.all("users", my_callback())
```

##### sort_by

Sort_by takes a child, category, and optional callback function, returning data sorted by category.

```
my_users = ref.sort_by("users", "name", None)
```

#### Complex Queries

##### sort_by_first

Sort_by_first takes a child, category, start_at, limit_to_first, and optional callback function.

start_at finds the first instance of the value assigned to category.

limit_to_first restricts the amount of data returned.

Data is returned sorted by category.

```
sort_first = ref.sort_by_first("articles", "index", 5, 10, None)
```
Here we search for data in "articles" and sort entries by "index". If we have 50 entries, with indexes incremented
by 1 per entry, this query would start at the entry with an index of 5 and return 10 results from index 5-15.

##### sort_by_last

Sort_by_last takes a child, category, start_at, limit_to_last, and optional callback function.

start_at finds the first instance of the value assigned to category.

limit_to_last restricts the amount of data returned.

Data is returned sorted in reverse by category.

```
sort_last = ref.sort_by_last("articles", "index", 30, 10, None)
```
Here we search for data in "articles" and sort entries by "index". If we have 50 entries, with indexes incremented
by 1 per entry, this query would start at the entry with an index of 30 and return 10 results from index 30-20.
