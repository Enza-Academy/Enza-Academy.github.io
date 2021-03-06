---
title: BLITZ CODING IN HTML & CSS II
---

Blitz Coding with Enza: HTML/CSS II
======

**Introduction:
We will learn use what we know about HTML and CSS to add the framework bootstrap**

Create a codepen account at www.codepen.io , and create a new pen. We will start by using the code from the previous lab. Get it here:
https://enza-academy.github.io/DYR2018/HTMLCSS-II

Scroll down to the end of the list and paste into your pens -- HTML into the HTML tab and CSS into the CSS tab.

Open the Bootstrap documentation in a new tab:
https://getbootstrap.com/

Click "documentation" at the top of the page, and use this to guide you throughout the rest of the lab.

Include bootstrap within your head tags:

```html
<head>
  <title>TutorFinder</title>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
  <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
</head>
```

You will immediately notice a difference in the style of the page after you add these lines.

We will make a change to the team member photo: giving it a 'img-thumbnail' class to add the border as in bootstrap.
```html
      <!-- creating a div for each team member -->
      <div class="team-member">
        <img class="img-thumbnail team-member-photo" src="[Member photo link]" />
        <br><span class="team-member-title">[Member title]</span>
        <br><span class="team-member-name">[Member name]</span>
      </div>
      <!--...repeated for every team member-->
```

We will change our menu's from a ul to a 'nav', and give it a "nav" class. Doing this makes our menu Bootstrap-friendly since 'nav' elements are built into bootstrap. We will also remove the `<li>` elements from the links since it is now a nav and not a list. Your HTML should now be:
```html
<nav class="nav">
    <a class="nav-link" href="#home">Home</a>
    <a class="nav-link" href="#about">About</a>
    <a class="nav-link" href="#team">Team</a>
    <a class="nav-link" href="#contact">Contact</a>
</nav>
```

Center the menu by adding the Bootstrap built-in "justify-content-center" class to it:
```html
<nav class="nav justify-content-center">
    <a class="nav-link" href="#home">Home</a>
    <a class="nav-link" href="#about">About</a>
    <a class="nav-link" href="#team">Team</a>
    <a class="nav-link" href="#contact">Contact</a>
</nav>
```

Your CSS rules will remain the same, we just need to update them to accomodate the new element. Styles from `#top-menu` become styles for `nav`:
```css
nav{
  position: fixed;
  top: 0;
  width: 100%;
  background-color: green;
  height: 40px;
}
nav a{
  color: white;
}
```

We don't need the `#top-menu li` rules either, so remove it completely. Notice we also removed the `li` from the `nav a` rules, and the `text-decoration` rule too because it's no longer needed.

Since Bootstrap has default text colors, we need to override them. We use the '!important' keyword to do this in CSS. Do this for the `body` rules to ensure the text is green and centered:
```css
body{
  color: green !important;
  font-size: 20px;
  text-align: center !important;
}
```

We will be adding an advanced item to our page: a modal popup in the contact section. It functions with a programming language called JavaScript. First we will start by adding the button:
```html
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#contactModal">
  Give us a shout!
</button>
```
The attributes aren't too important, as to how they work, just know they work. The important thing is to remember the 'data-target' attribute, because this is what makes the modal appear. We haven't created the modal yet, but we will do so now. Paste the following code AFTER the button code:

```html
<!-- Modal -->
<div class="modal fade" id="contactModal" tabindex="-1" role="dialog" aria-labelledby="contactModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Contact</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <form>
          <div class="form-group">
            <label>Name</label>
            <input type="text" class="form-control" placeholder="Enter name">
          </div>
          <div class="form-group">
            <label>Email address</label>
            <input type="email" class="form-control" placeholder="Enter email">
            <small class="form-text text-muted">We'll never share your email with anyone else.</small>
          </div>
          <div class="form-group">
            <label>Comment</label>
            <textarea class="form-control" placeholder="Enter comment"></textarea>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Send</button>
      </div>
    </div>
  </div>
</div>
```

