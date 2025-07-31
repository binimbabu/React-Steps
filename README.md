Handling Events the React way


const messages = [
  "Learn React ⚛️",
  "Apply for jobs 💼",
  "Invest your new income 🤑",
];

export default function App() {
  const step = 1;
  function handlePrevious() {
    alert("Previous");
  }
  function handleNext() {
    alert("Next");
  }
  return (
    <div className="steps">
      <div className="numbers">
        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
      </div>
      <p className="message">
        Step {step} : {messages[step - 1]}
      </p>
      <div className="buttons">
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handlePrevious}
        >
          Previous
        </button>
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handleNext}
        >
          Next
        </button>
      </div>
    </div>
  );
}



Here i this piece of code ' onClick={handlePrevious}' we are passing function name 'handlePrevious' in onClick event.







State in React

State is a data that a component can hold over time, necessary for information that it needs to remember throughout the app's lifecycle. State can be called as the components memory. State is all pieces of state

Examples of state can be simple things like a notification count, the text content of an input field, or the active tab in a tab component. It can also be more complex data, for example, the content of a shopping cart. What all these pieces of state have in common is that in the application, the user can easily change these values. For example, when they read a notification, the count will go down by one, or when they click on another tab, that tab will become active. Each of these components needs to be able to hold this data over time, over the lifecycle of the application. For that reason, each of these pieces of information is a piece of state.

 A piece of state, or a state variable, is just one single actual variable in the component that we can define in our code. On the other hand, the term state itself refers to the entire state that the component is in, like the entire condition at a certain point in time. Basically, the general term state is all the pieces of state together. If this sounds confusing, don't worry; these are just minor differences in terminology. In practice, we usually use the terms state, piece of state, and state variable quite interchangeably.

When we update a state in a component this will make React to re-render the component in the user interface. Which means it will give new updated view. A web page comprises different components and the group of each components give the entire view or webpage. State will sync User interface with the component data. When state changed the Ui is changed.
State allows developers to update  the component view by re-rendering it, persist local variable's between renders.

State variable created using useState. useState has arguments first argument is the default value. Second argument is the function which returns the state variable.

 In the below example the default value is 1 that is why we give 1 inside useState and setStep as the function which returns the state variable (here state variable is step)

let [step, setStep] = useState(1);

The above code is defining the state variable use the useState function.
We used the state (i.e <div className={`${step >= 1 ? "active" : ""}`}>1</div>
 )
Then update state variable suing setState (i.e in below example setStep(step + 1); )


Full example

import { useState } from "react";

const messages = [
  "Learn React ⚛️",
  "Apply for jobs 💼",
  "Invest your new income 🤑",
];

export default function App() {
  let [step, setStep] = useState(1);
  let [test, setTest] = useState({ name: "Bini" });
  function handlePrevious() {
    if (step > 1) setStep(step - 1);
  }
  function handleNext() {
    if (step < 3) setStep(step + 1);
    setTest({ name: "Babu" });
  }
  return (
    <div className="steps">
      <div className="numbers">
        <div className={`${step >= 1 ? "active" : ""}`}>1</div>
        <div className={`${step >= 2 ? "active" : ""}`}>2</div>
        <div className={`${step >= 3 ? "active" : ""}`}>3</div>
      </div>
      <p className="message">
        Step {step} : {messages[step - 1]} - {test.name}
      </p>
      <div className="buttons">
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handlePrevious}
        >
          Previous
        </button>
        <button
          style={{ backgroundColor: "#7950f2", color: "#fff" }}
          onClick={handleNext}
        >
          Next
        </button>
      </div>
    </div>
  );
}

useState is a hook in React because they start with use keyword. useState can be used initially/top in the component function.
Hooks must be called only at the top level of the component function, not inside loops, conditions, or nested functions.

For example, calling useState inside an if statement or another function will cause errors. state variable using its setState not by manually (i.e setStep in above example). Update the state using only setState here in this example setStep

Array state can be handled in the following way

let [test, setTest] = useState({ name: "Bini" });
setTest({ name: "Babu" });





Mechanics of State

