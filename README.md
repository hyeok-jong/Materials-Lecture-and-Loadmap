
# Materials-Lecture-and-Loadmap

### Experience Before Full Stack  
- Conda  
- Docker  
- Python for deep learning and data analysis  
- Torch (modeling and training with DDP)  
- Blogs with Minimal Mistakes and Hugo  
- Flask app hosting on GCP  
- Basic familiarity with Linux  
- Git and Github  

---

### How I Study  
1. I follow lectures step-by-step.  
2. I ensure I understand concepts so I can replicate them without needing the lecture again.  
3. With internet access or LLMs, I can independently research and implement the functions I want to create.  
4. Currently, I can write over 80% of my code independently in an offline setting (without external help).  

---

### Recommendations  
- Don’t rely too much on lectures.  
- Use GPT effectively as a tool.  
- Don’t try to memorize all the code—no one does. Search for new functions as needed.  
- For styling, find good references or explore beautiful CSS resources.  
- Note everything (like this page) to review later instead of memorizing.  
- Keep notes focused on concepts, not detailed descriptions, for quick reference. For example, write "properties can send data between components."  
- Work on as many projects as possible to strengthen your skills.  

---

# 0. Concepts  
- **Frontend** (client): Runs on your local machine.  
- **Backend**: Runs on a remote server.  
- Interaction between the two forms the foundation of any app.  

---

# 1. Frontend  

## 1.1 HTML, CSS  
### [HTML & CSS Full Course - Beginner to Pro](https://youtu.be/G3e-cpL7ofc?si=6khpQeP_MXAW5nkh)  
This lecture covers the basics of HTML and CSS. With it, you can build static websites.  

After this, I recommend watching videos on **Flexbox** and **Grid** for better layout management.  

---

## 1.2 JavaScript  
### [JavaScript Tutorial Full Course - Beginner to Pro (2024)](https://www.youtube.com/watch?v=EerdGm-ehJQ)  
This lecture teaches how to make websites more interactive using the DOM.  
It also introduces generating HTML with JavaScript, a fundamental concept in React.js.  

### [ColorCode - 20 Things JavaScript Developers Should Know](https://www.youtube.com/playlist?list=PL1PqvM2UQiMoGNTaxFMSK2cih633lpFKP)  
Covers advanced JavaScript topics, especially async functions and API calls (Lectures 11–14).  

### [Build a JavaScript WEATHER APP in 30+ minutes!](https://www.youtube.com/watch?v=VaDUGPMjzOM)  
A hands-on lecture on building an app using public API calls.  

---

## 1.3 React.js  

### [2022 코딩애플 리액트 강의](https://www.youtube.com/watch?v=00yJy7W0DQE&list=PLfLgtT94nNq0qTRunX9OEmUzQv4lI4pnP)  
Great for understanding the basics of React, including state and components.  

### [React Full Course for Free ⚛️ (2024)](https://www.youtube.com/watch?v=CgkZ7MvWUAA)  
While not fully comprehensive, this course explains how to transition HTML, CSS, and JS skills into React.  

Topics covered:  
- **Component**: Functions that create reusable blocks of HTML.  
- **Properties**: Pass data (e.g., objects) into components.  
- **style.module.css**: Use `{styles.className}` in JSX for styling components.  
- **useState**: Updates state and triggers re-rendering of only affected components and children. If references don't change (e.g., for lists or objects), rendering won't happen unless you create a new copy.  
- **onClick/onChange**: Simplifies event handling directly in JSX. For DOM manipulation, use `useEffect` to prevent Virtual DOM conflicts.  
- **useRef**: Similar to `useState`, but doesn’t trigger re-rendering when updated.  
- **useEffect**: Runs after the component renders, ideal for DOM manipulation or setting up event listeners.  
- **createContext**: Helps pass data between distant components. Use `.Provider` to pass values and `useContext` in children to consume them.  

