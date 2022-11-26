# Face Recognition Application

- Owner: Erwan GOUDARD
- Ressources:
    - https://www.clarifai.com/
    - https://www.npmjs.com/package/react-tilt
    - https://www.npmjs.com/package/particles.js?3.9.8
    - https://tachyons.io/
    - https://www.npmjs.com/package/react-cookie-consent

## Glossary

| Facial Recognition | Facial recognition is a technology that involves classifying and recognizing human faces, mostly by mapping individual facial features and recording the unique ratio mathematically and storing the data as a face print. The face detection in your mobile camera makes use of this technology. |
| -------- | ---- | 


## Table of contents

[[_TOC_]]

## Summary

It's a web application that enables users to **paste the URL** of an image within an input, **displays the image** and a **box around the location of faces**. It also contains a **rank** variable that keeps track of all pasted URL's and gets **incremented** with each new input. 

The app also handles basic authentication thanks to the creation of a small Back-End server using Node and Express.js, and a database using PostgreSQL to store our users. This way we can register users, delete them, and retrieve their information and counter when logged in.

|![](https://i.imgur.com/A9UY4vD.jpg)| ![](https://i.imgur.com/OR2aDYn.jpg)|
| -------- | ---- |



## Components

**Components structure**


```
src/Components

├── src
  ├── Components 
    ├── FaceRecognition
    ├── ImageLinkForm 
    ├── Logo 
    ├── Navigation
    ├── Profile 
    ├── Rank
    ├── Register
    ├── Signin
      
```

### <Register/>

```js 
 <Register onRouteChange={this.onRouteChange} isDarkMode={isDarkMode} loadUser={this.loadUser} />
```

**Screenshot**

|<img src='https://i.imgur.com/XCayQrl.png'  width="300">|
|---|


**Component API**

| Property | Type  | Description |
| -------- | ---- | ----------- |
| loadUser | Function  | Fetch the user information on submit |
| onRouteChange | Function  | Method triggering conditional display of components on route change |
| isDarkMode | Boolean  | Trigger variable to display or not dark mode |


### <Signin/>

```js 
 <SignIn onRouteChange={this.onRouteChange} isDarkMode={isDarkMode} loadUser={this.loadUser} />
```

**Screenshot**

|<img src='https://i.imgur.com/llo4B8V.png'  width="300">|
|---|


**Component API**

| Property | Type  | Description |
| -------- | ---- | ----------- |
| loadUser | Function  | Fetch the user information on submit |
| onRouteChange | Function  | Method triggering conditional display of components on route change |
| isDarkMode | Boolean  | Trigger variable to display or not dark mode |
          
### <Profile/>

```js 
 <Profile isDarkMode={isDarkMode} user={user} onRouteChange={this.onRouteChange} />
```


**Screenshot**

|<img src='https://i.imgur.com/z7v0CyH.png'  width="300">|
|---|


**Component API**

| Property | Type  | Description |
| -------- | ---- | ----------- |
| user | Object  | Object containing user information |
| onRouteChange | Function  | Method triggering conditional display of components on route change |
| isDarkMode | Boolean  | Trigger variable to display or not dark mode |
  
### <Logo/>

```js 
 <Logo isDarkMode={isDarkMode} />
```


**Screenshot**

|<img src='https://i.imgur.com/FEMhSX2.png'  width="300">|
|---|


**Component API**

| Property | Type  | Description |
| -------- | ---- | ----------- |
| isDarkMode | Boolean  | Trigger variable to display or not dark mode |

### <Rank />

```js 
 <Rank name={user.name} entries={user.entries} isDarkMode={isDarkMode}/>
```


**Screenshot**

|![](https://i.imgur.com/qTE4M8g.png)|
|---|


**Component API**

| Property | Type  | Description |
| -------- | ---- | ----------- |
| name | string  | Name of the user|
| entries | function  | Rank of the user (number of entries) |
| isDarkMode | Boolean  | Trigger variable to display or not dark mode |

### <ImageLinkForm />

```js 
<ImageLinkForm onInputChange={this.onInputChange} onPictureSubmit={this.onPictureSubmit} isDarkMode={isDarkMode} />
```


**Screenshot**

|![](https://i.imgur.com/KbHxKYp.png)|
|---|


**Component API**

| Property | Type  | Description |
| -------- | ---- | ----------- |
| onInputChange | function  | Set the input state when user types something|
| onPictureSubmit | function  | Update users rank (number of entries) and triggers the computation of the face location and display of the blue box |
| isDarkMode | Boolean  | Trigger variable to display or not dark mode |

       

### <FaceRecognition/>

**Description**

This component shows the image which url was put in and displays a blue box around the face/faces.


```js
<FaceRecognition imageUrl={imageUrl} box={box} />
```

**Screenshot**
|![](https://i.imgur.com/3Hgm2Ip.jpg)|
|--- |


**Component API**

| Property | Type | Required | Description |
| -------- | ---- | -------- | ----------- |
| imageUrl | string | false | Is used for the source of the image |
| box | object | false | Contains positions of the four corners of the blue square |







### Retrieving and displaying the face box

When performing the request, Clarifai sends us those four properties back:

```json
bottom_row: 0.52811456
left_col: 0.29458505
right_col: 0.6106333
top_row: 0.10079138
```
| Property | Description   |
| -------- | ----  |
| bottom_row | This indicates our face detection box start at 52% of the image height from the top.  |
| left_col | This indicates our face detection box start at 29% of the image width from the left.   |
| right_col | This indicates our face detection box start at 61% of the image width from the left.  |
| top_row | This indicates our face detection box start at 10% of the image height from the top.  |


In the following function, we retrieve those points and compute the exact position of those 4 points based on the image's dimensions. We then return them as follows:

![](https://i.imgur.com/q41gkbi.png)


We can now use those points to display the box using CSS.

![](https://i.imgur.com/cha95rk.png)


![](https://i.imgur.com/2KIc38A.png)


## Future possibilities

* Implement integration tests for each component
* Implement acceptance tests for all the possible flows
* Add validation to make sure the image URL is valid before updating counter
* Add validation on inputs and display error messages to the UI
* Use React Hooks
* use React Router for better user experience
