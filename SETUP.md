# ARSH FREE FIRE CUP — v2 setup

This is a frontend that uses Firebase for **real phone SMS OTP**, Firestore registrations/settings, and Storage for payment screenshots and QR images. It does not use fake OTPs. It will not work fully until Firebase is configured.

## 1. Firebase project
1. Open https://console.firebase.google.com and create a project.
2. Add a Web app (</>), register app, copy the Firebase web config.
3. In `index.html`, replace the `firebaseConfig` placeholder values with your app config.
4. Firebase Console → Authentication → Sign-in method → enable **Phone** and **Email/Password**.
5. Authentication → Settings → Authorized domains: add your Vercel domain (e.g. `arsha-free-fire-cup.vercel.app`).
6. Phone authentication requires reCAPTCHA and SMS; Firebase may require billing/quotas and SMS delivery is subject to provider limits/costs.

## 2. Admin account
Firebase Authentication → Users → Add user, create your admin email/password. Sign in once. Copy the admin user's **UID**.

## 3. Firestore
Create Firestore Database (production mode). Publish the `firestore.rules` from this package. Replace `YOUR_ADMIN_UID` with the UID copied above.

## 4. Storage
Enable Firebase Storage. Publish `storage.rules`, replacing `YOUR_ADMIN_UID` with your admin UID. These rules allow verified phone users to upload their own payment proof; admin can manage QR files.

## 5. Deploy
Replace the repo's `index.html` with this package's `index.html` and commit to `main`. Vercel should auto-deploy. Verify the Vercel domain is authorized in Firebase.

## 6. Important
- Payment is not automatically verified. Admin checks UTR and proof, then marks Pending/Verified/Rejected.
- The contact number shown is 9381327705; it is not the OTP sender. Firebase sends OTP to each player's mobile number.
- Keep Firebase config in the frontend (normal for Firebase web apps); **security is enforced by rules**, not by hiding config.
- Do not put admin UID, service-account keys, private API keys, or passwords in public code beyond the Firebase public web config. Never share service account credentials.
