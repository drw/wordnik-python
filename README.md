Wordnik Python Client
==========
This client has been generated using the Swagger code generator, which builds robust API clients and beautiful API documentation automatically. If you'd like to learn more about Swagger, visit http://swagger.wordnik.com/ (but you don't need to know anything about Swagger to simply use this API client for Wordnik, this page will tell get you up to speed on that account).

Basic Setup
-----

Place the `wordnik` folder that you downloaded somewhere where it can be accessed by your scripts. Create a new API connection as follows:

```
import sys
# Put the full path to the wordnik/api directory here
sys.path.append('/path/to/wordnik/api')

from APIClient import APIClient
import model

api_key = 'YOUR API KEY HERE'

my_client = APIClient(api_key, 'http://api.wordnik.com/v4')
```

You'll want to edit those lines to reflect the full path to the `wordnik/api` folder you downloaded, and to use your own personal API key.

Calling a Method

Once you have a client set up, you need to instantiate an API object for whichever category or categories of items you are interested in working with. For example, to work with the `word` API and apply the method `getTopExample` method, you can do the following:

```
from WordAPI import WordAPI
wordAPI = WordAPI(my_client)

example = wordAPI.getTopExample('irony')
print example.text
```

To find out what arguments the method expects, consult the online, interactive documentation at http://developer.wordnik.com/docs , and also check out the method definitions in `wordnik/api/word.php`. You can find out what fields to expect in the return value again by using the interactive docs, or by looking at the object which is returned by the method. In this case, the documentation in `WordAPI.py` shows that `getTopExample` returns an instance of `Example`, so you would examine that class in `wordnik/model/Example.py`.

Some methods like `getTopExample` take a few arguments corresponding to different method parameters. Some of our more complex methods instead take an input object as their parameter. This object is a container for the values for all of the various paremeters the method accepts. To use a method of this sort, first you instantiate its input object and then set whatever values you desire for the properties of that object, which correspond to the method parameters you can see in the online docs. You can find out the class of the input object you need to instantiate by examining the argument in the method definition.

Let's see an example using the `getDefinitions` method. Examining its definition in `WordAPI.php`:

```
	def getDefinitions(self, wordDefinitionsInput=None, ):
```

we see that it takes `wordDefinitionsInput` as its input, so we'll first instantiate an object of class `WordDefinitionsInput`.

```
input = model.WordDefinitionsInput.WordDefinitionsInput()
```

Here `word` is a mandatory argument to the `getDefinitions` method, so we make sure to set that property on the input object after instantiating it. We'll also set a limit of 1, to get back a single definition, and let's also specify that we want a definition for our word when used as a verb.

```
input.word = 'tree'
input.limit = 1
input.partOfSpeech = 'verb'
definition = wordAPI.getDefinitions(input) 
```

The variable `$definition` is now an instance of the `Definition` class defined in `wordnik/model/Definition.py`, as indicated in the documentation for `getDefinition`. It has all the properties that you'll see in the response body for that method call if you invoke it from the online documentation.