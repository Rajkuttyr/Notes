HTTP (HyperText Transfer Protocol) is the foundation of communication between a **client (browser)** and a **server**. It works using two types of messages:

* **HTTP Request Message** → sent by the client
* **HTTP Response Message** → sent by the server

These messages allow data exchange on the web.

---

# 1. Role of HTTP Request Message

An **HTTP request message** is sent by the client to request a resource from the server.

## Purpose

* Ask the server for data (HTML page, image, video, API data, etc.)
* Send user data to server (form submission, login details)

---

## Example Scenario

When you open:

```
https://www.google.com
```

Your browser sends an HTTP request to Google's server.

---

## Structure of HTTP Request Message

An HTTP request has 4 main parts:

```
Request Line
Headers
Blank Line
Body (optional)
```

---

## Example HTTP Request

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Chrome/120
Accept: text/html

```

---

## Explanation Line by Line

### 1. Request Line

```
GET /index.html HTTP/1.1
```

Contains:

| Part       | Meaning                  |
| ---------- | ------------------------ |
| GET        | Method (type of request) |
| index.html | Resource requested       |
| HTTP/1.1   | Protocol version         |

---

## 2. Request Headers

Provide additional information.

Example:

```
Host: www.example.com
User-Agent: Chrome
Accept: text/html
```

Purpose:

• Identify client
• Specify data format
• Provide authentication

---

## 3. Blank Line

Separates headers and body.

---

## 4. Request Body (Optional)

Used in POST request.

Example:

```
username=raj&password=123
```

---

# Common HTTP Request Methods

| Method | Purpose       |
| ------ | ------------- |
| GET    | Retrieve data |
| POST   | Send data     |
| PUT    | Update data   |
| DELETE | Delete data   |

---

# 2. Role of HTTP Response Message

An **HTTP response message** is sent by the server to the client after receiving a request.

## Purpose

• Provide requested resource
• Inform request status
• Send data to client

---

## Structure of HTTP Response Message

```
Status Line
Headers
Blank Line
Body
```

---

## Example HTTP Response

```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 150

<html>
<body>
Hello World
</body>
</html>
```

---

## Explanation

### 1. Status Line

```
HTTP/1.1 200 OK
```

| Part     | Meaning          |
| -------- | ---------------- |
| HTTP/1.1 | Protocol version |
| 200      | Status code      |
| OK       | Status message   |

---

## Common Status Codes

| Code | Meaning      |
| ---- | ------------ |
| 200  | Success      |
| 404  | Not found    |
| 500  | Server error |
| 403  | Forbidden    |

---

## 2. Response Headers

Example:

```
Content-Type: text/html
Content-Length: 150
```

Purpose:

• Tell browser data type
• Tell browser data size

---

## 3. Blank Line

Separates headers and body.

---

## 4. Response Body

Contains actual data:

Example:

```
HTML page
Image
JSON data
Video
```

---

# 3. Complete Communication Flow

Step-by-step process:

```
1. User enters URL
2. Browser sends HTTP request
3. Server receives request
4. Server processes request
5. Server sends HTTP response
6. Browser displays content
```

---

# Diagram (Exam Drawing)

```
Client (Browser)
      |
      | HTTP Request
      ↓
Server
      |
      | HTTP Response
      ↓
Client displays webpage
```

---

# Real Example

User visits:

```
www.youtube.com
```

Flow:

```
Browser → sends request
Server → sends HTML, CSS, JS
Browser → displays YouTube page
```

---

# 4. Importance of HTTP Request and Response

They enable:

• Web browsing
• Form submission
• API communication
• File downloads
• Authentication

Without them, web communication is impossible.

---

# 5. Key Differences

| Feature   | HTTP Request          | HTTP Response         |
| --------- | --------------------- | --------------------- |
| Sent by   | Client                | Server                |
| Purpose   | Request resource      | Provide resource      |
| Contains  | Method, headers, body | Status, headers, body |
| Direction | Client → Server       | Server → Client       |

---

# 6. Short Exam Definition (2 marks)

HTTP request message is sent by the client to request resources from the server, and HTTP response message is sent by the server to provide the requested resource along with status information.

---

# 7. Long Exam Answer (10 marks conclusion)

HTTP request and response messages form the foundation of web communication. The client sends an HTTP request to the server specifying the required resource, and the server processes the request and returns an HTTP response containing the requested data and status information. This request-response cycle enables web browsing, data transfer, and interaction between clients and servers.

---

If you want, I can also provide **diagram image explanation and real packet-level example** which helps for 13-mark questions.

Here is a **simple JavaScript program to create Popup box, Alert box, and Confirm box** with explanation. This is perfect for exams and practicals.

---

# 1. JavaScript Program

```html
<!DOCTYPE html>
<html>
<head>
    <title>Popup, Alert and Confirm Box</title>
