# Tech Lead At-home Task

## Background

We at the Local News Lab are focused on empowering local newsrooms and the communities they serve. One of the systems we’ve built for our partners is an article recommendation engine. At the bottom of an outlet’s articles, readers are shown recommendation(s) for one or more articles they can check out next. This is pretty basic as a concept, but it’s something our early newsroom collaborators expressed a need for — and then we unpacked just what recommendation meant for them, the purpose, and what constitutes a “good” recommendation. This was an example of a concept that we would consider to be pretty established by now and yet still unfolding and offering new dimensions. Of course the technical methods and technologies for making recommendations are also changing rapidly, animating our exploration further.

The lab was founded on the idea that we build things for local newsrooms, but try to avoid “bossy” systems that impose a particular ideology on its users — it’s about flexibility in design, and what has been termed “use-inspired R&D”. Small newsrooms’ proximity to the communities they serve mean some topics take on different textures. Modular design seems important, open interfaces seem important, and, because we are a startup in a university, taking opportunities to teach (and learn) are also important. 

Our design processes so far have been very “high touch”, involving small cohorts, frequent meetings and lots of Miro. Moving to a venture that will need to serve actual products is a big pivot. What does that mean to how we identify newsroom needs and test out and deliver products? This is all by way of background as you take on the task we have designed. You have choices about how code is created, the classes you make, the flexibility you bake into the system. We teach in our data classes that each piece of digital technology embeds within it a model of the world, and acts as an argument for that model. In our case, the model has to do with the relationship between a news outlet and its readers, with the values of our publishers, with the role of journalism in communities.

Have fun!

## The Task

We would like you to create an article recommendation API. The goal of this API is to empower newsrooms’ readers to be as fully informed as they’d like to be, in the areas they’re most concerned about. 

We use the [Tornado web framework](https://www.tornadoweb.org/en/stable/index.html) so we would like you to create a Tornado web app that implements a simple RESTful article recommendation API. 

You will be provided with a starter Python module (tornadoserver.py) and a csv file (articlesembeds.csv) that contains a small article “database”. Please build on the module as much as you’d like, including modifying it and/or creating additional modules. You are welcome and encouraged to use additional libraries as necessary.

The article “database” contains essentially two columns:
- Article ID
- Article text embedding (generated by [Google’s Gemini API](https://ai.google.dev/gemini-api/docs/embeddings))

Given this data, please develop the recommendation algorithm that you feel is most appropriate (and it doesn’t need to be complicated).

We’re acutely aware of local newsrooms’ constraints and we aim to build our products accordingly. When you’re working out how this API should work, make sure you’re thinking about the technical and organizational constraints of the newsrooms.

From an implementation perspective, we’re interested in how you’re approaching and breaking down the problem. This includes, among other things:
- How you’ll structure requests from newsrooms to the API
- How one or more recommended articles are selected
- How you’ll structure the responses back to the newsrooms

From a coding perspective, we’re interested in how you structure solutions and how you think our codebase should look. This includes, among other things:
- How you’ll structure the code
- How you think about things like maintenance, future proofing, scalability, and documentation

We want to be respectful of your time, so we’re kindly requesting only 2 to 3 hours of your time. If you’d like, you can note areas where you’d expand or do things differently with more time and resources. 

This is a conversation starter to show us how you think and work!

## Deliverable

The key deliverable is a Python package that implements the above task.

Our preferred delivery method is for you to send us your Python package with your implementation. If it’s a single file you can send us just that file or if there are multiple files, please zip them. 

If you’d like, you can send us a link to a Github repository with the package.

## What’s there already

As you’ll see, the tornadoserver.py module contains basic web server components:
```
def make_app():
    return tornado.web.Application([
        (r"/", MainHandler),
    ])

async def main():
    app = make_app()
    app.listen(8888)
    await asyncio.Event().wait()

if __name__ == "__main__":
    asyncio.run(main())
```


And a helper function that reads articlesembeds.csv and returns a reader object:
```
def read_db():
    """Reads the article database and returns a reader object with the data"""
    with open('articlesembeds.csv', newline='') as csvfile:
        articlereader = csv.reader(csvfile, delimiter=';')
        return articlereader
```


There is a handler class that is currently the starting point for API requests (but feel free to modify):
```
class MainHandler(tornado.web.RequestHandler):
    """MainHandler handles requests to the server/API.

    Given a request like this:

    http://localhost:8888/?xyz=123&abc=456

    the get() method pulls xyz=123&abc=456 into the variable api_request

    Feel free to add additional methods, create other classes, etc.
    """

    def get(self):
        api_request = self.request.query

        # Write back the api request to the browser, for convenience.
        self.write(api_request)

        ### Do stuff with the api request ###
```


## Wrapping up

Please send us your final deliverable by the day before you’re scheduled to have our next interview sessions.

We’re looking forward to seeing how you work and we’re excited to continue the conversation!

If you have any questions, don’t hesitate to reach out: eric.evan.chen@columbia.edu 

And finally, have fun with this! We love what we do and want this to reflect in the work we do! 😄
