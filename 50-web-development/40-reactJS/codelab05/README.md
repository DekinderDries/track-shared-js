# Codelab05 - Adding a pet

Time to provide the possibility to add a pet! We want this app to grow larger than Facebook! In this codelab, we'll be working making a new component called **AddPet**, which we will include in our **ProfileGallery** component. We will
also add a new call to our **PetService**, since we need to make a post to our API in order to add a new pet. Let's start with the latter!

## Extending our service

At this moment, **getPets()** is the only function present in our service. Time to add a second one, called **addPet()**. 
* Make a new function called **addPet()**. Not sure how to? Get inspiration from the **getPets()** function. It looks kind of the same, with just a few tweaks since this is a different kind of request.
* This function should call our API and make a post request. Check the controller in our backend to see the details needed to make this work. What does the backend need in order to be able to accept this request? Do you need
to pass anything on with this function for that?

## THe AddPet component

Adding a pet is an entirely independent functionality. We can make a new component for this. It helps keep our codebase structured and separates responsibilities. 
* Make a new functional component called **AddPet.jsx**.
* Paste the contents of **add-pet.html** into this new component.
