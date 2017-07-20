---
title: Lab 4: STEM with Enza Academy
---
## Lab 4

**Introduction:
Today we will learn about loops, adding events to HTML, and CSS.**

Office hours for 7/20:
6:30p-7:30p, Room 328


You now have your list of questions but no way to loop through the list. We can manually select individual questions from the list with indexing, but that is not efficient. What if there were 150 questions? We would need to write 150 lines of code to do the exact same thing. What if there was a way to execute one line of code for all 150 items? Looping through the array will allow you to do so.

To loop through an array, we use something called a "for" loop. We set up for loops like this:
```javascript
var names = ["Jack", "Joe", "Mark", "James"];
for(counter=0; counter<names.length; counter++){
  console.log(names[counter]);
}
```
Try that code above in your scrap editor.

There are 4 parts to the for loop -- set the counter, give our counter a max, increment our counter until we meet that max, and tell the program to do something each time. So for our example, we set the counter to 0, gave it a max of 1 less than the length of the names array(which is 4), incremented the counter from 0 until we reached the max, and told the console to print the question it is currently on in the loop.

As you can guess, to loop through our questions array we would need to loop through the array in a similar fashion. Remember that clicking the "Start Quiz" button on our HTML side makes the questions appear, so lets place the following code inside our 'startQuiz()' function:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   console.log(questions[counter]);
 }
}
```
Although we have code, the button still isn't doing anything when we click it. We must connect the 'Start Quiz' button to the 'startQuiz()' function. To do this, we add a property to the button called an 'onclick', and set it equal to the function we want to execute when it is clicked. In this case we want to set it to the 'startQuiz()' function. So our HTML button should look like:
```html
<button onclick="startQuiz()">Start Quiz</button>
```

Try clicking the 'Start Quiz' button. Our code is now being executed because the button is connected to the function.

Notice that this gives us the entire question object -- the console prints the object itself. However, we want the parts of the object. To get a specific property value of the object, we use bracket notation on the object. It is easiest to set another variable so that we don't confuse ourselves:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[counter];
   var question_text = current_question_in_loop['question'];
   
   console.log(question_text);
 }
}
```
Now you see the question text from all of the questions, but they are all printing back to back. There is no formatting. We want to display a number before the question, starting with 1, so let's just add the number 1 to our counter to get the number of the question in the list. For instance, we know our counter starts at 0, which is the number 1 question. This means when the counter is at 1, it is the number 2 question, and when the counter is 2, it is the number 3 question etc. Let's create a 'display_number' number so we know what's going on:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[i];
   var question_text = current_question_in_loop['question'];
   var question_number = counter+1;

   console.log(question_number);
 }
}
```
We now have a question and a display number to format the appearance of the questions. Remember we can simply concatenate(add) strings to each other to get a longer string. So let's add our numbers to the questions:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[i];
   var question_text = current_question_in_loop['question'];
   var question_number = counter+1;
   var displayed_question = question_number+". "+question_text;

   console.log(displayed_question);
 }
}
```
We now see the question number, a period, a space, and our question text correctly. Let's start adding this stuff to our HTML page. Recall that adding to HTML is simply calling the 'innerHTML' function on the div.

We want our questions to appear on our HTML form, so let's create a reference variable at the top of our JS file under the quiz feedback variable:
```javascript
var questions_form_div = document.getElementById("questions_form");
```

Our file should now look something like:
```javascript
var main_quiz_area_div = document.getElementById("main_quiz_area");
var questions_form_div = document.getElementById("questions_form");

var question_list = [
    {question:'What is the capital of Italy?', answer:'Rome'},
    {question:'What is the capital of the United States?', answer:'Washington D.C.'},
    {question:'What is the capital of Alabama?', answer:'Montgomery'},
    {question:'What is the capital of Arkansas?', answer:'Little Rock'},
    {question:'What is the capital of Arizona?', answer:'Phoenix'},
    {question:'What is the capital of Alaska?', answer:'Juneau'},
    {question:'What is the capital of California?', answer:'Sacramento'},
    {question:'What is the capital of Colorado?', answer:'Denver'},
    {question:'What is the capital of Connecticut?', answer:'Hartford'},
    {question:'What is the capital of Delaware?', answer:'Dover'}
];

function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[i];
   var question_text = current_question_in_loop['question'];
   var question_number = counter+1;
   var displayed_question = question_number+". "+question_text;

   console.log(displayed_question);
 }
}

function checkAnswers(){
}

function displayQuizResults(questions_wrong_count){
}
```

