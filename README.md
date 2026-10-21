# Login-Management-System

A React single-page app for account management with Firebase Authentication: sign up, log in, reset a forgotten password, view a profile, and update the account email or password.

**Status:** Working demo. The sign-up, log-in, password-reset, dashboard, profile-update and log-out flows are all wired to Firebase Auth in code, and private routes redirect signed-out users to the login page. It is not deployed from the repo, and it has no tests.

## The problem

Most apps need a standard set of account screens before any real feature can be built. This project builds those screens on top of Firebase so the account flow can be reused or studied on its own.

## What it does

- **Sign up (`src/components/SignUp.js`)**: creates an account with email and password through Firebase.
- **Log in (`src/components/Login.js`)**: signs in with email and password.
- **Forgot password (`src/components/ForgotPassword.js`)**: sends a password reset email.
- **Dashboard (`src/components/Dashboard.js`)**: shows the signed-in user's email and a log-out button.
- **Update profile (`src/components/UpdateProfile.js`)**: changes the account email or password through the Firebase user object.
- **Private routes (`src/components/PrivateRoute.js`)**: the dashboard and profile pages redirect to `/login` when no user is signed in.

## How it's built

- **Frontend**: React 17 with Create React App (react-scripts 4), React Router 5 and react-bootstrap for layout and forms.
- **Auth state**: `src/context/AuthContext.js` subscribes to `onAuthStateChanged` and exposes sign-up, sign-in, sign-out, reset and update functions through a React context. Components call `useAuth()` rather than Firebase directly.
- **Config**: `src/firebase.js` reads the Firebase project settings from `REACT_APP_FIREBASE_*` environment variables.
- **Decision**: one context owns the auth state and the routes stay declarative, so the screens never call Firebase themselves.

## Running it locally

Create a `.env` file with the `REACT_APP_FIREBASE_*` values for a Firebase project that has email and password sign-in enabled, then:

```bash
npm install
npm start    # react-scripts start, with --openssl-legacy-provider
npm run build
npm test     # react-scripts test
```

## What's left

- The test libraries are installed, but there are no test files.
- `firebase.js` reads a database URL from the environment, but the code only imports `firebase/auth`.
- Firebase SDK v8 and react-scripts 4 are old major versions, and the start script needs `--openssl-legacy-provider` to run on current Node.
- The Firebase config is read from environment variables, so the repo does not set up a project for you.
