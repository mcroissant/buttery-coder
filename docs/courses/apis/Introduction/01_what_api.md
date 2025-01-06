# What's an API

## 1. Introduction: Why APIs Matter
APIs (Application Programming Interfaces) are the backbone of modern software development and integration. They allow different applications to communicate and work together seamlessly, those are also key for different components of a single system to communicate and evolve in a more independent manner in that instance they work as interfaces (as understood in coding).

### Example
Think about how your favorite food delivery smartphone application shows restaurant menus, lets you place orders, and tracks delivery status. Behind the scenes, APIs connect the smartphone app to the delivery provider servers, payment gateways, and mapping services.


---

## 2. Core Concept: What Is an API?

> **Definition:** An API (Application Programming Interfaces) is a contract defining how a service is provided to consuming applications (any piece of software with a distinct function). The contract usually stipulates which requests and responses are available and their corresponding structures

### What happens in the physical world
Imagine you are at a restaurant (preferably French or Italian ;-\) ), they way you interact within this context is rather bounded and the request and results are defined in advance and you could map this to what is foud in APIs in the following way :
- **Menu**: Represents the API contract, showing what you can request.
- **Kitchen**: Handles the actual work (hidden from you).
- **Order**: Your request to the API.
- **Meal**: The response delivered back to you.

---

## 3. Components of an API
Now that you have some idea of what an API is, let's dive deeper into its constituents. All three of them have of course many variation possible depending on the API purpose and implementation.



### Endpoints
The URL or address where an API can be accessed.


### Requests and Responses
- **Request**: What you send to the API, specifying what you need.
- **Response**: The data the API sends back to you.

### Data Formats
Web APIs often use:

- **JSON** (JavaScript Object Notation): `{ "key": "value" }`
- **XML**: `<key>value</key>`

however there is no limit in what format is used by APIs


---

## 4. Types of APIs
Most type of programatic interface can be seen as APIs, here are a few types you wan't to consider.

### Web APIs
Web APIs are one of the most commonly know type of APIs as they are predominently used on the internet, again we are still on a high level definition as many different implementation are available in this context like : 
- REST (Representational State Transfer): Most common, uses HTTP.
- GraphQL: Flexible query-based API, usually leveraged by frontend components.

### Library APIs
Used within programming, libraries and frameworks for developers are prebuilt functions that can be leveraged and avoids you to build your own.

### Remote Method Invocation or Protocol Call
RMI or RPC allow multiple components of a distributed system to exchange together over the network, those are usually reserved for components developed as part of the same system and rarely exposed to the public.

### OS APIs
Enable interaction with operating systems, e.g., file systems or hardware.

---

## 5. Real-World Examples
### **Example 1: Weather Data**
A first API that could want to leverage is [OpenWeatherMap](https://openweathermap.org/api/one-call-3), after subscription (free) you can get an API key which secures you call to their server and get weather information for your local area with just one call


!!! try-it
    You could give it a go using python

    ```python
    import requests

    url = "https://api.openweathermap.org/data/3.0/weather?q=Strasbourg&appid=YOUR_API_KEY"
    response = requests.get(url)
    print(response.json())
    ```

    or **type the url directly in your browser**, as it is a rest API it leverages the same protocol your browser does to navigate the web


### **Example 2: Python File API**
Here is an other example show casing the python [File API](https://docs.python.org/3/library/functions.html#open)


!!! try-it

    ```python
    # File interaction with Python File API

    # Step 1: Create and write to a file
    print("Creating and writing to a file...")
    with open("example.txt", "w") as file:
        file.write("Hello, this is a file API example.\n")
        file.write("We are writing this text to the file.\n")
    print("File created and initial content written.\n")

    # Step 2: Append additional data to the file
    print("Appending new data to the file...")
    with open("example.txt", "a") as file:
        file.write("Adding a new line to the file.\n")
    print("New data appended.\n")

    # Step 3: Verify the appended content
    print("Re-reading the file to verify appended content:")
    with open("example.txt", "r") as file:
        updated_content = file.read()
        print(updated_content)
    ```

---

## 7. Hands-On Activity

1. Choose a public API from https://github.com/public-apis/public-apis preferably without any authentication or free of use.
2. Use a tool like [**Bruno CLI**](https://docs.usebruno.com/introduction/what-is-bruno) or **curl** to send a request.
3. Retrieve specific data.

--

## 8. Conclusion


### Common Misconceptions
- APIs are **not limited** to web services—they can exist in libraries, etc.
- APIs themselves don’t store data—they provide access to it.


### Importance of APIs in Software Ecosystems
- **Integration**: APIs enable services to work together (e.g., payment gateways, maps, social logins, OS and software).
- **Marketplaces**: APIs drive businesses like Stripe, Twilio, and Google Maps, you can make money out of an API.

### Key Takeaways
- APIs define how software applications interact.
- They use endpoints, requests, and responses to exchange data.
- APIs simplify complex integrations in the modern digital ecosystem.