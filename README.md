#SemWeb :

1)Les bibliothèques:

This project uses the following libraries:

rdflib
SPARQLWrapper
icalendar
You can install these libraries by running the following commands:

      !pip install rdflib
      !pip install SPARQLWrapper
      !pip install icalendar
      
rdflib is a Python library for working with RDF, a simple yet powerful language for representing information. It provides an API for parsing and serializing RDF, and it's easy to use.

SPARQLWrapper is a Python wrapper for the SPARQL query language. It allows you to query RDF data using the SPARQL query language and get results in a variety of formats.

icalendar is a Python library for working with iCalendar files. It provides an easy way to create, read, and write iCalendar files, which are commonly used to store calendar events and to-do lists.

Note that these libraries are compatible with python 3.8 and you may have to run the command to install them on your local machine or environment.

2)The first Container :

The first block of code creates an RDF graph. Then, it serializes the graph to a turtle file and sends a POST request to the LDP container to create the resource where we will send all the events graphs. 

3)EVENT : COURSE 
uses the icalendar library to read an iCalendar file and then adds event information from the file to an RDF graph, then it sends a POST request to the LDP container to put the resources.

4)EVENT : FROM THE WEB

This code is using the Python dataclasses library to define an Event class, and the rdflib library to create RDF triples based on the data in a list of JSON-LD objects. It then sends a POST request to the LDP container with the RDF data serialized in the Turtle format.

5)Requette : This part contains 5 codes that help to request resources from the LDP container using the SPARQLWrapper library.

"1. List of events after this date"
"2. Today events"
"3. Today events that didn't started yet "
"4. Today courses or Today events that not a course "
"5. List of events in Saint Etienne "

6)Modification : 

This code is using the subprocess library to make HTTP requests to a LDP container (https://territoire.emse.fr/ldp/AmineAhmad3/) and modify a resource. It defines a function modification(resource_uri,name) that takes a resource URI and a name as inputs and modifies the resource's name to the input name.

The function first retrieves the turtle representation of the resource using a GET request and curl command. Then it uses the rdflib library to parse the turtle data and change the name of the resource.

Then it sends a DELETE request to the LDP container to delete the existing resource.

Finally, it sends a POST request to the LDP container to create a new resource with the modified turtle data.

It prints "Done" if the resource is successfully modified, otherwise it prints "I can't do it !"

It is also using the requests library to send the POST request and it is using basic authentication with the credentials like username and password.

7) Validation : This part contains 2 codes :

1-This code is using the pyshacl library to validate an event against a SHACL shape. It defines a function its_event(event) that takes an event as an input and checks if it conforms to the shape.

The function first creates an RDF graph using the rdflib library, binds several namespaces and adds triples to the graph based on the input event data such as event type, description, startDate, endDate, location1 and location2.

Then it opens a file containing the shape in turtle format and parses it into an RDF graph using the rdflib library.

The validate function from the pyshacl library is then used to check if the event graph conforms to the shape graph. If it does conform, the function prints "The data conforms to the shapes." and sends a POST request to create a new resource with the turtle data, otherwise it prints "The data does not conform to the shapes."

It is also using the requests library to send the POST request and it is using basic authentication with the credentials like username and password.

2-the second code is very similar to the first code, with the main difference being that it is for creating resources for courses instead of events. Additionally, it also uses a different SHACL graph for validation. Specifically, it uses the '/content/course.txt' file for validation instead of '/content/event.txt' used in the first code.


8)This code is an interactive menu-based program that allows users to perform various actions related to events and courses. The user can select options from a menu, such as "List of events after this date," "Today events," "Add an event," and "Add a course." The program uses the SPARQLWrapper library to query a LDP server and retrieve event information, and the pyshacl library to validate events and courses before they are added to the server. The program also uses the requests library to interact with the LDP server and make modifications to resources. The program is written in python.

#The second code is for :
The code imports the subprocess library and defines a variable called resource_uri which is the URI of the resource you want to delete. Then it creates a curl_command variable which is a command that uses the curl command to delete the resource specified by the resource_uri variable. The -u flag is used to specify the username and password, and the -X DELETE flag is used to specify that you want to delete the resource. Finally, the subprocess.run function is used to run the command and the response variable stores the output of the command.