DOM/view cannot be changed by React directly rather React uses State. In react a view is updated by re-rendering the component whenever the underlying data changes. Re-rendering means React calls the component function again each time the component is rendered. Conceptually, we can imagine React removing the entire view and replacing it with a new one each time a re-render needs to happen. State value is preserved throughout the re-render. Even though a component can be rendered and re-rendered many times, the state will not reset unless the component disappears from the UI entirely, which is called unmounting.
When state is updated the component is re-rendered.
When in the view there is a button click happening. In the button click an event handler updates the state using set and re-renders the component and updates the view.
React reacts to state changes by re-rendering the UI.

Full updated example
 
import { useState } from "react";

const messages = [
  "Learn React ⚛️",
  "Apply for jobs 💼",
  "Invest your new income 🤑",
];

export default function App() {
  let [step, setStep] = useState(1);
  let [isOpen, setOpen] = useState(true);
  //let [test, setTest] = useState({ name: "Bini" });
  function handlePrevious() {
    if (step > 1) setStep((st) => st - 1);
  }
  function handleNext() {
    if (step < 3) setStep((st) => st + 1);
    // setTest({ name: "Babu" });
  }
  function close() {
    setOpen((isOpenVal) => !isOpenVal);
  }
  return (
    <>
      <button className="close" onClick={close}>
        &times;
      </button>
      {isOpen && (
        <div className="steps">
          <div className="numbers">
            <div className={`${step >= 1 ? "active" : ""}`}>1</div>
            <div className={`${step >= 2 ? "active" : ""}`}>2</div>
            <div className={`${step >= 3 ? "active" : ""}`}>3</div>
          </div>
          <p className="message">
            Step {step} : {messages[step - 1]}
          </p>
          <div className="buttons">
            <button
              style={{ backgroundColor: "#7950f2", color: "#fff" }}
              onClick={handlePrevious}
            >
              Previous
            </button>
            <button
              style={{ backgroundColor: "#7950f2", color: "#fff" }}
              onClick={handleNext}
            >
              Next
            </button>
          </div>
        </div>
      )}
    </>
  );
}




Each component has and manages its own state no matter how many times we render the same component. 
State is isolated with each other on the component that it uses. Example below

import { useState } from "react";

const messages = [
  "Learn React ⚛️",
  "Apply for jobs 💼",
  "Invest your new income 🤑",
];

export default function App() {
  return (
    <div>
      <Steps />
      <Steps />
    </div>
  );
}

function Steps() {
  let [step, setStep] = useState(1);
  let [isOpen, setOpen] = useState(true);
  //let [test, setTest] = useState({ name: "Bini" });
  function handlePrevious() {
    if (step > 1) setStep((st) => st - 1);
  }
  function handleNext() {
    if (step < 3) setStep((st) => st + 1);
    // setTest({ name: "Babu" });
  }
  function close() {
    setOpen((isOpenVal) => !isOpenVal);
  }
  return (
    <div>
      <button className="close" onClick={close}>
        &times;
      </button>
      {isOpen && (
        <div className="steps">
          <div className="numbers">
            <div className={`${step >= 1 ? "active" : ""}`}>1</div>
            <div className={`${step >= 2 ? "active" : ""}`}>2</div>
            <div className={`${step >= 3 ? "active" : ""}`}>3</div>
          </div>
          <p className="message">
            Step {step} : {messages[step - 1]}
          </p>
          <div className="buttons">
            <button
              style={{ backgroundColor: "#7950f2", color: "#fff" }}
              onClick={handlePrevious}
            >
              Previous
            </button>
            <button
              style={{ backgroundColor: "#7950f2", color: "#fff" }}
              onClick={handleNext}
            >
              Next
            </button>
          </div>
        </div>
      )}
    </div>
  );
}

With state we view Ui as a reflection of data changing over time
We describe that reflection of data using state, event handlers and JSX.


Practical guidelines about state

State variable should track any data that component has over time. For this in Vanilla JavaScript we use let, var, [], {}
When the component need to be dynamic , create a state and update the state say in the event handler function.
Dont use state variables everytime for also creating a simple variable because state updates will re-render the UI which leads to performance issues.