Notice we added a contact form inside the modal. You can add whatever you'd like, but the form is a good start.

Your HTML page should now look like this:

```html
<html>
  <head>
    <title>TutorFinder</title>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
    <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384-ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>
  </head>
  <body>
    <nav class="nav justify-content-center">
      <a class="nav-link active" href="#home">Home</a>
      <a class="nav-link" href="#about">About</a>
      <a class="nav-link" href="#team">Team</a>
      <a class="nav-link" href="#contact">Contact</a>
    </nav>
    
    <div id="page-wrapper">
    <div id="home" class="page-section">
      <h1>TutorFinder</h1>
      <img src="https://calendarmedia.blob.core.windows.net/assets/1d58fcb6-fee1-4dce-8725-4656e39cb979.png" id="home-logo" />
      <p>We see a need to build a platform to unite classrooms by connecting the strongest students in class with the students that need extra help.</p>
      <br>
      <p>Stay tuned for our web & mobile app launch!</p>
      <br>
      <p>Coming soon to iOS and Android!</p>
    </div>
    <div id="about" class="page-section">
      <h1>About</h1>
      <p>We are building a platform to connect the brightest in class to those who need help.</p>
      <br>
      <p>Our idea was conceived as a result of our founder needing help in class; but he was too shy to ask questions in front of the class, and too proud to utilize the university tutoring resources.</p>
    </div>
    <div id="team" class="page-section">
      <h1>Team</h1>
      <h2>Say hello to our awesome team!</h2>
      <div id="team-members">
          <!-- creating a div for each team member -->
          <div class="team-member">
            <img class="team-member-photo" src="[Member photo link]" />
            <br><span class="team-member-title">[Member title]</span>
            <br><span class="team-member-name">[Member name]</span>
          </div>
          <!--...repeated for every team member-->
      </div>
    </div>
    <div id="contact" class="page-section">
      <h1>Contact</h1>
      <!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#contactModal">
  Give us a shout!
</button>

<!-- Modal -->
<div class="modal fade" id="contactModal" tabindex="-1" role="dialog" aria-labelledby="contactModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Contact</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
        <form>
          <div class="form-group">
            <label>Name</label>
            <input type="text" class="form-control" placeholder="Enter name">
          </div>
          <div class="form-group">
            <label>Email address</label>
            <input type="email" class="form-control" placeholder="Enter email">
            <small class="form-text text-muted">We'll never share your email with anyone else.</small>
          </div>
          <div class="form-group">
            <label>Comment</label>
            <textarea class="form-control" placeholder="Enter comment"></textarea>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Send</button>
      </div>
    </div>
  </div>
</div>
    </div>
    </div>
  </body>
</html>
```

Your CSS side should now look like:
```css
*{
  padding:0;
  margin: 0;
}
body{
  color: green !important;
  font-size: 20px;
  text-align: center !important;
}
nav{
  position: fixed;
  top: 0;
  width: 100%;
  background-color: green;
  height: 40px;
}
nav a{
  color: white;
}
.page-section{
  padding-top:50px;
  min-height:500px;
}
#home-logo{
  height: 100px;
}
#page-wrapper{
  margin-left: auto;
  margin-right: auto;
  width: 960px;
}
h1{
  margin-bottom: 50px;
}
#about{
  background-color: #bfbfbf;
}
#contact{
  background-color: #bfbfbf;
}
.team-member{
  display: inline-block;
  margin-left: 50px;
}
.team-member-photo{
  height: 100px;
  width: 100px;
}
```

Now that you are familiar with adding components with bootstrap, take this time to scroll through the bootstrap documentation and try adding at least 2 more components to your pages for practice. We recommend adding a dropdown menu, and an image carousel.

Feel free to Google concepts that you either you are having trouble with, or desire to learn more information about. A great website to use to learn more about the topics discussed in class:<br>
**https://www.w3schools.com/**
<br>
Simply go here, search a specific topic, and you'll find detailed explanations and examples of all the topics that were discussed today.
