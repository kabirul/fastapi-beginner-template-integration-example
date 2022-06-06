#Requirements
Python 3.6+

FastAPI stands on the shoulders of giants:

Starlette for the web parts.
Pydantic for the data parts.

pip install fastapi
pip install "uvicorn[standard]"

#The simplest FastAPI file could look like this:

from fastapi import FastAPI
app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}

Copy that to a file main.py.
Run the live server: uvicorn main:app --reload

#The command uvicorn main:app refers to:
main: the file main.py (the Python "module").
app: the object created inside of main.py with the line app = FastAPI().
--reload: make the server restart after code changes. Only use for development.

In the output, there's a line with something like:
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
That line shows the URL where your app is being served, in your local machine.

Check it
Open your browser at http://127.0.0.1:8000

You will see the JSON response as:
{"message": "Hello World"}

Interactive API docs¶
Now go to http://127.0.0.1:8000/docs
You will see the automatic interactive API documentation (provided by Swagger UI)

Alternative API docs
And now, go to http://127.0.0.1:8000/redoc.
You will see the alternative automatic documentation (provided by ReDoc)

#Templates
You can use any template engine you want with FastAPI.
A common choice is Jinja2, the same one used by Flask and other tools.
There are utilities to configure it easily that you can use directly in your FastAPI application (provided by Starlette).
#Install dependencies
pip install jinja2

#Using Jinja2Templates
Import Jinja2Templates.
Create a templates object that you can re-use later.
Declare a Request parameter in the path operation that will return a template.
Use the templates you created to render and return a TemplateResponse, passing the request as one of the key-value pairs in the Jinja2 "context".

from fastapi.templating import Jinja2Templates

app = FastAPI()
...
templates = Jinja2Templates(directory="templates")

Notice that you have to pass the request as part of the key-value pairs in the context for Jinja2. So, you also have to declare it in your path operation.

By declaring response_class=HTMLResponse the docs UI will be able to know that the response will be HTML.


