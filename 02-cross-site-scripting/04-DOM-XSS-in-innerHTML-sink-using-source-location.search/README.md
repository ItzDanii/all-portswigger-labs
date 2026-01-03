# DOM XSS in innerHTML Sink Using location.search

**Written by Dnyaneshwar Yadav**

---

## Overview

This lab contains a **DOM-based cross-site scripting (XSS)** vulnerability in the search blog functionality.

The application dynamically updates page content using a JavaScript `innerHTML` assignment. The value assigned to `innerHTML` is taken directly from `location.search`, which is fully controlled by the user through the URL.

Because the input is inserted into the DOM **without validation or encoding**, an attacker can inject malicious HTML and JavaScript code.

The objective of this lab is to exploit the DOM XSS vulnerability and trigger the JavaScript `alert()` function.

---

## Vulnerable Code (Observed via Inspect)

While inspecting the page, the following JavaScript code was identified:
```html
<script>
    function doSearchQuery(query) {
        document.getElementById('searchMessage').innerHTML = query;
    }
    var query = (new URLSearchParams(window.location.search)).get('search');
    if(query) {
        doSearchQuery(query);
    }
</script>
```

This code directly assigns user-controlled input from `location.search` to `innerHTML`, making the application vulnerable to DOM-based XSS.

---

## Solution

### Step 1: Observe the normal search box

Open the lab and observe the normal search box displayed on the page.

At this stage, no payload has been entered.

![Normal Search Box](screenshots/01-normal-search-box.png)

---

### Step 2: Enter the XSS payload in the search box

Enter the following payload into the search box:
```html
<img src=1 onerror=alert(1)>
```

This payload uses an invalid image source to trigger the `onerror` event, which executes JavaScript.

![Payload Entered](screenshots/02-payload-entered.png)

---

### Step 3: Trigger the alert

Click on the **Search** button.

Because the `src` attribute value is invalid, the browser throws an error and executes the `onerror` event handler, triggering the JavaScript `alert()` function.

![Alert Triggered](screenshots/03-alert-triggered.png)

---

### Step 4: Inspect the DOM after payload execution

Inspect the page and observe that the injected payload is rendered inside the HTML using `innerHTML`.

The payload appears inside the DOM as an image element with an `onerror` handler.

![Payload in DOM Inspect](screenshots/04-payload-inspect-1.png)

---

### Step 5: Verify the injection point in the DOM

Further inspection confirms that the user-supplied input is inserted directly into the `searchMessage` element without any sanitization.

This confirms that the XSS vulnerability exists due to unsafe use of `innerHTML`.

![DOM Injection Confirmed](screenshots/05-payload-inspect-2.png)

---

### Step 6: Confirm lab completion

After successful execution of the payload, the lab is marked as **solved**.

![Lab Solved](screenshots/06-lab-solved.png)

---

## Result

The successful execution of the `alert(1)` function confirms the presence of a **DOM-based XSS vulnerability** caused by unsafe use of `innerHTML` with data taken directly from `location.search`.

---

## 📂 Screenshots Folder Structure
```text
screenshots/
├── 01-normal-search-box.png
├── 02-payload-entered.png
├── 03-alert-triggered.png
├── 04-payload-inspect-1.png
├── 05-payload-inspect-2.png
└── 06-lab-solved.png
```

---