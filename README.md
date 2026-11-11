# Adarsh Agri Science — Order Management Portal

This is the deployment package for the Adarsh Agri Science order-management website. The supplied Adarsh logo is already installed as `adarsh-logo.png`.

## Before the website can go live

This portal uses Firebase Authentication and Cloud Firestore for secure staff/HQ logins and shared live orders. A static hosting service alone cannot provide the database.

1. Create a Firebase project at https://console.firebase.google.com/ and add a Web app.
2. In `index.html`, replace the six placeholder values in `firebaseConfig` (`YOUR_API_KEY`, `YOUR_PROJECT_ID`, etc.) with your Firebase Web app configuration.
3. Enable **Authentication → Email/Password**.
4. Create a Firestore database and publish the included `firestore.rules` rules.
5. Create each user in Firebase Authentication. In Firestore, create a `users` document with that user's Authentication UID as its document ID. Use `{ "role": "staff", "branch": "Birgunj" }` for branch staff or `{ "role": "hq", "branch": "HQ" }` for head office.
6. Test branch and HQ accounts before using real orders.

## Publish free with GitHub Pages

1. Sign in to GitHub and create a new **public** repository, e.g. `adarsh-order-management`.
2. Upload the four files in this folder to the repository's top level (not inside another folder).
3. Open **Settings → Pages**. Under Build and deployment, choose **Deploy from a branch**, select `main` and `/(root)`, then Save.
4. GitHub will show the public website URL in the Pages section after deployment completes.

## Security

- Do not upload Firebase Admin SDK keys or service-account JSON files.
- The Firebase browser configuration is public by design; access control must be enforced by Firebase Authentication and the included Firestore rules.
- Assign user roles only through Firebase Console or a trusted server/Admin SDK. The rules prevent users from changing their own role documents.
- Test the rules in a non-production Firebase project before handling business data.

## Included workflow

Branch staff create orders → HQ accepts → HQ records invoice and dispatch details → branch staff confirm received quantities and create a printable GRN. The portal also provides live order updates and CSV export.
