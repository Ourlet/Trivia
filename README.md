# Full Stack API Final Project

## Introduction

This project Trival is part of the Udacity Nanodegree "Full Stack Web Developer". The goal of this project is to build a trivia game to let the users challenge them-selves or their friends on their knowledge.

In order to complete this project, APIs had to be created and unit tested. The scope of the project covered the implementation of the following features:
1. Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.
2. Delete questions.
3. Add questions and require that they include question and answer text.
4. Search for questions based on a text query string.
5. Play the quiz game, randomizing either all questions or within a specific category.

## Getting Started

### Dependencies

In order to launch the project, the developer should have installed:
- Python 3.7
- pip 3
- node
- npm

#### Backend dependencies
- Backend Setup
Once you have your virtual environment setup and running, install dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

- Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

#### Frontend dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the `frontend` directory of this repository. After cloning, open your terminal and run:

```bash
npm install
```

>_tip_: **npm i** is shorthand for **npm install**

### Running the project

#### Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
python -m flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

#### Running the frontend in Dev Mode

The frontend app was built using create-react-app. In order to run the app in development mode use ```npm start```. You can change the script in the ```package.json``` file. 

Open [http://localhost:3000](http://localhost:3000) to view it in the browser. The page will reload if you make edits.<br>

```bash
npm start
```

#### Running the tests

To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

## API Reference

### Getting Started

Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, http://127.0.0.1:5000/, which is set as a proxy in the frontend configuration.
Authentication: This version of the application does not require authentication or API keys.

### Error Handling

Errors are returned as JSON objects in the following format:

```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```

The API will return four error types when requests fail:

- 400: Bad Request
- 404: Resource Not Found
- 422: Not Processable
- 500: Internal server error

### Endpoints

#### GET /categories
- Return a list of category object and success value
- Sample: ```curl http://127.0.0.1:5000/categories```

```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "success": true
}
```

#### GET /questions
- Return a list of questions including:
    - list of categories
    - page with a total of 10 questions per pages
    -  the question, answer, category, difficulty and id as values
- Sample: ```curl http://127.0.0.1:5000/questions```

```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "current_category": null, 
  "questions": [
    {
      "answer": "Apollo 13", 
      "category": 5, 
      "difficulty": 4, 
      "id": 2, 
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    }, 
    {
      "answer": "Tom Cruise", 
      "category": 5, 
      "difficulty": 4, 
      "id": 4, 
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    }, 
    {
      "answer": "Maya Angelou", 
      "category": 4, 
      "difficulty": 2, 
      "id": 5, 
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    }, 
    {
      "answer": "Edward Scissorhands", 
      "category": 5, 
      "difficulty": 3, 
      "id": 6, 
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }, 
    {
      "answer": "Muhammad Ali", 
      "category": 4, 
      "difficulty": 1, 
      "id": 9, 
      "question": "What boxer's original name is Cassius Clay?"
    }, 
    {
      "answer": "Brazil", 
      "category": 6, 
      "difficulty": 3, 
      "id": 10, 
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    }, 
    {
      "answer": "George Washington Carver", 
      "category": 4, 
      "difficulty": 2, 
      "id": 12, 
      "question": "Who invented Peanut Butter?"
    }, 
    {
      "answer": "Lake Victoria", 
      "category": 3, 
      "difficulty": 2, 
      "id": 13, 
      "question": "What is the largest lake in Africa?"
    }, 
    {
      "answer": "The Palace of Versailles", 
      "category": 3, 
      "difficulty": 3, 
      "id": 14, 
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }, 
    {
      "answer": "Agra", 
      "category": 3, 
      "difficulty": 2, 
      "id": 15, 
      "question": "The Taj Mahal is located in which Indian city?"
    }
  ], 
  "success": true, 
  "total_questions": 23
}
```

#### DELETE /delete/int:question_id
- Delete a question of the returned question_id
- Return success value and id of the deleted question if successfull
- Sample: ```curl -X DELETE http://127.0.0.1:5000/questions/4```
```
{
  "deleted": 4,
  "success": true,
}
```
#### POST /questions
- Create a new question in the database from the JSON request made on the frontend
- Return the id of the created question, the success value and the total number of questions on the database
- Sample: ```curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{"question": "Quelle est la couleur du cheval blanc de Henry 4?", "answer": "Blanc", "difficulty": 1, "category": "4" }'```

```
{
  "added": 33,
  "success": true,
  "total_questions": 23
}
```

#### POST /questions/search
- Search questions including the search term
- Return a JSON object with paginated questions matching the search term, the success value and the number of questions matching the search term
- Sample: ```curl http://127.0.0.1:5000/questions/search -X POST -H "Content-Type: application/json" -d '{"searchTerm": "Hanks"}'```
```
{
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"        
    }
  ],
  "success": true,
  "total_questions": 1
}
```

#### GET /categories/int:category_id/questions
- Get all the questions of the specified category
- Return the id of the category specified on the URL and all the questions as well as the success value
- Sample: ```curl http://127.0.0.1:5000/categories/3/questions```

```
{
  "current_category": 3, 
  "questions": [
    {
      "answer": "Lake Victoria", 
      "category": 3, 
      "difficulty": 2, 
      "id": 13, 
      "question": "What is the largest lake in Africa?"
    }, 
    {
      "answer": "The Palace of Versailles", 
      "category": 3, 
      "difficulty": 3, 
      "id": 14, 
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }, 
    {
      "answer": "Agra", 
      "category": 3, 
      "difficulty": 2, 
      "id": 15, 
      "question": "The Taj Mahal is located in which Indian city?"
    }, 
    {
      "answer": "AnsCurlJson", 
      "category": 3, 
      "difficulty": 3, 
      "id": 24, 
      "question": "QuesCurlJson"
    }, 
    {
      "answer": "AnsCurlJson", 
      "category": 3, 
      "difficulty": 3, 
      "id": 25, 
      "question": "QuesCurlJson"
    }, 
    {
      "answer": "AnsCurlJson", 
      "category": 3, 
      "difficulty": 3, 
      "id": 26, 
      "question": "QuesCurlJson"
    }, 
    {
      "answer": "Michigan", 
      "category": 3, 
      "difficulty": 3, 
      "id": 27, 
      "question": "Which US state contains an area known as the Upper Penninsula?"
    }
  ], 
  "success": true
}
```

#### POST /quiz
- Launch the trivia game
- Consume JSON request parameters of quiz category and previous questions
- Return JSON object with random questions 
- Sample: ```curl http://127.0.0.1:5000/quiz -X POST -H "Content-Type: application/json" -d '{"previous_questions": [], "quiz_category": {"type": "History", "id": "5"}}'```
```
{
  "question": {
    "answer": "Edward Scissorhands",
    "category": 5,
    "difficulty": 3,
    "id": 6,
    "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
  },
  "success": true
}
```
## Requirements of the project

### Tasks

There are `TODO` comments throughout project. Start by reading the READMEs in:

1. [`./frontend/`](./frontend/README.md)
2. [`./backend/`](./backend/README.md)

We recommend following the instructions in those files in order. This order will look familiar from our prior work in the course.

### Starting and Submitting the Project

[Fork](https://help.github.com/en/articles/fork-a-repo) the [project repository]() and [Clone](https://help.github.com/en/articles/cloning-a-repository) your forked repository to your machine. Work on the project locally and make sure to push all your changes to the remote repository before submitting the link to your repository in the Classroom.

### About the Stack

We started the full stack application for you. It is designed with some key functional areas:

#### Backend

The `./backend` directory contains a partially completed Flask and SQLAlchemy server. You will work primarily in app.py to define your endpoints and can reference models.py for DB and SQLAlchemy setup.

#### Frontend

The `./frontend` directory contains a complete React frontend to consume the data from the Flask server. You will need to update the endpoints after you define them in the backend. Those areas are marked with TODO and can be searched for expediency.

Pay special attention to what data the frontend is expecting from each API response to help guide how you format your API.

[View the README.md within ./frontend for more details.](./frontend/README.md)
