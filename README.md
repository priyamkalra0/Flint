# Flint is a simple & dumb python client around Google's [Firebase](https://web.app) API: Deploy to web-hosting with almost zero setup.

## Usage
You must generate a new private key (certificate.json) for the Firebase Admin SDK service account in your firebase project by clicking [here](https://console.firebase.google.com/u/0/project/_/settings/serviceaccounts).
Copy the body of this JSON file and use it to authenticate your deployments when using Flint as shown below:

```py
from flint import Firebase, Certificate
certificate = Certificate({ # this is the JSON body mentioned above
    "type": "service_account",
    "token_uri": "https://oauth2.googleapis.com/token",
    "private_key": "-----BEGIN PRIVATE KEY-----\n[EXAMPLE]\n-----END PRIVATE KEY-----\n",
    "client_email": "example@example.iam.gserviceaccount.com",
})

firebase = Firebase("example", certificate)
firebase.deploy("./public")
```

NOTE: Flint is not yet available as a package, so you need to manually download and include it in your project, and you must install the `firebase-admin` and `requests` python packages.

The above snippet will create a new app version, add all files in the ./public directory (recursive directory tree) to that version, and deploy it. Progress is printed to the console like so:
```
Access token: XXXXXXXcp81
Version: 96ab635551db9191

[1/7 file_uploaded] /scripts/lib/sha256.js, b62a0e9f2e35abfdcd0606bfb09aeacaf017320a2dfd0f31dcc5cdc0222faa70
[2/7 file_uploaded] /scripts/lib/firebase.js, 96b537e08b014f835ebed3bbd681d9f62f75cdba48b87926f423474b34f81f11
[3/7 file_uploaded] /scripts/main.js, e131df7eb1a0d93f12a1ddd9ba5768c94ee192936c264072f943722df329f167
[4/7 file_uploaded] /scripts/metadata.js, 8ed6ce5202a60c754676d13362409272dbcafdc702743fbb51434908d73176ed
[5/7 file_uploaded] /static/style.css, f04ab9cf5508d1c97a1a8b7b6379a65f4cb45cd6f3a8c38fa4bff27c932cc2ac
[6/7 file_uploaded] /static/metadata.json, f55c3093546826f29ab5b534a1b12bb817f09b2d3b4e476bbf696d6efed0f3d8
[7/7 file_uploaded] /index.html, 5742e6746c14e846943e42d127b254e75d80800a64932e1b0ca9afec91f3aeaf

[success] Deployed to example.web.app
```