We have a reference to our HTML form, so now we are ready to use the innerHTML function to add the questions to the page. SO in the 'startQuiz()' function, set the displayed question equal to the innerHTML:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[i];
   var question_text = current_question_in_loop['question'];
   var question_number = counter+1;
   var displayed_question = question_number+". "+question_text;

   questions_form_div.innerHTML = displayed_question;
 }
}
```

Whoops, what happened? We are only seeing our last question being added to the HTML and not the others. Why aren't our other questions being displayed? This is because we keep overwriting the previous question with the next one when set the innerHTML. If we use an equal sign, it simply replaces the value with what we tell it. We don't want to replace the value, but add to it instead. So instead of an equal sign, we use a plus-equal sign:`+=`. Change the `=` sign atfer innerHTML to `+=` and notice the difference:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[i];
   var question_text = current_question_in_loop['question'];
   var question_number = counter+1;
   var displayed_question = question_number+". "+question_text;

   questions_form_div.innerHTML += displayed_question;
 }
}
```
We see our questions being displayed, but they all run together. We want them to appear on a separate line each, so let's add HTML code that accomplishes this. HTML has break tags, `<br>`, to break the current line and go to the next. Ideally we want to add these to the end of our displayed question -- this will make every question start on its own line. Let's add break tags to our 'displayed_question' variable:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[i];
   var question_text = current_question_in_loop['question'];
   var question_number = counter+1;
   var displayed_question = question_number+". "+question_text+"<br>";

   questions_form_div.innerHTML += displayed_question;
 }
}
```

We should now see our questions being displayed on their own lines. Recall that we need to inform the user when a specific question is wrong. We currently have no way to identify each question. How can we do that? Give it an id! Let's make our questions labels using an HTML label tag, and give it an id:
```javascript
function startQuiz(){
 for(counter=0; counter<questions.length; counter++){
   var current_question_in_loop = questions[i];
   var question_text = current_question_in_loop['question'];
   var question_number = counter+1;
   var displayed_question = "<label id='question"+counter+"'>"+question_number+". "+question_text+"</label><br>";

   questions_form_div.innerHTML += displayed_question;
 }
}
```

See where we included the counter in the id? The reason we do this is to differentiate every question id from each other. Because we are inside a loop, if we used an id without using our counter, every question would be issued the same id, which will not work when we want to target a specific question. The counter changes for every question, so it makes sense to use that counter in our question id. 

Also, pay close attention to the quote usage. We started our line with double quotes, but also used single quotes. Whatever quote type we start with, the code will look for that same type to close the quote. For example, see where we close the double quote right before the `+` sign and the `counter` variable? This is to ensure we got the variable `counter` and not the word "counter". If we kept the word "counter" inside the double quotes, it would display the word "counter" instead of the number of the counter, which is what we want. When we started the double quotes again, noticed we added a single quote to finish closing off the id name of the label. Remember that our ids need to be inside quotes, but we needed to use 2 types of quotes to mix our variables with our HTML.



Voila! You now know JavaScript basics, including variables, getting/referencing HTML elements, and adding code to HTML. If you were able to complete the extras, you also know how to create objects, access properties, and create arrays. You are well on your way to creating an awesome quizzer tool.

Feel free to Google concepts that you either you are having trouble with, or desire to learn more information about. A great website to use to learn more about the topics discussed in class:<br>
**https://www.w3schools.com/**

Simply go here, search a specific topic, and you'll find detailed exmplanations and examples of all the topics that were discussed today.


Instructor contact information can be found at the bottom of the lab for one-on-one questions.

Enza Instructors:
<ul>
<li>Mr. Jenkins: mjenkins@enzaacademy.org</li>
<li>Mr. Kyei: kkyei@enzaacademy.org</li>
<li>Mr. Kibret: nkibret@enzaacademy.org</li>
<li>Mr. Cudjoe: rcudjoe@enzaacademy.org</li>
</ul>