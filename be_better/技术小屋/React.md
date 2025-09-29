## What is React ?
react is a javascript library used to create web applications 
## Create React Project
(Vite + React)
run in cmd
`npm create vite@latest projectname -- --template react`
run in project terminal
`npm install`
run the project
`npm run dev`
## React Usage Notes
### Components
![[Pasted image 20250819122900.png]]
split up the *different parts* of this web page into *different components*
#### step1 write your components
write as function and remenber export `export defualt Name` so that other jsx can import this component .
![[Pasted image 20250819182155.png]]
==attention: if you have many part in your return, there will be error. remenber put them in one `<></>` as the example followed==
![[Pasted image 20250819183433.png]]
#### step2 use your components after writing
import component with relative path . `./`
like `import Todo from "./components/Todo.jsx"`
and then use your components as a part by `<component />`
![[Pasted image 20250819182942.png]]
### Props
props allow us to make our components dynamic
#### step1 creating props
#### step2 using props
### Event Handling
event handling is just executing some code when an exent occurs
### React Hooks
the most important two hooks: useState , useEffect
#### useState
 useState is how we create variables in react
 and the reason why we use useState instead of a regular javascript variable is that whenever the useState variable changes in value it's actually going to render.
##### conditonal rendering
rendering an element based on whether a conditon is true or false
![[Pasted image 20250819234937.png]]

##### change base on the prevarous
 if your variable change *base on the prevarous one* , use the *() => {}* instead of the normal one . 

if your variable is a *object* and just want to change a property, need to use `...preUser`
![[Pasted image 20250820113333.png]]

##### Emitting Events
![[Pasted image 20250820114636.png]]
==pass function as a prop to child' component ==
![[Pasted image 20250820114716.png]]
#### useEffect
used before `return`
it's running as soon as our component ==first renders==
a very common use case for this userEffect hook is to fetch some data as soon ase page first loads
`useEffect( () => {}, [] )`
![[Pasted image 20250820120541.png]]
as this example, `console.log` will run at the page first loads and when the `popupOpen` is true
### Routing
routing allows you to navigate to different pages on your app
run this code in terminal `npm install react-router-dom`

![[Pasted image 20250820135810.png]]
whenever we want to use react router, all have to be *inside* of router(BrowserRouter)
==take notes==: use `<Link>` instead of `<a>` can avoid refresh
#### dynamic routing
create one route and *make it dynamic* so that it can be used *across all the different users*

### APIs in React
how do we fetch data from APIs in React? Fetch or Axios
install axios by runing this code `npm install axios` in terminal
