# Database Web App

Check it out at: https://hidden-inlet-38981.herokuapp.com/

Make sure you've followed all instructions for [BaseWebApp](https://github.com/zsobin/BaseWebApp)

The files that you're going to change are `project/js/main.js`, `project/html/pages/index.ejs`, and `project/html/helpers/head.ejs`.

I. Get Firebase up and running
  1) Login and 'Add Project' on firebase `https://console.firebase.google.com`. Name it whatever you like!
  2) When your database is ready, it should take you to an overview page. We'll come back to this.
  3) In the sidebar, select 'Develop' -> 'Authentication' and then 'Set up a sign in method'. Select google for now, and flip the switch to 'Enable', and then save. This will make google the sign-in method to use your web application. _Can you think of why we'd want to make people log in before they can use your app? Ask a hubspotter near you what they think!_
  3) While still on the sign in method, scroll down and add your app's bas url to the `Authorized domains` list (in my case, I added ` hidden-inlet-38981.herokuapp.com`). This essentially gives your app permission to use the database. 
  4) Go back to overview and select the angle brackets under 'Get started by adding Firebase to your app'.
  5) You should see a bunch of code pop up. This is what you'll add to your app to hook it up to Firebase!
  6) Copy ALL the code from my [`head.ejs`](https://github.com/zsobin/DatabaseWebApp/blob/master/project/html/helpers/head.ejs) file, and use it to replace ALL the code in _your_ `head.ejs` file. 
  7) Copy ONLY the `config` variable from the code snippet on firebase, and add it you your head.ejs, replacing my `config` variable! 

II. Hook up the API Key
  1) Leaving API keys in your code is bad- Bots continuously scrape github looking for apikeys to abuse! These next steps help you "hide" your api key from the code that lives on github, but still makes it accessible to be used by your app. 
  2) Run `heroku config:set API_KEY=whateveryourapikeyis` in your terminal (Substituting whateveryourapikeyis for whatever your API key is- found in your firebase config)
  3) Then run `heroku config:get API_KEY -s >> .env`. This writes the `API_KEY` variable to a file named `.env` (this file will never be pushed to github/heroku); the webapp will read from this file locally, while on heroku the variable will be pulled from heroku's own configuration system. This way you can use API_KEY in your local environment and on heroku without actually having it in your code. NOTE: if your app is already running you will need to kill the process (ctrl + c) and restart (`heroku local web`)
  4) In your `head.ejs`, replace your api key it with the enviroment variable `apiKey` (example [here](https://github.com/zsobin/DatabaseWebApp/blob/master/project/html/helpers/head.ejs#L29)). 

_There are 2 ways to interact with a database. To use Firebase, we're using the API they provided. The other way would be to access a database directly through server-side code. The server-side code would then pass the relevant data to the page that gets rendered. Can you think of why you would choose one over the other? Ask a HubSpotter what they think!_

III. Update the rest of your code!
_For each of these steps, make sure you reload the page that's running locally to check that it's working_
  1) Update your index.ejs to add the new html that we'll need for the form and for displaying posts - CHECK: Can see form on page
  2) Update your `js/main.js` with the bottom 2 functions used for auth- window.onload and toggleSignIn - CHECK: Google login form pops up, able to log in.
  3) Update your `js/main.js` to handle adding and displaying posts- handleMessageFormSubmit, addMessage and initializeStreamListener - CHECK: The post gets displayed!
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