</head>
<body>

<h2>JavaScript Popup Boxes Example</h2>

<button onclick="showAlert()">Show Alert Box</button>
<button onclick="showConfirm()">Show Confirm Box</button>
<button onclick="showPopup()">Show Popup Box</button>

<script>

// Alert Box
function showAlert()
{
    alert("This is an Alert Box!");
}


// Confirm Box
function showConfirm()
{
    var result = confirm("Are you sure you want to continue?");

    if(result == true)
    {
        alert("You pressed OK");
    }
    else
    {
        alert("You pressed Cancel");
    }
}


// Popup Box using window.open
function showPopup()
{
    window.open("https://www.google.com", "popup", "width=400,height=300");
}

</script>

</body>
</html>
```

---

# 2. Explanation

JavaScript provides popup boxes to interact with users.

There are mainly 3 types:

1. Alert box
2. Confirm box
3. Popup box

---

# 3. Alert Box

## Syntax

```javascript
alert("message");
```

## Example

```javascript
alert("This is an Alert Box!");
```

## Purpose

• Displays warning message
• Shows information
• Has only OK button

## Output

```
---------------------
| This is Alert Box |
|        OK         |
---------------------
```

---

# 4. Confirm Box

## Syntax

```javascript
confirm("message");
```

## Example

```javascript
var result = confirm("Are you sure?");
```

## Purpose

• Asks user confirmation
• Has OK and Cancel button
• Returns true or false

---

## Example Program Explanation

```javascript
var result = confirm("Are you sure?");
```

If user clicks OK → result = true
If user clicks Cancel → result = false

---

```javascript
if(result == true)
{
    alert("You pressed OK");
}
else
{
    alert("You pressed Cancel");
}
```

---

# 5. Popup Box (window.open)

## Syntax

```javascript
window.open("URL", "name", "size");
```

## Example

```javascript
window.open("https://www.google.com", "popup", "width=400,height=300");
```

## Purpose

• Opens new browser window
• Used for ads, login window, tools

---

# 6. Types Summary Table

| Popup Type | Function      | Buttons    | Purpose          |
| ---------- | ------------- | ---------- | ---------------- |
| Alert      | alert()       | OK         | Show message     |
| Confirm    | confirm()     | OK, Cancel | Ask confirmation |
| Popup      | window.open() | New window | Open new page    |

---

# 7. Flow Diagram

```
User clicks button
       ↓
JavaScript function called
       ↓
Popup box displayed
       ↓
User responds
       ↓
Action performed
```

---

# 8. Exam Definition

Alert box displays a message with an OK button. Confirm box displays a message with OK and Cancel buttons and returns user choice. Popup box opens a new browser window using window.open() function.

---

# 9. Short Answer Version (for 5 marks)

JavaScript provides popup boxes such as alert(), confirm(), and window.open(). The alert box displays information, confirm box asks for user confirmation, and popup box opens a new browser window. These are used for user interaction.

---

If you want, I can also give **prompt box program**, which is commonly asked along with alert and confirm.
Here is a **complete HTML + JavaScript program for Whiteboard Manufacturing Company Customer Registration with validation**, along with clear explanation.

---

# HTML + JavaScript Code

```html
<!DOCTYPE html>
<html>
<head>
<title>Whiteboard Company Registration</title>

<script>

