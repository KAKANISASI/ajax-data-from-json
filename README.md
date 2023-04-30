# ajax-data-from-json
In the sample JavaScript, we’re only manipulating the array associated with the items key. In contrast to ordinary JavaScript, JSON requires us to place keys in double quotes. Additionally, we can’t use trailing commas for specifying objects or arrays. However, as with ordinary JavaScript arrays, we are allowed to insert objects of different types.
We’ve already looked at the script and the sample JSON file. All that’s left is the web page, which provides the parts being used by the JavaScript file to trigger and display the JSON file:
There’s not much to say here. We use the minified version of jQuery from the official web page. Then we include our script, which is responsible for injecting the logic.
Note: as we’re including our JavaScript files in the correct place (just before the closing </body> tag), it no longer becomes necessary to use a $(document).ready() callback, because at this point, the document will be ready by definition.
As previously mentioned, the $.ajax method is the real deal for any (not only JSON-related) web request. This method allows us to explicitly set all the options we care about. We can adjust async to true if we want this to call to run concurrently — that is, run potentially at the same time as other code. Setting it to false will prevent other code from running while the download is in progress:
The overrideMimeType method (which overrides the MIME type returned by the server) is only called for demonstration purposes. Generally, jQuery is smart enough to adjust the MIME-type according to the used data type.
Before we go on to introduce the concept of JSON validation, let’s have short look at a more realistic example. Usually, we won’t request a static JSON file, but will load JSON, which is generated dynamically (for example, as the result of calling an API). The JSON generation is dependent on some parameter(s), which have to be supplied beforehand:
Here we check the status to ensure that the result is indeed the object returned from a successful request and not some object containing an error message. The exact status code is API-dependent, but for most GET requests, a status code of 200 is usual.
The data is supplied in the form of an object, which leaves the task of creating the query string (or transmitting the request body) up to jQuery. This is the best and most reliable option.

JSON Validation

We shouldn’t forget to validate our JSON data! There’s an online JSON Validator tool called JSONLint that can be used to validate JSON files. Unlike JavaScript, JSON is very strict and doesn’t have tolerances — for example, for the aforementioned trailing commas or multiple ways of writing keys (with /, without quotes).
So, let’s discuss some of the most common errors when dealing with JSON.

How to fix JSON errors

There are three essential points that should be covered before starting any JSON-related debugging:

We have to make sure that the JSON returned by the server is in the correct format with the correct MIME-type being used.
We can try to use $.get instead of $.getJSON, as it might be that our server returns invalid JSON. Also, if JSON.parse() fails on the returned text, we immediately know that the JSON is to blame.
We can check the data that’s being returned by logging it to the console. This should then be the input for further investigations.
Debugging should then commence with the previously mentioned JSONLint tool.

Conclusion

JSON is the de-facto standard format for exchanging text data. jQuery’s $.getJSON() method gives us a nice little helper to deal with almost any scenario involving a request for JSON formatted data. In this article, we’ve investigated some methods and possibilities that come with this handy helper.

If you need help implementing JSON fetching in your code (using $.getJSON() or anything else), come and visit us in the SitePoint forums.
