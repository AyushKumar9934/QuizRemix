# Remix Quiz App

This project is made in **Remix** by **Ayush Kumar (ayush848209@gmail.com, 9142818533)**.

## How to Install the Project

1. Clone the repository:  
   `git clone --recurse-submodules https://github.com/AyushKumar9934/QuizRemix.git`  
2. Install the root module:  
   `npm i`  
3. Change the directory:  
   `cd .\my-remix-app\`  
4. Install project-required modules:  
   `npm i`  
5. Start the project:  
   `npm run dev`  

The app will run on **[http://localhost:5173/](http://localhost:5173/)**.

## Home Page

The home page will look like this:  

![Home Page](https://github.com/user-attachments/assets/c8353811-13e3-48fc-a262-919d7f94c278)  

- **Features:**  
  i) Two buttons for exploring user and admin views.  
  ii) Clicking "Admin View" shows the admin interface.  

## Admin View

The admin view looks like this:  

![Admin View](https://github.com/user-attachments/assets/e6775ac7-4643-4c23-9377-2d4ffccdf7f0)  

- **Features:**  
  a) Three-column grid layout:  
     - Column 1: Icons.  
     - Column 2: Drag different layouts.  
     - Column 3: Drop selected quiz layouts.  
  b) Drag-and-drop sets the quiz layout for the user view.  
  c) Admin can switch back to the user view.  

## User View

The user view displays the layout set by the admin:  

![User View](https://github.com/user-attachments/assets/48bac16c-1360-4f4e-9141-03a919f394d9)  

- **Features:**  
  i) Displays the layout configured by the admin.  
  ii) Quiz card includes:  
     - Previous and Next arrow buttons.  
     - Progress bar showing completed questions.  
     - Numeric view (answered/total questions) and a timer bar.  
     - Image (in specific layouts), options, and a "Check Answer" button.  
  iii) Options change color on hover and click.  
  iv) "Check Answer" highlights the correct option in green.  

## Business Logic for our Project

i) Initially, we need the two views, i.e., user view and admin view, so I have created two routes for the same inside the `routes` folder named `admin.tsx` and `user.tsx`, which can be rendered by the `_index.tsx` (home page) by adding two buttons and linking them to the respective routes.  
ii) For storing the layout set by the admin, I have made a **Layout.json** file at the root level, and initially, all the questions are stored in **questions.json**.  
iii) For the implementation of drag and drop, I have used the `react-dnd` library. I have wrapped the **admin component in DndProvider** for access to its drag-and-drop functionality. **I have mapped Layout1 with id=1, Layout2 with id=2, and so on. On drop, we send the id with the help of `fetch('/admin')` inside the `useEffect` hook.**  

### Logic in Admin Router

iv) **Now we have an action function that accepts the request as a prop and extracts the layout id from the request. Then it sets the layout in Layout.json by calling the function `setLayout(currentLayoutId)`. The `setLayout` function is defined to write the data to the file.**

### Logic in User Router

**Now we get the admin set layout (which is in Layout.json) and all questions in question.json by the loader function with the help of the helper functions `getStoredLayout` and `getAllQuestions`. It returns a response and sends a new response from the backend to the frontend. We get this response by using the `useLoaderData` hook.**  
**Now we render the particular layout passing all questions as props based on the response id received from `useLoaderData`.**

### For a Particular Layout

i) We map all questions received in props and handle clicking options and the "Check Answer" button.