function validateForm()
{
    var name = document.getElementById("name").value;
    var phone = document.getElementById("phone").value;
    var email = document.getElementById("email").value;
    var gender = document.querySelector('input[name="gender"]:checked');
    var experience = document.getElementById("experience").value;
    var certificate = document.getElementById("certificate").checked;

    var namePattern = /^[A-Za-z ]+$/;
    var phonePattern = /^[0-9]{10}$/;
    var emailPattern = /^[^ ]+@[^ ]+\.[a-z]{2,3}$/;

    // Name validation
    if(name == "")
    {
        alert("Customer Name is required");
        return false;
    }

    if(!namePattern.test(name))
    {
        alert("Name should contain only alphabets");
        return false;
    }

    // Phone validation
    if(!phonePattern.test(phone))
    {
        alert("Phone number must be exactly 10 digits");
        return false;
    }

    // Email validation
    if(!emailPattern.test(email))
    {
        alert("Enter valid Email ID");
        return false;
    }

    // Gender validation
    if(gender == null)
    {
        alert("Please select Gender");
        return false;
    }

    // Experience validation
    if(experience == "")
    {
        alert("Please select Years of Experience");
        return false;
    }

    // Certificate validation
    if(!certificate)
    {
        alert("Please attach Certificate Proof");
        return false;
    }

    alert("Successfully registered your details");
    return true;
}


// Clear function
function clearForm()
{
    document.getElementById("regForm").reset();
}

</script>

</head>
<body>

<h2>Whiteboard Manufacturing Company</h2>
<h3>Customer Registration Form</h3>

<form id="regForm" onsubmit="return validateForm()">

Customer Name:
<input type="text" id="name"><br><br>

Phone Number:
<input type="text" id="phone"><br><br>

E-mail ID:
<input type="text" id="email"><br><br>

Gender:
<input type="radio" name="gender" value="Male"> Male
<input type="radio" name="gender" value="Female"> Female
<br><br>

Years of Experience:
<select id="experience">
<option value="">Select</option>
<option value="<5">Less than 5</option>
<option value="5-10">5 to 10</option>
<option value="10-15">10 to 15</option>
</select>
<br><br>

Certificate Proof Attached:
<input type="checkbox" id="certificate">
<br><br>

<input type="submit" value="Submit">
<input type="button" value="Clear" onclick="clearForm()">

</form>

</body>
</html>
```

---

# Explanation

## 1. Text Boxes

```html
<input type="text" id="name">
<input type="text" id="phone">
<input type="text" id="email">
```

Used to enter:

• Customer Name  
• Phone Number  
• Email

---

## 2. Gender Options (Radio Buttons)

```html
<input type="radio" name="gender" value="Male">
<input type="radio" name="gender" value="Female">
```

Allows only one selection.

---

## 3. Combo Box (Drop-down)

```html
<select id="experience">
<option value="<5">Less than 5</option>
<option value="5-10">5 to 10</option>
<option value="10-15">10 to 15</option>
</select>
```

Used to select experience.

---

## 4. Checkbox

```html
<input type="checkbox" id="certificate">
```

Used for certificate proof confirmation.

---

## 5. Submit Button

```html
<input type="submit" value="Submit">
```

Calls validation function.

---

## 6. Clear Button

```html
<input type="button" value="Clear" onclick="clearForm()">
```

Clears form.

---

# JavaScript Validation Explanation

## Get values

```javascript
var name = document.getElementById("name").value;
```

Gets input value.

---

## Name Validation (only alphabets)

```javascript
var namePattern = /^[A-Za-z ]+$/;
```

Checks only letters allowed.

Example valid:

```
Raj Kumar ✓
```

Invalid:

```
Raj123 ✗
```

---

## Phone Validation (10 digits)

```javascript
var phonePattern = /^[0-9]{10}$/;
```

Valid:

```
9876543210 ✓
```

Invalid:

```
98765 ✗
```

---

## Email Validation

```javascript
var emailPattern = /^[^ ]+@[^ ]+\.[a-z]{2,3}$/;
```

Valid:

```
raj@gmail.com ✓
```

Invalid:

```
rajgmail.com ✗
```

---

## Gender validation

```javascript
if(gender == null)
```

Checks if selected.

---

## Checkbox validation

```javascript
if(!certificate)
```

Ensures certificate proof checked.

---

# Output Cases

## Invalid Input

```
Name should contain only alphabets
```

OR

```
Phone number must be exactly 10 digits
```

---

## Valid Input

```
Successfully registered your details
```

---

# Flow Diagram (Exam)

```
User enters details
        ↓