### [Learn React Router v6 In 45 Minutes](https://www.youtube.com/watch?v=Ul3y1LXxzdU&list=PLE00K2dj1di6OW5VFsz0rXZeDVhLp8_6L&index=4)  
A concise lecture on using routers in React for creating multiple pages.  

Key topics:  
- **BrowserRouter**: Wraps the `App` component in `index.jsx`.  
- **Routes**: Define multiple components inside `Routes` in `App.js`. Content outside `Routes` (e.g., navigation) persists across route changes.  
- **Route**: Maps `path` (URL) to `element` (component). Example: `<Route path="/login" element={<Login />} />`.  
- **Wildcard Route**: Handles nested routes or undefined paths. Example: `<Route path="*" element={<NotFound />} />` to catch invalid URLs.  

### [React 입문자들이 알아야할 Redux 쉽게설명 (8분컷)](https://www.youtube.com/watch?v=QZcYz2NrDIs)  
Explains why Redux is needed and its core concepts.  

### [생활코딩 - React Redux](https://www.youtube.com/playlist?list=PLuHgQVnccGMDuVdsGtH1_452MtRxALb_7)  
Walks through props → Redux → React Redux, highlighting the benefits of React Redux for managing complex state and reducing unnecessary props.  

---

# 2. Backend  

## 2.0 Getting Started  
### [2시간만에 웹서버 쉽게 개발하기 (코딩애플)](https://www.youtube.com/watch?v=-zOfTS1HQTc&list=PLfLgtT94nNq1qmsvIii_CAxFlD7tvB5NE)  
A quick overview of building web servers using **Node.js**.  

Key topics:  
- HTTP requests: GET, POST, PUT, DELETE  
- Basics of **Node.js** as a JavaScript runtime environment (not a programming language).  
- **Nodemon**: Automatically restarts the server when changes are made.  

---

## 2.1 Node.js  
JavaScript was originally designed for browser use only. However, with the introduction of Chrome's V8 engine, Node.js emerged, enabling JavaScript to run locally. This allowed developers to use JavaScript for server-side development as well.


### [조코딩 Node.js](https://www.youtube.com/watch?v=ZeD8yNMYe-o&list=PLU9-uwewPMe2-R9-taf4oIjwrEZDgE-q2)  
Key topics from the playlist:  

- **Why Node.js?**: It allows JavaScript to run on local machines, not just browsers.  
- **npm init**: Initializes a project for managing dependencies.  
- **npm**: Unlike `pip` or `conda`, it installs packages directory-based, meaning per-project installations.  
- Modules vs. Libraries: For example, **figlet** is a module, while **React** is a library.  
- **Deploying APIs**: Learn to deploy using platforms like Cloudtype.  



## 2.2 Express.js  
### [Express Crash Course](https://www.youtube.com/watch?v=CnH3kAXSrmU&t=53s)  

Although you can build servers using just **Node.js**, starting directly with Express.js shouldn’t cause major issues.  

I’ve decided to focus on this **Express-only** lecture for now.  

It’s true that learning with vanilla Node.js first could provide a deeper understanding, but I trust my current approach. It’s similar to how I use **torch** without first creating modules from scratch with NumPy—it’s fine as long as I understand the fundamentals.  

If needed later, I can refer to this YouTuber’s Node.js lecture: [Vanilla Node.js Server Tutorial](https://www.youtube.com/watch?v=32M1al-Y6Ag).  

## 2.3 Express.js With DB



# 3. AWS  
## 3.0 IAM  
## 3.1 S3  
## 3.2 Route 53  
## 3.3 CloudFront  
## 3.4 Certificate Manage  
## 3.5 Serverless backend server  


# YouTube Teacher Recommendations  
- [SuperSimpleDev](https://www.youtube.com/@SuperSimpleDev/videos)  
- [ColorCode](https://www.youtube.com/@ColorCode-io)  
- [Traversy Media](https://www.youtube.com/@TraversyMedia)  

---

This version ensures consistency and readability without altering your meaning. Let me know if there’s anything more to refine!