---
title: "Building a Web scraping API in 20 Minutes"
date: 2022-07-05T22:18:21+02:00
draft: false
---
*A brief step-by-step guide for turning a website that is not yours into an API using Beautifulsoup and FastAPI*

![Photo by Oskar Yildiz on Unsplash, showing a pc with code](../../../images/mac_with_code_compressed_cropped.jpeg)
I’ve begun mass-producing APIs to practice my API developing skills for the past weeks.

> Creating your own RESTful API can be a great way to build a business around data you’ve collected or a service you’ve created, or it can just be a fun personal project that allows you to learn a new skill.

This is from [RapidApi’s](https://rapidapi.com/) website; I didn’t want to build an entirely new service to practice APIs. So I focused on the “data you’ve collected” part and decided to web scrape data from other’s sites to use that for the APIs.

To practice my skills, I’ve created one API daily for a week (still going). Throughout this experience, I’ve made a routine/setup for creating the APIs. And though it could help you start your API journey or at least help you.

---

**Note:** This is my first post, so if you have any feedback or questions, let me know! I’m excited to join this great community and see what it brings. Enough about myself; let us get into the system.

---
### Setting up the Environment
Create the project locally, on GitHub, and set up the virtual environment:

1. Create a local folder ```mkdir Name```
2. Create a new GitHub repository with ```Name```
3. Inside the local folder:
	* ```git init```
	* ```git init```
	* ```git add README.md```
	* ```git commit -m “initial commit”```
	* ```git remote add origin URL_TO_GIT_REPO```
	* ```git push -u origin master```
4. Create the file structure
```python
mkdir src
cd src
touch __init__.py main.py scraper.py
```
* ```python3 -m venv venv``` to create the virtual environment
5. Install requirements:
	* ```pip install requests fastapi bs4```

Now we have:
	* local folder
	* GitHub repository
	* a virtual environment
	* git version control
	* and all packages we need
### Getting to the code
Now that we have everything set up. We can get codin’.

First, we need to get the data, so we start in ```scraper.py```. We’ll use [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).

I will give you the code as an outline, but each site is different, so you may need some extra functions or don’t need the one I provided.

**Scraping**

```python
#import necessary packages
from typing import List
import requests as _request
import bs4 as _bs4
#in case you scrape data which goes over multiple pages
def _generate_url(page: str) -> List:
    url = f"https://www.exampleurl.com/{page}"
    return url
#create the Spider
def _get_page(url: str) -> _bs4.BeautifulSoup:
   page = _request.get(url)
   soup = _bs4.BeautifulSoup(page.content, "html.parser")
   return soup
#kind of the main outline you can use to find your data
def get_data(var: str) -> List:
    url = _generate_url(var)
    page = _get_page(url)
    raw_data = page.find_all(class_="event") #example search
    data = [data.text for data in raw_events]
    return data
```

What I like to do here is create the output of ```get_data()``` as a dictionary, the output adjusted better for the API, but it varies mainly depending on your project, so I’ll stick with this.

---

**The FastAPI**
Now that we have the functions and the data, we can create our API. For that, we'll use [FastAPI](https://fastapi.tiangolo.com/) and code in ```main.py```.
```python
from fastapi import FastAPI
import scraper as _scraper
app = FastAPI()
@app.get("/")
async def root():
    return {"message":"Welcome to my API"}
#this is how it should look like and for other functions you can #create duplicates of this block
@app.get("/example-function)
async def example_function:
    return _scraper.get_data("1")
```
We're done with the code :partying_face:

### Usage
To see and test your API, you need to ```pip install uvicorn``` . Cd into your ```src``` folder and run your API Ux with: ```uvicorn main:app --reload``` .

Now you see the message you have put into the ```root()``` function.

FastAPI has this beautiful feature when you write /docs next to your localhost URL (like this: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)), it should look something like this:

![FastAPI docs demonstration](../../../images/building_web_scraper_fastapi_docs.png)

As you can see, you can set it up fast and already have a working API!

I recommend this [video](https://www.youtube.com/watch?v=Nni0HX9O4hc&ab_channel=rithmic) for more of an in-depth look into an example code and maybe even your first hands-on experience.

And I also started my journey with this [article](https://towardsdatascience.com/develop-and-sell-a-python-api-from-start-to-end-tutorial-9a038e433966).

---

### Closing thoughts
That’s it with this step-by-step guide to implementing a complete API using FastAPI and BeautifulSoup.

I hope you enjoyed creating an API just as much as I did and want to continue your journey.

If you want to get ideas for more API projects, check out my [GitHub](https://github.com/VinceDerPrince).

As I’ve already mentioned, this is my first post, and I’m sure I will post more in the future, so if you’ve liked this post, if you want to, you can follow me on [Medium](https://medium.com/@VinceDerPrince).

Thank you.

