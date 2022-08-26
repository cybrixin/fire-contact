# 🔥 Fire Contact 📧

> 🤝🏻 Sometimes the perfect person for you is who you least expected to be.

Fire Contact is built to get messages from you. My [website](https://formula21.github.io) is hosted on [GitHub](https://github.com/formula21/formula21.github.io), which is basically a static site hosting, with no backend. But a website devoid of a contact form is really in-efficient. Again it is arguably easy to shift to a hosting provider in less than a minute. They provide me with a SQL database, a backend to host my files, a custom dashboard so on and forth. But I really like to stick on to GitHub Pages.

Enter [Firebase by Google](https://firebase.google.com) a product which basically is a backend jamstack only better. It can be accessed from the front-end, is lightweight, easy to learn, and packed with a lot of features other than a database. Most importantly it is built by Google, so it must be good right. You may want to argue that, most (if not all) my projects are open source and I am an open-source fan. So why not use [Supabase](https://supabase.com) or any other [alternatives](https://blog.back4app.com/firebase-alternatives/). Honestly, I find this product of Google like many other best suited and quick to learn.

My client side code is bootstraped & built by [Vite.js](https://vitejs.dev) with the `Vanilla JS` flavour.

## Proprietary Third Party Stuff
- 🔥 Google Firebase (code for this is open-source & I have used the [firebase/js-sdk](https://github.com/firebase/firebase-js-sdk))
  - 🔒 Authentication ~ Firebase Anonymous Authentication for tracking
  - 🗺 Google Analytics
  - 🗄 Cloud Firestore
  - ✔ App Check
  - ☁ Cloud Functions (Soon to be implemented)
- Google reCAPTCHA
  - Version 2 _(v2)_ ➡ "✅ I am not a robot"
  - Version 3 _(v3)_ ➡ "🙈 Invisible for App Check"

## Open Source Stuff
- 🤬|❎ [Bad Words Filter](https://github.com/web-mech/badwords)
- #️⃣ [SHA-1](https://github.com/emn178/js-sha1)
- 📢 [Snackbar](https://github.com/polonel/SnackBar)

## Killer features

- 🔥 Blazingly fast
- ⚖ Extremely Lightweight
- ⏳ Realtime features
- 🔐 Standard Verification & Security
-🤺 Battle tested

## Other features

- 🔁 Idempotent Messages (No replay attacks)
- 🛡 Messages sent only by humans (reCAPTCHA token has to be solved & the site is protected via reCAPTCHA 😈)
- 🚦 Protected backend by security rules.
- 📏 Easily scaleable
- ⛔ No read access
- 📉 Low writes & reads keeping the 💳 cost low
- ⏳ Scheduled auto-reply

**NOTE**: You will find a ⚙ [.env.production](.env.production) file with all the VALUES filled in & then uploaded to the repository. Be assured these values are public facing values and no matter who sees them 👀, just cannot tamper with these.

## Workflow

### Client Side workflow

⌨ | 🧼 `➡` 🖱 `➡` 💪🏻 `➡` 🖱 `➡` 🛡 `➡` 🔥|🗄 `➡` ⏳ `➡` 📩

👆🏻 The above emojis summarize the workflow. It starts with the user typing ⌨ a message. They intially try to check 🕵🏻‍♂️ & filter 🧼 any profanity from the message, while validating the name, email and the subject. After that it challenges 💪🏻 the user 👤 to solve the same. The user then submites the solved challenge, which gets verified 🛡 and at the end a document is written to the Cloud Firestore under the collections "messages" (by default). I deviced a plan to make the message idempotent (no recording/writting) more than once, by making the document id the "hash of the token" solved by the user.

The following is the structure of the document written:

```json
{
  "name": "name",
  "email": "example@example.com",
  "subject": "The subject",
  "message": "Your message",
  "replied": false,
  "sentAt": "The general timestamp of your device",
  "token": "The challenge 💪🏻 solved by the user 👤, now tokenized"
  "uid": "The user id, generated by the anonymous sign in provider"
}
```

👆🏻 If you look closely `replied` field is a boolean which is significant for the scheduler, details of which are given below ⬇.

### Server Side

The server side is kept very simple. It is an [Express.js](https://expressjs.com/) application having an endpoint `/verify`. My backend is hosted on Heroku and you will find the code at the [server](/sever) folder in this repository. 

Please remeber to setup the required secrets in a ⚙ `.env` file using the example [.env.example](server/.env.example) file. It requires the `SITE KEY` & `SECRET KEY` bought found on the dashboard of your reCAPTCHA project. It also requires a `PORT` (default 3000) which is generally at the dev mode \[at production this is proxied to port 443\] . You can specify `MODE=development` to ease in the [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). To associate these variables (or constants) with your `process.env` we require the [dotenv](https://github.com/motdotla/dotenv) package.

📝Please remeber that .env file cannot be uploaded to the Heroku instance or any repository unless otherwise it is specifically not exposed to the public. Heroku does not allow .env files to be parsed, so you need to set up an app and goto `https://dashboard.heroku.com/apps/[REPLACE App name]/settings` and click `REVEAL CONFIG VARS` and manully set the secrets 🤫.

Speaking of CORS, I have a whitelist of domains which can send requests to the backend for verification. This is done by the [CORS Middleware](https://github.com/expressjs/cors).

📦 You can clone the server stuff seperately from [fire-contact-server.git](https://git.heroku.com/fire-contact-server.git).

👇🏻 One click install:

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://git.heroku.com/fire-contact-server.git)


### Scheduling ⏳

> Please note if you do it the Cloud Functions way, you need to have a billing account with Google Cloud.

> If you are willing to pay, please check out [Cloud Firestore triggers on Cloud Function](https://firebase.google.com/docs/functions/firestore-events), which help you to do this much more efficiently.

I have been setting up the Pipedream Scheduling Workflow to go over the task. The scheduling will not immediately trigger a response, but will definitely do it within 1 - 1.5 hours. You need to however have a [Service Account on your Firebase Project](https://firebase.google.com/docs/admin/setup), while this [blog post](https://medium.com/litslink/firebase-admin-sdk-basics-in-examples-ee7e009a1116) is extemely helpful to do the basics.


## Conclusion

Thats it 🍻. I am ready to get your messages 💭 and make some new friends 👥 while have a nice talk 🦜. Send messages @ [https://me.anweshan.online](https://formula21.github.io) now ...

Built with care,
Anweshan Roy Chowdhury (@formula21)
