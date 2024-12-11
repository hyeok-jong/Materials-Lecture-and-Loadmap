
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
5. A project is the best way to review what you have studied. Below are some projects for reference or as checkpoints.  


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
- **Backend**: Runs on a remote server.(Bridge between local PC and DB)  
- Interaction between the two forms the foundation of any app.  

---

# 1. Frontend  

## 1.1 HTML, CSS  
### [HTML & CSS Full Course - Beginner to Pro](https://youtu.be/G3e-cpL7ofc?si=6khpQeP_MXAW5nkh)  
This lecture covers the basics of HTML and CSS. With it, you can build static websites.  

After this, I recommend watching videos on **Flexbox** and **Grid** for better layout management.  


<h2 style="color:red;"> Project 1. </h2>
<p style="color: red;">Create your own static web page as demonstrated in the lecture.</p>  

---

## 1.2 JavaScript  
### [JavaScript Tutorial Full Course - Beginner to Pro (2024)](https://www.youtube.com/watch?v=EerdGm-ehJQ)  
This lecture teaches how to make websites more interactive using the DOM.  
It also introduces generating HTML with JavaScript, a fundamental concept in React.js.  

### [ColorCode - 20 Things JavaScript Developers Should Know](https://www.youtube.com/playlist?list=PL1PqvM2UQiMoGNTaxFMSK2cih633lpFKP)  
Covers advanced JavaScript topics, especially async functions and API calls (Lectures 11–14).  

### [Build a JavaScript WEATHER APP in 30+ minutes!](https://www.youtube.com/watch?v=VaDUGPMjzOM)  
A hands-on lecture on building an app using public API calls.  


<h2 style="color:red;"> Project 2. </h2>
<p style="color: red;">Create your own static web page as demonstrated in the lecture. Generate your HTML code dynamically using JavaScript. And use DOM.</p>

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


<h2 style="color:red;"> Project 3. </h2>
<p style="color: red;">Create your own web with React. And use Routes for multiple pages.</p>



### [React 입문자들이 알아야할 Redux 쉽게설명 (8분컷)](https://www.youtube.com/watch?v=QZcYz2NrDIs)  
Explains why Redux is needed and its core concepts.  

### [React Redux](https://www.youtube.com/playlist?list=PLuHgQVnccGMDuVdsGtH1_452MtRxALb_7)  
Walks through props → Redux → React Redux, highlighting the benefits of React Redux for managing complex state and reducing unnecessary props.  

### [react-redux(2022 ver)](https://youtu.be/yjuwpf7VH74?si=RWQdZGgZM-xIsFdq)  

### [Redux toolkit](https://www.youtube.com/watch?v=9wrHxqI6zuM)  


<h2 style="color:red;"> Project 4. </h2>
<p style="color: red;">Create your own web with React. And use react-redux for global state.</p>




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

Although you can build servers using just **Node.js**, starting directly with Express.js shouldn’t cause major issues.(I think)  

I’ve decided to focus on this **Express-only** lecture for now.  

It’s true that learning with vanilla Node.js first could provide a deeper understanding, but I trust my current approach. It’s similar to how I use **torch** without first creating modules from scratch with NumPy—it’s fine as long as I understand the fundamentals.  

If needed later, I can refer to this YouTuber’s Node.js lecture: [Vanilla Node.js Server Tutorial](https://www.youtube.com/watch?v=32M1al-Y6Ag).  



<h2 style="color:red;"> Project 5. - CRUD Proejct (w/o DB)</h2>  

<p style="color: red;">Create your own application using React and Express. Please refer to my repository below.</p>
<p style="color: red;">In the repository, I have utilized everything we learned so far, allowing you to review and consolidate all the concepts covered above.</p>


### [github repo](https://github.com/hyeok-jong/crud-project)  



## 2.3 MongoDB  
### [MongoDB Crash Course](https://youtu.be/ofme2o29ngU?si=sKzwqO4ShNm6yuj7)  
Nice explain of MongoDB with multiple examples.  

## 2.4 Mongoose  
### [Mongoose Crash Course - Beginner Through Advanced](https://www.youtube.com/watch?v=DZBGEVgL2eE)



<h2 style="color:red;"> Project 5. - CRUD Proejct (mini todo app)</h2>  

<p style="color: red;">Create your own application using React, Express, and MongoDB. Please refer to my repository below.</p>
<p style="color: red;">In this resposityofy 해당 앱은, DB를 사용하여 ㄹ.</p>

### [github repo](https://github.com/hyeok-jong/crud-project)  







## 2.5 Next Step

- Here, you have learned everything needed to prepare for building an application.  
- This includes creating a web page with React, a server with Express, and a database with MongoDB.  
- However, currently, all these components are running on your local PC.  
- For a real-world application, each of these should ideally run on the cloud. (Of course, it's also possible to run and deploy them from your local PC.)  
- To build a true application, you need to learn about MongoDB Atlas, Docker, and AWS services such as S3 and ECS.  



# 3. Application.  
- As mentioned earlier, the application will be deployed to the cloud.  
- First, upload MongoDB to ensure the database runs smoothly in the cloud.  
- Next, learn Docker to prepare for deploying the backend (API).  
- Deploy the backend to ECS and verify that the React project runs properly on the local environment.  
- Finally, build the React project and upload it to S3. Once this is done, the process is complete.  




## 3.1 MongoDB Atlas  

## 3.2 Docker  


## 3.2 AWS ESC  


## 3.3 AWS S3  

## 3.4 AWS CloudFront  

## 3.5 Certificate Manage  




# 4. DB Backup


# YouTube Teacher Recommendations  
- [SuperSimpleDev](https://www.youtube.com/@SuperSimpleDev/videos)  
- [ColorCode](https://www.youtube.com/@ColorCode-io)  
- [Traversy Media](https://www.youtube.com/@TraversyMedia)  








## 2.5 JWT, Express, and MongoDB(Local PC).  

1. Send Login Data: Browser sends username and password to the server.  
2. Create JWT: Server verifies the credentials and generates a JWT using a secret key.  
3. Return JWT: Server sends the generated JWT back to the browser.  
4. Store JWT: Browser stores the JWT (e.g., in localStorage or cookies).  
5. Send Authenticated Request: Browser includes the JWT in the Authorization header for subsequent requests.  
6. Validate JWT: Server validates the JWT to ensure the request is authenticated.  
7. Return Response: Server processes the request and sends the response back to the browser.  



# TBD  
web socket for chat app






### [User Authentication and Authorization in Express and MongoDB using JWT](https://medium.com/@it.ermias.asmare/user-authentication-and-authorization-in-express-and-mongodb-using-jwt-643503a23452)

### [Node.js + MongoDB: User Authentication & Authorization with JWT](https://www.bezkoder.com/node-js-mongodb-auth-jwt/)
