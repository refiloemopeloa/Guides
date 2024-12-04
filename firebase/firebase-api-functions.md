# Firebase API Functions

## Setup

Firebase API Functions are deployed using the Firebase CLI. To do this, we need to install the Firebase CLI. 

There are many ways to do this, but the easiest is to use NPM.

The first thing to do is to check your `Node` version. To do this, type:

```shell
node --version
```

The target version is 18.

Once this is done, create a directory named after the API web-app on your firebase console. Then open that directory and start the terminal in that directory.

After this is done, install the firebase tools:

```shell
npm install -g firebase-tools
```

Then, you need to login to firebase by typing:

```shell
firebase login
```

Type `yes` and it will prompt you to login via your browser. Once this is done, you'll be redirected to the terminal instance you called login from.

Once this is done, initialize the CLI:

```shell
firebase init
```

You should then see this:

```shell

     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You''re about to initialize a Firebase project in this directory:

	\your\directory\

Are you ready to proceed?
```

Type `Yes`. You'll then be prompted with:

```shell
Which Firebase features do you want to set up for this directory? Press Space to select features, then Enter to
confirm your choices. 
```

Move down to: 
```shell
() Functions: Configure a Cloud Functions directory and its files
```
and hit the space-bar.
Then press <button>Enter</button>. 

You'll then be prompted with:

```shell
=== Project Setup

First, let''s associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add,
but for now we'll just set up a default project.

? Please select an option: 
```

Select:
```shell
Use an existing project
```

Then:
```shell
Select a default Firebase project for this directory:
```
and select the project you want to use from the list of projects linked to your account.

Now, you can setup your functions:
```shell
=== Functions Setup
Let''s create a new codebase for your functions.
A directory corresponding to the codebase will be created in your project
with sample code pre-configured.

See https://firebase.google.com/docs/functions/organize-functions for
more information on organizing your functions using codebases.

Functions can be deployed with firebase deploy.

? What language would you like to use to write Cloud Functions?
```
It is your choice what language you choose.

```shell
? Do you want to use ESLint to catch probable bugs and enforce style?
```
This is also up to personal preference.

```shell
? Do you want to install dependencies with npm now? 
```
Type `Yes`. 

Congratulations! You have set up your directory for firebase CLI.

However, we aren't done yet. There are still a few things we need to do.

We'll start with checking a few packages:

```shell
express --version

cors --version
```

If you are missing either one of these, install them by typing:

```shell
npm install express

npm install cors
```


Once this is done, change into the `functions/` directory. Then type:

```shell
npm install --save firebase-functions@latest
```

## Run

From the `functions/` directory, type:

```shell
npm run serve
```

to run your functions. 

If running successfully, you should see something like:

```shell

> serve
> firebase emulators:start --only functions

i  emulators: Starting emulators: functions
!  functions: The following emulators are not running, calls to these services from the Functions emulator will affect production: auth, firestore, database, hosting, pubsub, storage, dataconnect
i  ui: downloading ui-v1.13.0.zip...
Progress: =======================================================================================================================================> (100% of 4MB) 
i  ui: Emulator UI logging to ui-debug.log
i  functions: Watching "\your\directory" for Cloud Functions...
+  functions: Using node@18 from host.
Serving at port [portnumber]

+  functions: Loaded functions definitions from source: app.
+  functions[us-central1-app]: http function initialized (http://127.0.0.1:5001/project-name/us-central1/app).

┌─────────────────────────────────────────────────────────────┐
│ ✔  All emulators ready! It is now safe to connect your app. │
│ i  View Emulator UI at http://127.0.0.1:4000/               │
└─────────────────────────────────────────────────────────────┘

┌───────────┬────────────────┬─────────────────────────────────┐
│ Emulator  │ Host:Port      │ View in Emulator UI             │
├───────────┼────────────────┼─────────────────────────────────┤
│ Functions │ 127.0.0.1:5001 │ http://127.0.0.1:4000/functions │
└───────────┴────────────────┴─────────────────────────────────┘
  Emulator Hub running at 127.0.0.1:4400
  Other reserved ports: 4500

Issues? Report them at https://github.com/firebase/firebase-tools/issues and attach the *-debug.log files.


```

A link has been generated which you can use to view your functions and what they return:
```shell
http://127.0.0.1:5001/project-name/us-central1/app
```

To access your functions, simply type the path of each function after the link:
```shell
http://127.0.0.1:5001/project-name/us-central1/app/function/id1
```

I recommend using Thunder Client for viewing your functions. To do this, just copy the link generated and use it in Thunder Client. The server has to be running for this to work.

## Functions

Before you get started on making any functions, you will need an `index.js` file in your `functions/` directory.

In this file, you'll need a few crucial things.

1. Open your firebase console in the browser for the app you are working on. 
2. Go to `Home`.
3. Click on `apps` under the title of the project.
4. Click on your API web page's settings.
5. Click on `Service accounts`.
6. Click on `Firebase Admin SDK`
7. Click `Node.js`
8. Copy the code given and paste it in your index.js file. it should look something like this:
```shell
var admin = require("firebase-admin");

var serviceAccount = require("path/to/serviceAccountKey.json");
	
admin.initializeApp({
	  credential: admin.credential.cert(serviceAccount),
	  databaseURL: "https://project-name-default-rtdb.europe-west1.firebasedatabase.app"
	});
	
```
9. Click `Generate new private key`. This will generate `serviceAccountKey.json`.
10. Place this file in your `functions/` directory.
11. Change the `"path/to/serviceAccountKey.json"` to the directory where you placed the file.
12. Add the following as well:
```shell
const functions = require("firebase-functions");
const { FieldValue } = require('firebase-admin/firestore');

const express = require("express");  
const app = express();  
const db = admin.firestore();  
const cors = require("cors");  
const crypto = require('crypto');  
app.use(cors({ origin: true }));

// Middleware to check authentication  
const authenticateRequest = async (req, res, next) => {  
    const apiKey = req.get('X-API-Key');  
    const authHeader = req.get('Authorization');  
  
    if (apiKey) {  
        // API Key authentication  
        try {  
            const apiKeyDoc = await db.collection('api_keys').doc(apiKey).get();  
            if (apiKeyDoc.exists) {  
                req.authType = 'apiKey';  
                next();  
                return;  
            }        } catch (error) {  
            console.error('Error verifying API key:', error);  
        }    } else if (authHeader && authHeader.startsWith('Bearer ')) {  
        // Firebase Authentication  
        const idToken = authHeader.split('Bearer ')[1];  
        try {  
            const decodedToken = await admin.auth().verifyIdToken(idToken);  
            req.user = decodedToken;  
            req.authType = 'firebase';  
            next();  
            return;  
        } catch (error) {  
            console.error('Error verifying Firebase token:', error);  
        }    }  
    res.status(403).json({ error: 'Unauthorized' });  
};
```

Nice! You can now begin developing your functions.
## Deploy

Once you've made your functions and have ran them with `npm`, and are ready to have them running remotely, type the following in the `functions/` directory:

```shell
firebase deploy
```

You will find the link to your api-functions on the firebase console website. 
1. On the side bar, click `All products`.
2. Click `Functions`.
3. On the dashboard, you should see your api-functions webapp details. 
4. Access your api-functions by using the link under `Trigger`.
5. To call on specific functions, simply add their paths to the end of the link.