Click Submit
        ↓
JavaScript validation
   ↓         ↓
Invalid     Valid
 ↓           ↓
Show error   Show success message
```

---

# Exam Definition (Short Answer)

Form validation using JavaScript ensures that the customer enters correct details such as alphabets in name, 10-digit phone number, and valid email ID. If validation fails, error messages are displayed, otherwise successful registration message is shown.

---

If you want, I can also give **this in 10-mark exam format with diagram and step explanation exactly as expected in university exams**.## DOM Event Handling – Detailed Explanation

DOM Event Handling is the process of detecting and responding to user actions on a web page using JavaScript.

An **event** is any action performed by the user or browser, such as clicking a button, typing in a textbox, or loading a page.

JavaScript uses the **Document Object Model (DOM)** to handle these events.

---

# 1. What is DOM?

DOM (Document Object Model) is a tree structure that represents HTML elements as objects.

Example HTML:

```html
<button id="btn">Click Me</button>
```

DOM represents it as:

```
Document
   ↓
 HTML
   ↓
 BODY
   ↓
 BUTTON (object)
```

JavaScript can access and control this button.

---

# 2. What is an Event?

An event is an action that occurs in the browser.

Examples of events:

|Event|Description|
|---|---|
|click|User clicks element|
|mouseover|Mouse moves over element|
|keydown|Key is pressed|
|submit|Form submitted|
|load|Page loaded|
|change|Input value changed|

---

# 3. What is Event Handling?

Event handling is the process of executing a function when an event occurs.

Example:

```javascript
button.onclick = function() {
    alert("Button clicked");
}
```

When button is clicked → alert appears.

---

# 4. Ways to Handle Events in DOM

There are 3 methods:

---

## Method 1: Inline Event Handling

Event written inside HTML.

Example:

```html
<button onclick="showMessage()">Click</button>

<script>
function showMessage()
{
    alert("Hello");
}
</script>
```

Disadvantage:  
Not recommended for large programs.

---

## Method 2: Event Handler Property

Using JavaScript property.

Example:

```javascript
var btn = document.getElementById("btn");

btn.onclick = function()
{
    alert("Button clicked");
};
```

---

## Method 3: addEventListener() Method (Best Method)

Example:

```javascript
var btn = document.getElementById("btn");

btn.addEventListener("click", function()
{
    alert("Button clicked");
});
```

Advantages:

• Can add multiple events  
• More flexible  
• Recommended method

---

# 5. Syntax of addEventListener()

```javascript
element.addEventListener("event", function, useCapture);
```

Example:

```javascript
button.addEventListener("click", showMessage);
```

---

# 6. Event Object

When event occurs, event object is created.

Example:

```javascript
button.addEventListener("click", function(event)
{
    console.log(event.type);
});
```

Output:

```
click
```

Event object contains:

|Property|Description|
|---|---|
|type|Event type|
|target|Element that triggered event|
|clientX|Mouse X position|
|clientY|Mouse Y position|

---

# 7. Common DOM Events

Mouse Events:

|Event|Description|
|---|---|
|click|Mouse click|
|dblclick|Double click|
|mouseover|Mouse over|
|mouseout|Mouse out|

Keyboard Events:

|Event|Description|
|---|---|
|keydown|Key pressed|
|keyup|Key released|

Form Events:

|Event|Description|
|---|---|
|submit|Form submit|
|change|Value change|
|focus|Input selected|

Window Events:

|Event|Description|
|---|---|
|load|Page loaded|
|resize|Window resized|

---

# 8. Example Program

```html
<!DOCTYPE html>
<html>
<body>

<button id="btn">Click Me</button>

<script>

document.getElementById("btn").addEventListener("click", function()
{
    alert("DOM Event Handling Example");
});

</script>

</body>
</html>
```

Output:

When button clicked → alert appears.

---

# 9. Event Flow in DOM

There are 3 phases:

```
1. Capturing Phase
2. Target Phase
3. Bubbling Phase
```

Example structure:

```
HTML
 ↓
BODY
 ↓
DIV
 ↓
BUTTON
```

Event flow:

```
Capturing: HTML → BODY → DIV → BUTTON
Target: BUTTON
Bubbling: BUTTON → DIV → BODY → HTML
```

---

# 10. Event Bubbling Example

```javascript
div.addEventListener("click", function(){
    alert("DIV clicked");
});

