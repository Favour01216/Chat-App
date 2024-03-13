# Realtime Chat App

This is a realtime chat application built using Svelte and Firebase. It allows users to log in with their Google account and engage in chat conversations with other users in real time.

## Features

- **Google Authentication**: Users can log in to the chat application using their Google account.
- **Realtime Messaging**: Chat messages are sent and received in real time, allowing for seamless communication.
- **Responsive Design**: The application is designed to work well on various devices, including desktops, tablets, and smartphones.
- **Avatar Support**: Users can see avatars of other chat participants next to their messages.
- **Custom Styling**: The user interface is styled using custom CSS for an appealing and user-friendly experience.

## Technologies Used

- **Svelte**: A modern JavaScript framework for building user interfaces.
- **Firebase**: A platform provided by Google for building web and mobile applications. Firebase is used for authentication and real-time database functionality.
- **RxJS**: A library for reactive programming using Observables.
- **Rollup**: A module bundler for JavaScript applications.

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/Favour01216/Chat-App.git


## Project Setup

1. **Navigate to the project directory:**

    ```bash
    cd realtime-chat-app
    ```

2. **Install dependencies:**

    ```bash
    npm install
    ```

3. **Set up Firebase:**

    - Create a Firebase project at Firebase Console.
    - Enable Google authentication in the Firebase Authentication section.
    - Create a Firestore database in the Firebase Database section.
    - Go to Project Settings > General and copy your Firebase SDK snippet.

4. **Configure Firebase:**

    - Create a file named `firebaseConfig.js` in the `src` directory.
    - Paste your Firebase configuration object into `firebaseConfig.js`.
    - Export the configuration object as `firebaseConfig`.

    ```javascript
    // firebaseConfig.js
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_STORAGE_BUCKET",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    export default firebaseConfig;
    ```

5. **Replace the Firebase import in `firebase.js` with your new configuration:**

    ```javascript
    // firebase.js
    import firebaseConfig from "./firebaseConfig";
    ```

6. **Run the application:**

    ```bash
    npm run dev
    ```

7. **Open your browser and navigate to http://localhost:8080 to see the application running.**

## Usage

- Log in with your Google account.
- Start chatting with other users in real time.
- Log out when you're done.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Usage 
 This image shows the app with one side in a private browser  window and the other side using a regular window.
 ![image showing the chat app](./src/images/chat%20app.png)

