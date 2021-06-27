
# Full Stack API Final Project

  
  

## Full Stack Trivia

  

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game, but their API experience is limited and still needs to be built out.

  

That's where you come in! Help them finish the trivia app so they can start holding trivia and seeing who's the most knowledgeable of the bunch. The application must:

  

1. Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.

2. Delete questions.

3. Add questions and require that they include question and answer text.

4. Search for questions based on a text query string.

5. Play the quiz game, randomizing either all questions or within a specific category.

  

Completing this trivia app will give you the ability to structure plan, implement, and test an API - skills essential for enabling your future applications to communicate with others.

  

## Getting Started

### Installing Dependencies for the Backend

1.  **Python 3.7**  - Follow instructions to install the latest version of python for your platform in the  [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)
    
2.  **Virtual Enviornment**  - We recommend working within a virtual environment whenever using Python for projects. Instructions for setting up a virual enviornment for your platform can be found in the  [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)
    
3.  **PIP Dependencies**  - Once you have your virtual environment setup and running, install dependencies by naviging to the  `/backend`  directory and running:
    
```
pip install -r requirements.txt
```
This will install all of the required packages we selected within the  `requirements.txt`  file.

4.  **Key Dependencies**

-   [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.
    
-   [SQLAlchemy](https://www.sqlalchemy.org/)  is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py.
    
-   [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#)  is the extension we'll use to handle cross origin requests from our frontend server.

### Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```
psql trivia < trivia.psql
```
### Running the server

From within the  `./src`  directory first ensure you are working using your created virtual environment.

To run the server, execute:
```
flask run --reload
```
The  `--reload`  flag will detect file changes and restart the server automatically.

### Installing Dependencies for the Frontend
> tip: this frontend is designed to work with [Flask-based Backend](https://github.com/udacity/FSND/blob/master/projects/02_trivia_api/starter/backend). It is recommended you stand up the backend first, test using Postman or curl, update the endpoints in the frontend, and then the frontend should integrate smoothly.

1.  **Installing Node and NPM**  
    This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (the download includes NPM) from  [https://nodejs.com/en/download](https://nodejs.org/en/download/).
    
2.  **Installing project dependencies**  
    This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the  `frontend`  directory of this repository. After cloning, open your terminal and run:
```
npm install
```
> tip:  **npm i**  is shorthand for  **npm install**

3. **Running  Your Frontend in Dev Mode**
	The frontend app was built using create-react-app. In order to run the app in development mode use  `npm start`. You can change the script in the  `package.json`  file.

	Open  [http://localhost:3000](http://localhost:3000/)  to view it in the browser. The page will reload if you make edits.
	```
	npm start
	```
## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
*Note*:  You should omit the dropdb command if you run the tests in the first time.

## API Reference
### Getting Started
* Base URL: This application hosted locally only. The backend app hosted at the default http://127.0.0.1:5000/ . Also, the frontend app hosted at http://127.0.0.1:3000/ . 
*  Authentication does not use in the project as well as API Keys.

### Error Handling
JSON objects are used to return errors in the following format:
```
{
	"success":False,
	"error":400,
	"message": "bad request"
}
```
The API has three type of errors:
* 400: Bad Request
* 404: Resource Not Found
* 422: Not Processable

### Endpoints
#### GET  '/categories'

- Fetches  a  dictionary  of  categories  in  which  the  keys  are  the  ids  and  the  value  is  the  corresponding  string  of  the  category

- Request  Arguments: None

- Returns: An  object  with  a  single  key, categories, that  contains  an  object  of  id: category_string  key:value  pairs.
- Sample: `curl http://127.0.0.1:5000/categories`
```js
{

'categories': { '1' :  "Science",

'2' :  "Art",

'3' :  "Geography",

'4' :  "History",

'5' :  "Entertainment",

'6' :  "Sports" }

}

```

  ### GET  '/questions?page=${integer}'

- Fetches  a  paginated  set  of  questions, a  total  number  of  questions, all  categories  and  current  category  string.

- Request  Arguments: page - integer

- Returns: An  object  with  10  paginated  questions, total  questions, object  including  all  categories, and  current  category  string
- Sample: `curl http://127.0.0.1:5000/questions?page=1`
  

```js
{

'questions': [

{

'id':  1,

'question':  'This is a question',

'answer':  'This is an answer',

'difficulty':  5,

'category':  2

},

],

'totalQuestions': 100,

'categories': { '1' :  "Science",

'2' :  "Art",

'3' :  "Geography",

'4' :  "History",

'5' :  "Entertainment",

'6' :  "Sports" },

'currentCategory': 'History'

}

```

  ### GET  '/categories/${id}/questions'

- Fetches  questions  for  a  cateogry  specified  by  id  request  argument

- Request  Arguments: id - integer

- Returns: An  object  with  questions  for  the  specified  category, total  questions, and  current  category  string
- Sample: `curl http://127.0.0.1:5000/categories/4/questions`
```js
{

'questions': [

{

'id':  1,

'question':  'This is a question',

'answer':  'This is an answer',

'difficulty':  5,

'category':  4

},

],

'totalQuestions': 100,

'currentCategory': 'History'

}

```

 ### DELETE  '/questions/${id}'

- Deletes  a  specified  question  using  the  id  of  the  question

- Request  Arguments: id - integer

- Returns: Does  not  need  to  return  anything  besides  the  appropriate  HTTP  status  code. Optionally  can  return  the  id  of  the  question. If  you  are  able  to  modify  the  frontend, you  can  have  it  remove  the  question  using  the  id  instead  of  refetching  the  questions.
 - Sample: `curl -X DELETE http://127.0.0.1:5000/questions/2`

### POST  '/quizzes'

- Sends  a  post  request  in  order  to  get  the  next  question

- Request  Body:

{'previous_questions': an  array  of  question  id's such as [1, 4, 20, 15]

'quiz_category': a  string  of  the  current  category }

- Returns: a single new question object

```js
{
 'question': {
 
 'id': 1,
 
 'question': 'This is a question',
 
 'answer': 'This is an answer', 
 
 'difficulty': 5,
 
 'category': 4
 
    }
}
```

### POST  '/questions'

- Sends  a  post  request  in  order  to  add  a  new  question
- Returns: a  new  question  object with paginated questions
- Sample: `curl -X POST http://127.0.0.1:5000/questions -H "Content-Type: application/json" -d "{ \"question\": \"This is a question\", \"answer\": \"This is an answer\", \"difficulty\": 5, \"category\": \"4\" }"`
```js
{
'success': True,

'created': 25,

'questions': [

{"answer":"Tom Cruise",

"category":5,

"difficulty":4,

"id":4,

"question":"What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
}
,
{"answer":"Maya Angelou",

"category":4,

"difficulty":2,

"id":5,

"question":"Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"}
]
,
"success":true,

"total_questions":20

}

```

### POST  '/questions'

- Sends  a  post  request  in  order  to  search  for  a  specific  question  by  search  term

- Returns: any  array  of  questions, a  number  of  totalQuestions  that  met  the  search  term  and  the  current  category  string  

- Sample: `curl -X POST http://127.0.0.1:5000/questions -H "Content-Type: application/json" -d "{ \"searchTerm\": \"this is the term the user is looking for\"}"`
```js
{

'questions': [

{

'id':  1,

'question':  'This is a question',

'answer':  'This is an answer',

'difficulty':  5,

'category':  5

},

],

'totalQuestions': 100,

'currentCategory': 'Entertainment'

}

```

### Authors
* Mohammed Alali who developed the API, test suite and this README.
* The rest files of project such as the models and backend and frontend created by [Udacity](https://www.udacity.com/) for [Full Stack Web Developer Nanodegree](https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd0044) as project template.
