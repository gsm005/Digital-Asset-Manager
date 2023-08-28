# Digital-Asset-Manager

Take a look at live working website right here - https://dam-pix.web.app/

This is a Digital Asset Manager which provides a one stop solution for digital assets. It automatically generate tags for the images you upload, provides an in-browser image transformation and enables you to download the image in webp,jpeg and png format.

It uses React as frontend, Firebase as backend and uses Imagga API to automatically assign tags to your images.

Clone the project 

`git clone https://github.com/gsm005/Digital-Asset-Manager.git`

Open the Project directory in the terminal
  
`npm install`

After installation is complete, Create a new firebase project and create a Web app, copy the const firebaseConfig from firebase,and paste it in place of const firebaseConfig your folder directory.

`src/firebase/config.js`

After creating webapp enable firestore database, firebase storage and firebase Authentication.

Update the rules of firestore database

`rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write,delete,update: if request.time<timestamp.date(2025,1,25);
    }
  }
}`


Update the rules of firebase storage

`rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write,delete: if request.time<timestamp.date(2025,1,25);
    }
  }
}`


In Firebase Authentication Enable Email/Password  and Google.

Now, Open Google Cloud Console select the project that you are working on. Click open Cloud Shell and write these commands.

`nano cors.json`

`{[
"origin":["*"],
"method":["GET"],
"maxAgeSeconds":3600
]}`

Save this and then write in shell

`gsutil cors set cors.json <link_of_firebase_storage>`

After setting up firebase you need to set up Imagga API, for this go to imagga.com and create an account. After creating an account copy API key and API secret and paste it in place of API key and API secret in your folder directory.

`src/components/upload/progressList.js`

Start the server

  `npm start`

Inorder to increase or decrease the no. of tags you can change the number from 10 in src/components/upload/progressList.js
  
  `const detectedTags = response.data.result.tags.slice(0, 10);`
