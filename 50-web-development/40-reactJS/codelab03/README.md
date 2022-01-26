# Codelab03 - Showing our pets on the screen

## Time for some real content

With our basic layout structured and working, it's time to finally show some content. In real Tinder, it's all about the pics, so let's get our pets on the screen! For this, we have a basic Java backend running which is connected to a PostgreSQL database, all in Heroku. 
This codelab will teach us how to fetch this data from within our Angular app and show it to the world! Even though our backend app is available through Heroku, we will check it out locally and spin it up ourselves.
This way, we can check and/or change backend code if needed (spoiler: you won't have to change a lot). It helps understanding what is needed to enable our back- and frontend to talk to each other. You can find it at [https://github.com/switchfully/angular-pet-tinder-backend](https://github.com/switchfully/angular-pet-tinder-backend). Download it and spin it up!

### Defining a pet

* From this point on, we will have to take our backend into account. We're not just showing pets, we're going to fetch them from a backend which has its own peculiarities and rules. In our Java code, we have defined what a Pet object needs before it can be a real Pet object. 
Have a look at it and check the necessary fields for a Pet object.
* In React, we also want to define what a Pet object consists of. We will use it when we want to add a new pet. Similar to Java, we will make a Pet class that has the necessary fields. For structure, make a model directory in our app's root folder. Inside of that model directory, create a new file and call it Pet.js. 
Inside this file, we will write the code to define a Pet object's contents. The syntax looks like this:

```
export default class Pet {
  constructor(var1, var2, and so on...) {
    this.var1 = var1 
    this.var2 = var2
    and so on...
  } 
}
```

You can fill this up with the contents you find in our backend Pet class (look for the constructor for this).

### Creating our profile gallery

We'll show our pets in the center of our screen. Since this is a key-part of our application, we can hear the profile gallery screaming for a component! Make a new component and call it **ProfileGallery.jsx**. Don't start adding code to it yet, we'll cover something else first.
In order to get our list of pets, we are going to be making a call to the API running in our backend. We _could_ include all this information in our ProfileGallery component, but this would make it extensive and cluttered. It's best to keep calls like this in a separate file. Let's do
this first.

#### Creating a service

* Create a new subfolder in **src** and call it **api**. Create two new files inside that folder, **Client.js** and **PetService.js**.
* In the **Client** file, we will define our backend address. In **PetService**, we will be making the actual calls to our backend.
* Making http calls in React is a bit different from for example Angular. React does not have a library included that by default is able to handle these kinds of requests. Angular has **HTTPClient** present, allowing you to perform such operations out-of-the-box. This is one of the key differences
between React and other frameworks. React feels like an empty box at times. This is good because you are free to choose the solution you like, but to somewhat inexperienced devs, this can sometimes be daunting. What is the right way to go here? Want our honest answer? We're not sure either. Sometimes 
the answer is quite obvious, sometimes every article you research tells you something different. Experience is the only thing that can save you here. Give yourself time to learn and, over time, you'll have a toolkit at your disposal of which you know it will do what it needs to do!
* As for our current issue, a beloved library that has kind of become an industry standard is [Axios](https://axios-http.com/). Install it by using npm: ``npm install axios``.
* If all went well, you're now able to use the Axios library to make http calls. Back to our **Client.js**! We are going to define the url where React can find our backend here. To do this, we will define a constant called **apiClient**. We will attach an axios instance to this constant with the information we
want to specify. Afterwards, we'll export that constant, so it can be used throughout our app. Add the following to **Client.js**.
```
import axios from 'axios';

const client = axios.create({
  baseURL: 'https://pettinder.herokuapp.com/',
});
export default client;
```
* Let's move to **PetService.js**. We will be making the call to our API from here. Start by adding the import for the **client.js** file we just created, enabling our PetService to access and use it.
* Create a function **getPets()**. From within this function, we will call our API and return its reponse. The code that does this, is this: ``client.get('pets');``. ``client`` refers to the value obtained from our **Client.js** file. ``get`` is a function accessible to every axios instance and its purpose is quite clear in
this case, it will make a get call. ``'pets'`` is the mapping in our API where this request can be made. For now, this is all you'll need in **PetService**. We want this function to be accessible throughout our app, so don't forget to expose it. You should know by now how to achieve this.

#### Back to our ProfileGallery component!

Hold on to your horses, lots of stuff is about to happen in this ProfileGallery component. We'll clearly state what we want to achieve for now: **We want to show all the pets available in our database in this profile gallery.** This seems and feels like a pretty straightforward task, but implementing it will introduce several
new concepts. **Hooks**, **state** and **promises**! The first is a relatively new concept in React, the second is a very important part of React as it defines the lifecycle of our components and therefore the behaviour of our app, the latter has been around in JavaScript for quite some time and is typically used when working with asynchronous operations (which a get call to a backend API is). 
Let's provide some more insights here.

#### State

React uses state in its components. State can be seen as a plain JavaScript object containing information we provided. State is managed within the component it is declared in. The most important aspect of state is the fact that, if state gets altered, React will respond by re-rendering our component. This is of major importance for any application
and we will show it in action once we add functionalities like adding or deleting a pet (spoiler: React will not be so kind to refresh our list of pets automatically after we alter it, we'll have to tell it to do so and to achieve this, we'll be using the state of our component). We'll get back to it later and it will become more clear
once you're actually working with it over different components, but if you want to know more already you can check out [https://reactjs.org/docs/hooks-state.html](https://reactjs.org/docs/hooks-state.html).

