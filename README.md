# Flint is a simple & dumb python client around Google's [Firebase](https://web.app) API: Deploy to app-hosting with almost zero setup.

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

The above snippet will create a new app version, add all files in the ./public directory (recursive directory tree) to that version, and deploy it.  
Progress is printed to the console like so:
```
Access token: ya29XXXXXXX
Version: 2af6c788210327b6

[1/11 file_uploaded] 740f15c1e0c93dbebbd2bced77809730a3c3051729bf5252df2ec61b385e79c1
[2/11 file_uploaded] 698d38d849d0e46360063fad5fede42b999b352f3a9ef353e6b5f6a326f42795
[3/11 file_uploaded] a19d1b0bd36cfb13a555c77b546fd23e951dfb3ea422541de59b38ca1024ba48

...

[11/11 file_uploaded] 176dc7450a577b7917e4b5e84249dc0351f953e42759e78ee5154721d85d44ba

[success] Deployed to example.web.app
```
