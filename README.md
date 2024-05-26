# Deploying Cloud Functions in Firebase

Welcome! This repository provides a detailed guide on how to deploy cloud functions using Firebase. Follow the steps below to get started.


<img width="1104" alt="Deploy function" src="https://github.com/arthikrishh/Firebase-cloud-Function-Deployment/assets/116914004/bbb2821d-2885-436f-80ef-29fc05fbf4d8">


## Prerequisites

- Node.js installed on your system. Download it from [nodejs.org](https://nodejs.org/en/).
- A Firebase account. Sign up at [Firebase](https://firebase.google.com/).

## Setup Instructions

### Step 1: Install Node.js

Download and install Node.js from [nodejs.org](https://nodejs.org/en/).

Verify the installation by running the following commands in your terminal:

```sh
node -v
npm -v
```

### Step 2: Create a Firebase Account

Go to [Firebase](https://firebase.google.com/) and create an account if you don't have one already. Then, upgrade your account to the Blaze plan (Pay as you go). Note that you won't be charged unless you exceed the free usage limits.

### Step 3: Install Firebase CLI

Install the Firebase Command Line Interface (CLI) by running:

```sh
npm install -g firebase-tools
```

Verify the installation:

```sh
firebase --version
```

### Step 4: Set Up Your Project Directory

Create a directory for your Firebase project and navigate into it:

```sh
mkdir firecast-deploy
cd firecast-deploy
```

### Step 5: Log In to Firebase

Log in to your Firebase account using the CLI:

```sh
firebase login
```

This command will open a browser window for authentication. Log in with your Firebase credentials.

### Step 6: Initialize Firebase in Your Project

Initialize your Firebase project:

```sh
firebase init
```

Follow these prompts during the setup:
1. Choose `Functions: Configure a Cloud Functions directory and its files`.
2. Select your Firebase project from the list.
3. Choose `JavaScript` as the language.
4. Choose `No` for using ESLint.
5. Choose `Yes` for installing dependencies with npm.

### Step 7: Write Your First Cloud Function

Navigate to the `functions` directory and open the `index.js` file in your preferred code editor. Replace its content with the following code:

```javascript
const functions = require('firebase-functions');

exports.helloWorld = functions.https.onRequest((request, response) => {
    response.send("Hello from Firebase!");
});
```

Install the dependencies:

```sh
npm install
```

### Step 8: Deploy Your Cloud Function

Deploy your function to Firebase:

```sh
firebase deploy --only functions
```

### Step 9: Verify Deployment

After deployment, the CLI will output URLs for your deployed functions. Visit the URL for the `helloWorld` function in your browser to test it. You should see the message "Hello from Firebase!".

## Advanced Functionality

### Adding More Functions

You can add more functions to the `index.js` file. For example, a function that listens to Firebase Realtime Database events:

```javascript
exports.onDataWrite = functions.database.ref('/path/{id}')
    .onWrite((change, context) => {
        const beforeData = change.before.val(); // data before the write
        const afterData = change.after.val(); // data after the write
        // Perform desired operations
        return null;
    });
```

### Scheduling Functions

Add a scheduled function to `index.js`:

```javascript
exports.scheduledFunction = functions.pubsub.schedule('every 5 minutes').onRun((context) => {
    console.log('This will run every 5 minutes!');
    return null;
});
```

## Monitoring and Managing Functions

In the Firebase Console, go to your project and navigate to the `Functions` section under `Build`. Here, you can manage and monitor your deployed functions.

Firebase provides detailed usage metrics for each function, including invocation counts, execution times, and error rates.

## Conclusion

You've now learned how to set up, write, and deploy cloud functions using Firebase. This powerful feature allows you to run backend code in response to events triggered by Firebase features and HTTPS requests.

For more tutorials and updates, visit my [website](http://www.aarthikrishnan.com/).