button.addEventListener("click", function(){
    alert("Button clicked");
});
```

Output:

```
Button clicked
DIV clicked
```

Event moves upward.

---

# 11. Importance of DOM Event Handling

• Makes webpage interactive  
• Handles user actions  
• Enables dynamic behavior  
• Used in forms, buttons, games

Example:

Login form validation  
Button click action  
Mouse hover effects

---

# 12. Real World Example

When you click login button:

```
User clicks button
↓
Event triggered
↓
JavaScript validates input
↓
Login successful
```

---

# 13. Advantages of DOM Event Handling

• Interactive webpages  
• Easy user interaction  
• Dynamic content update  
• Efficient event management

---

# 14. Diagram (Exam Drawing)

```
User Action
   ↓
Event occurs
   ↓
DOM detects event
   ↓
Event handler executes
   ↓
Action performed
```

---

# 15. Exam Definition (2 Marks)

DOM Event Handling is the process of responding to user actions such as clicks, keyboard input, and form submission using JavaScript and the Document Object Model.

---

# 16. Long Answer Conclusion (10–13 Marks)

DOM Event Handling allows JavaScript to detect and respond to user interactions such as mouse clicks, keyboard input, and form submission. It uses methods like addEventListener() to attach event handlers to HTML elements. This makes web pages interactive, dynamic, and responsive to user actions.

---

If you want, I can also provide **DOM Event Handling notes in Obsidian format with diagrams and examples for exams**.
Here is a **simple CSS code example that adds a background image and text indentation**, along with explanation.

---

# Example HTML + CSS Code

```html
<!DOCTYPE html>
<html>
<head>
<title>CSS Background and Indentation Example</title>

<style>

/* Add background image to body */
body {
    background-image: url("https://via.placeholder.com/800x600");
    background-repeat: no-repeat;
    background-size: cover;
}

/* Style for heading */
h1 {
    color: darkblue;
    text-align: center;
}

/* Style for paragraph with indentation */
p {
    background-color: rgba(255,255,255,0.8);
    text-indent: 50px;
    padding: 15px;
    margin: 20px;
    border: 2px solid black;
}

</style>

</head>
<body>

<h1>Whiteboard Manufacturing Company</h1>

<p>
Whiteboard Manufacturing Company produces high-quality whiteboards for schools, colleges, and offices. 
This paragraph demonstrates CSS background image and text indentation. The first line is indented using CSS.
</p>

</body>
</html>
```

---

# Explanation of CSS Properties

## 1. background-image

```css
background-image: url("image.jpg");
```

Purpose:  
Adds image to background.

Example:

```css
background-image: url("bg.jpg");
```

---

## 2. background-repeat

```css
background-repeat: no-repeat;
```

Purpose:  
Prevents image repetition.

Types:

|Value|Meaning|
|---|---|
|repeat|repeat image|
|no-repeat|do not repeat|
|repeat-x|repeat horizontally|
|repeat-y|repeat vertically|

---

## 3. background-size

```css
background-size: cover;
```

Purpose:  
Makes image cover entire screen.

---

## 4. text-indent

```css
text-indent: 50px;
```

Purpose:  
Adds space at beginning of first line.

Output:

```
     Whiteboard Manufacturing Company produces...
```

---

## 5. padding

```css
padding: 15px;
```

Purpose:  
Adds space inside element.

---

## 6. margin

```css
margin: 20px;
```

Purpose:  
Adds space outside element.

---

## 7. border

```css
border: 2px solid black;
```

Purpose:  
Adds border around element.

---

# Output Result

• Background image shown  
• Paragraph has indentation  
• Text appears with spacing and border

---

# Short Exam Answer (5 Marks)

CSS Code:

```css
body {
    background-image: url("bg.jpg");
}

p {
    text-indent: 50px;
}
```

Explanation:  
The background-image property is used to set an image as background. The text-indent property is used to indent the first line of text.

---

# Exam Definition (2 Marks)

The background-image property is used to set an image as the background of an element, and text-indent property is used to add indentation to the first line of text.

---

If you want, I can also give **all background properties (position, attachment, repeat, size) in one complete exam-ready program**.