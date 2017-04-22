# Database Web App

Check it out at: https://hidden-inlet-38981.herokuapp.com/

Make sure you've followed all instructions for [BaseWebApp](https://github.com/zsobin/BaseWebApp)

The files that you're going to change are public/js/main.js, views/pages/index.ejs, and views/partials/head.ejs.

I. Get Firebase up and running
  1) Login and 'Add Project' on firebase `https://console.firebase.google.com`. Name it whatever you like!
  2) When your database is ready, it should take you to an overview page. We'll come back to this.
  3) In the sidebar, select 'Authentication' and then 'Set up a sign in method'. Select google for now, and flip the switch to 'Enable', and then save. This will make google the sign-in method to use your web application. _Can you think of why we'd want to make people log in before they can use your app? Ask a hubspotter near you what they think!_
  3) While still on the sign in method, scroll down and add your app's bas url to the `OAuth redirect domains` list (in my case, I added ` hidden-inlet-38981.herokuapp.com`). This essentially gives your app permission to use the database. 
  4) Go back to overview and select 'Add Firebase to your web app'.
  5) You should see a bunch of code pop up. This is what you'll add to your app to hook it up to Firebase!
  6) Add a `head.ejs` file to your project under views/partials, and copy the code from my [head.ejs](https://github.com/zsobin/DatabaseWebApp/blob/master/views/partials/head.ejs)
  7) Copy ONLY the `config` variable from the snippet, and add it you your head.ejs, replacing my config! The only thing you'll need to edit is the apiKey. Copy the one given to you from Firebase, and replace it with the enviroment variable `apiKey` that we'll set up in the next steps.

II. Hook up the API Key
  1) Grab the api key provided by firebase and run `heroku config:set API_KEY=whateveryourapikeyis` in your terminal (Substituting whateveryourapikeyis for whatever your API key is)
  2) Then run `heroku config:get API_KEY -s >> .env`. This way you can use API_KEY in your local environment and on heroku without actually having it in your code. Bots continuously scrape github looking for apikeys to abuse!

_There are 2 ways to interact with a database. To use Firebase, we're using the API they provided. The other way would be to access a database directly through server-side code. The server-side code would then pass the relevant data to the page that gets rendered. Can you think of why you would choose one over the other? Ask a HubSpotter what they think!_

III. Update the rest of your code!
_For each of these steps, make sure you reload the page that's running locally to check that it's working_

  1) Update your index.ejs to add the new html that we'll need for the form and for displaying posts - CHECK: Can see form on page
  2) Update your main.js with the bottom 2 functions used for auth- window.onload and toggleSignIn - CHECK: Google login form pops up, able to log in.
  3) Update your main.js to handle adding and displaying posts- handleMessageFormSubmit, addMessage and initializeStreamListener - CHECK: The post gets displayed!
  
  4) Try it out! Let us know if you get stuck. We can help you debug anything you run into. When you've been successful, go to your app on firebase and check out the database. You'll be able to see all the posts you've successfully stored!
  5) Really read through the code and try to understand what's going on. Let me know if anything is confusing and I'll happily explain!

IV. Make it your own! Here are some ideas to get started with:
- Make the app look less awful! (my bad)
- When you submit a post, the text inputs don't clear back to empty. Is there a way we could use jQuery to reset the fields for the next post?
- Each post is saved with a little more information than what currently appears (like displayName and authorPic)- let's show that info off! (make sure you check out <img> html tags)
- Add a "like" feature for posts. This would involve a few steps:
  - Add a button to each post
  - Use javascript and jQuery to monitor when someone clicks the button.
  - When someone does click the "like" button, use the post's key to update a "likes" counter on the object already saved in firebase. To keep track of the key when the "onClick" handler is called, check out something in javascript called "bind". To update a field in firebase, your function will look VERY similar to 'addMessage', except using ".update(postData)" instead of ".set(postData)".
- The personal website app uses routing to help change urls to show different pages. Using the information in that repo, try adding an "about the creator" page to your web app
