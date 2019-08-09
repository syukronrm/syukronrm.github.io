---
layout: post
title:  "The Power of HTML Form!"
date:   2019-08-09 22:59:35 +0700
categories: jekyll update
---

I found something interesting when digging over the documentation of HTML form tag and, of course, StackOverflow. Here's the summary.

## Separation of form and input control

You can separate the `<form>` with it's input control, such as `<input>` or `<textarea>` by specifying `form` attribute in each input control.

```html
<form id="user-form" method="post" action="/submit_user"></form>
<form id="address-form" method="post" action="/submit_address"></form>

<input name="name" form="user-form"> <!-- Faisal Ahmad -->
<input type="submit" value="Save Name" form="user-form">  

<div class="address-data">
  <input name="city" form="address-form"/> <!-- Madiun -->
  <input name="district" form="address-form"/> <!-- Dagangan -->
  <input type="submit" value="Save Address" form="address-form"/>
</div>
```

Below is the post data when you submit the form by using 'Save Name' button.
```js
{
  name: "Faisal Ahmad"
}
```

Here's the post data for 'Save Address'.
```js
{
  city: "Madiun",
  district: "Dagangan"
}
```

## More structured data

Imagine your data have structured like this and you have a form group to save the data:

```js
{
  name: "Faisal Ahmad",
  address: {
    city: "Madiun",
    district: "Dagangan"
  },
  friends: ["Septian", "Andre"]
}
```

The traditional approach that commonly I found is passing each attribute
name (name, city, district, etc), like `<input name='city'/>`. Even though it is simple to implement in HTML form, but the back-end programming takes more effort to restructure the data.

However, you can create similar structure in HTML form like this. 
```html
<form method="post" action="/update">
  <input name="name">               <!-- Faisal Ahmad -->
  <input name="address[city]">      <!-- Madiun -->
  <input name="address[district]">  <!-- Dagangan -->
  <input name="friends[]">          <!-- Septian -->
  <input name="friends[]">          <!-- Andre -->
  <input type="submit" value="Save"/>
</form>
```

It will reduce the complexity in the back-end as the data is already structured.
