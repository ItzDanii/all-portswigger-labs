# Stored XSS into HTML Context with Nothing Encoded

**Written by Dnyaneshwar Yadav**

---

## Overview

This lab contains a **stored cross-site scripting (XSS)** vulnerability in the blog comment functionality.

User input submitted through the comment form is stored on the server and later rendered in the HTML response **without any encoding or sanitization**.

This allows an attacker to inject JavaScript code that executes whenever the affected blog post is viewed.

The goal of this lab is to submit a malicious comment that triggers a JavaScript `alert()` function when the blog post is loaded.

---

## Solution

### Step 1: Access the home page

Open the application and navigate to the **home page** containing the list of blog posts.

![Home Page](screenshots/01-home-page.png)

---

### Step 2: Open a blog post and inject the stored XSS payload

From the home page, click on any blog post to open it.

Scroll down to the **comment section** and enter the following details:

**Comment payload:**
```html
<script>alert(1)</script>
```

**Other fields:**
- Name: test
- Email: test@test.com
- Website: http://test.com

This input is submitted through the comment form and is stored by the application without validation or output encoding.

![Blog Post and Payload](screenshots/02-blog-post-and-payload.png)

---

### Step 3: Trigger the stored XSS and confirm lab completion

Return to the home page or reload the blog post.

When the stored comment is rendered, the JavaScript payload executes and displays an alert dialog, confirming successful exploitation.

At this stage, the lab is marked as solved.

![Lab Solved](screenshots/03-lab-solved.png)

---

## Result

The successful execution of the `alert(1)` function confirms the presence of a **stored XSS vulnerability in an HTML context with no output encoding**.

---

## 📂 Screenshots Folder Structure
```text
screenshots/
├── 01-home-page.png
├── 02-blog-post-and-payload.png
└── 03-lab-solved.png
```

---