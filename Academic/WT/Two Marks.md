# CCS375 – WEB TECHNOLOGIES  
## PART – A (All Two Mark Questions Answers)

---

### 1. Compare between server and client in web communication.

- **Client** is a device or application that sends a request for services or resources.  
- **Server** is a system that receives the request and sends back the required response.  
- Client initiates communication, and the server responds.

---

### 2. Define the Same Origin Policy (SOP) in web security.

Same Origin Policy (SOP) is a security mechanism that restricts web pages from accessing resources from a different domain, protocol, or port than the one from which it was loaded.

---

### 3. Differentiate between an ordered list (`<ol>`) and an unordered list (`<ul>`).

- `<ol>` creates a numbered list.  
- `<ul>` creates a bulleted list.  
- `<ol>` shows sequence or order, whereas `<ul>` does not indicate order.

---

### 4. Define a CSS class selector and provide its syntax.

A CSS class selector is used to apply styles to elements that share the same class attribute.

**Syntax:**
```css
.classname {
    property: value;
}
```

---

### 5. What attribute is used to specify the destination of an anchor tag?

The `href` attribute is used to specify the destination URL.

**Example:**
```html
<a href="https://example.com">Click</a>
```

---

### 6. Which keyword is used to declare a variable in JavaScript?

The keywords used to declare variables in JavaScript are:
- `var`
- `let`
- `const`

---

### 7. Differentiate between exception handling and event handling.

- **Exception handling** deals with runtime errors using `try`, `catch`, and `finally`.  
- **Event handling** deals with user interactions such as click, submit, and keypress.

---

### 8. What is the "root" of the DOM hierarchy?

The `document` object is the root of the DOM (Document Object Model) hierarchy.

---

### 9. What is the default value of an uninitialized variable in JavaScript?

The default value of an uninitialized variable in JavaScript is `undefined`.

---

### 10. Differentiate between the == and === operators in JavaScript.

- `==` compares only values and performs type conversion if necessary.  
- `===` compares both value and data type (strict equality).

---

## PART – A (Second Set)

---

### 11. State the significance of the World Wide Web (WWW).

The World Wide Web (WWW) enables users to access and share information over the internet using web browsers and hyperlinks.

---

### 12. What is the purpose of a DNS lookup?

DNS lookup translates a domain name into its corresponding IP address.

---

### 13. How can an HTML table cell be made to span multiple columns?

By using the `colspan` attribute.

**Example:**
```html
<td colspan="2">Data</td>
```

---

### 14. What is the significance of the !important keyword in CSS?

The `!important` keyword gives higher priority to a CSS rule and overrides other conflicting styles.

---

### 15. Define the term "Rich Internet Application" (RIA).

A Rich Internet Application (RIA) is a web application that provides features and functionality similar to desktop applications using technologies like JavaScript and AJAX.

---

### 16. How are strings concatenated in JavaScript?

Strings are concatenated using the `+` operator.

**Example:**
```javascript
var fullName = "Raj" + " " + "Venkat";
```

---

### 17. Define the syntax rules for writing JSON data.

- Data is written in key-value pairs.  
- Keys must be enclosed in double quotes.  
- Data is enclosed within curly braces `{ }`.  
- Key-value pairs are separated by commas.

**Example:**
```json
{
  "name": "Raj",
  "age": 19
}
```

---

### 18. How do you create a new element node using the DOM?

By using `document.createElement()`.

**Example:**
```javascript
var p = document.createElement("p");
```

---

### 19. How do you remove a character from a string in JavaScript?

By using `slice()` or `replace()` methods.

**Example:**
```javascript
var str = "Hello";
var newStr = str.slice(1);
```

---

### 20. Define the scope of a variable declared inside a function.

A variable declared inside a function has **local scope**, meaning it can only be accessed within that function.

---

