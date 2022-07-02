## The Great Bookshelf of Udacity

This project is a virtual bookshelf for Udacity students. 
Students can add their books to the bookshelf, give them a rating, update the rating and search through their book lists. As a part of the Fullstack Nanodegree, it serves as a practice module for lessons from Course 2: API Development and Documentation. By completing this project, students learn and apply their skills in structuring and implementing well-formatted API endpoints that leverage the knowledge of HTTP and API development best practices.

All backend code follows PEP8 style guidelines.

# Student Guidelines

Hello students! As you expand your skills, you'll use this base in various workspaces throughout the course to build the project incrementally. At each stage, we marked multiple TODOs for you to complete. You'll also notice some TODOs in the frontend section. You should refer to those sections for formatting your endpoints and responses and update the frontend to match your chosen endpoints and the programmed behavior.

You should feel free to expand on the project in any way you can dream up to extend your skills. For instance, you could add additional book information to each entry or create individual book views, including more details about the book, your thoughts, or when you completed it.

## Getting Started
# Pre-requisites and Local Development
Developers using this project should already have Python3, pip, and node installed on their local machines.
## Backend
From the backend folder, run:
```
pip install requirements.txt
```

The requirements file contains all required packages.
To run the application, run the following commands:
```
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```
These commands put the application in development and direct our application to use the __init__.py file in our flaskr folder. 
Working in development mode shows an interactive debugger in the console and restarts the server whenever you make changes.
If running locally on Windows, look for the commands in the Flask documentation.
The application runs on http://127.0.0.1:5000/ by default and is a proxy in the frontend configuration.
# Frontend
From the frontend folder, run the following commands to start the client:
```
npm install // only once to install dependencies
npm start 
```
By default, the frontend will run on localhost:3000.
# Tests
To run tests, navigate to the backend folder and run the following commands:
```
dropdb bookshelf_test
createdb bookshelf_test
psql bookshelf_test < books.psql
python test_flaskr.py
```
The first time you run the tests, omit the dropdb command.
It would be best if you kept all tests in that file.
As you update the app with new functionality during development, you can also edit the test file.

## API Reference

# Base URL

- Currently, You can only run this app locally and not host it as a base URL. 
- The default address, http://127.0.0.1:5000/, is used to host the app backend.
- We set the app as a proxy in the frontend configuration.

# Authentication: 
This application version does not require authentication or API keys.


## Error Handling

The API returns Errors as JSON objects in the following format:


```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```

The API will return three error types when requests fail:

- 400: Bad Request
- 404: Resource Not Found
- 422: Not Processable

## GET /books

# Description:

Returns a list of book objects, success value, and total number of books
The return is paginated in groups of 8.
You can include a request argument to choose page number, starting from 1.

# Sample:


```
curl http://127.0.0.1:5000/books
```

# Return:


```
"books": [
    {
      "author": "Stephen King",
      "id": 1,
      "rating": 5,
      "title": "The Outsider: A Novel"
    },
    {
      "author": "Lisa Halliday",
      "id": 2,
      "rating": 5,
      "title": "Asymmetry: A Novel"
    },
    {
      "author": "Kristin Hannah",
      "id": 3,
      "rating": 5,
      "title": "The Great Alone"
    },
    {
      "author": "Tara Westover",
      "id": 4,
      "rating": 5,
      "title": "Educated: A Memoir"
    },
    {
      "author": "Jojo Moyes",
      "id": 5,
      "rating": 5,
      "title": "Still Me: A Novel"
    },
    {
      "author": "Leila Slimani",
      "id": 6,
      "rating": 5,
      "title": "Lullaby"
    },
    {
      "author": "Amitava Kumar",
      "id": 7,
      "rating": 5,
      "title": "Immigrant, Montana"
    },
    {
      "author": "Madeline Miller",
      "id": 8,
      "rating": 5,
      "title": "CIRCE"
    }
  ],
"success": true,
"total_books": 18
}

```

## POST /books

# Description:

You can create a new book using the submitted title, author, and rating. The API returns the id of the created book, success value, total books, and book list based on the current page number to update the frontend.

# Sample:



```
curl http://127.0.0.1:5000/books?page=3 -X POST -H "Content-Type: application/json" -d '{"title":"Neverwhere", "author":"Neil Gaiman", "rating":"5"}'
```

# Return:


```
{
"books": [
  {
    "author": "Neil Gaiman",
    "id": 24,
    "rating": 5,
    "title": "Neverwhere"
  }
],
"created": 24,
"success": true,
"total_books": 17
}
```

## DELETE /books/{book_id}

# Description:
You can delete the book of the given ID if it exists.
The API will return the deleted book id, success value, total books, and book list based on the current page number to update the frontend.

# Sample:


```python
curl -X DELETE http://127.0.0.1:5000/books/16?page=2
```

# Return:


```
{
"books": [
  {
    "author": "Gina Apostol",
    "id": 9,
    "rating": 5,
    "title": "Insurrecto: A Novel"
  },
  {
    "author": "Tayari Jones",
    "id": 10,
    "rating": 5,
    "title": "An American Marriage"
  },
  {
    "author": "Jordan B. Peterson",
    "id": 11,
    "rating": 5,
    "title": "12 Rules for Life: An Antidote to Chaos"
  },
  {
    "author": "Kiese Laymon",
    "id": 12,
    "rating": 1,
    "title": "Heavy: An American Memoir"
  },
  {
    "author": "Emily Giffin",
    "id": 13,
    "rating": 4,
    "title": "All We Ever Wanted"
  },
  {
    "author": "Jose Andres",
    "id": 14,
    "rating": 4,
    "title": "We Fed an Island"
  },
  {
    "author": "Rachel Kushner",
    "id": 15,
    "rating": 1,
    "title": "The Mars Room"
  }
],
"deleted": 16,
"success": true,
"total_books": 15
}
```

## PATCH /books/{book_id}

# Description:
You can update the rating of the specified book.
The API will return with the success value and id of the modified "book".

# Sample:

```
curl http://127.0.0.1:5000/books/15 -X PATCH -H "Content-Type: application/json" -d '{"rating":"1"}'
```

Return:

```
{ "id": 15, "success": true }
```


Authors
Coach Caryn
Alexandre Monteiro de Mello

Acknowledgments
Udacity Full-Stack Web Development Course