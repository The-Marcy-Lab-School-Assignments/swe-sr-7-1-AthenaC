# Technical Writing Assignment

For guidance on setting up and submitting this assignment, refer to the Marcy lab School Docs How-To guide for [Working with Short Response and Coding Assignments](https://marcylabschool.gitbook.io/marcy-lab-school-docs/fullstack-curriculum/how-tos/working-with-assignments#how-to-work-on-assignments).

## Prompt 1

In your own words, explain why React is a popular choice for building user interfaces. Make sure to mention at least one benefit, such as how it simplifies development, supports reusable components, or helps optimize performance. Feel free to include any specific features you find particularly helpful.

### Response 1

> React is popular because it simplifies the process of building interactive and dynamic user interfaces. One key benefit is its component-based architecture, which allows developers to create reusable components. This leads to cleaner, more maintainable code since you can reuse the same component across different parts of an app, reducing redundancy.
>
> Additionally, React's virtual DOM enhances performance by only updating parts of the UI that have changed, rather than re-rendering the entire page. This results in faster and more efficient updates, especially in larger applications.
>
> Other features, like JSX (JavaScript XML), make it easier to write and read the code, as you can mix HTML-like syntax with JavaScript logic in a seamless way. React's ecosystem, including tools like React Router and state management libraries, further supports developers in creating scalable and smooth user experiences.

## Prompt 2

Explain how the useState hook is used in React to manage state within functional components. In your response, include an example of how useState might be used in a simple application and why managing state is important in building interactive user interfaces.

### Response 2

The `useState` react hook allows components to maintain and update local state(data) without manually having to re-render a webpage. Instead, components re-render when data changes, making user interfaces dynamic and interactive. Without this, user actions like clicking a button, typing in an input, or toggling visibility wouldn't reflect updates properly.

To declare a variable with the `useState` react hook, you have to declare it, since it is a function. the `useState()` function takes in an initial value, and returns an array. The array contains the variable name, and a setter function that will be called when the state is updated.

In this code block, we see these concepts demonstrated.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // count variable declared & starts at 0

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  ); // setCount function called to update and re-render page when button is clicked and count is updated
}
```

## Prompt 3

Describe the different ways the useEffect hook can be triggered in a React component. Include an explanation of how the dependency array influences its behavior. If possible, provide a code example for each scenario to illustrate your explanation.

### Response 3

## Prompt 4

The component below makes a mistake when using useEffect. When running this code, we will get an error from React! Please fix this code.

```js
const DogDisplay = () => {
  const [imgSrc, setImgSrc] = useState(
    "https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg"
  );

  useEffect(async () => {
    try {
      const response = await fetch("https://dog.ceo/api/breeds/image/random");
      if (!response.ok) throw new Error(`Error: ${response.status}`);
      const data = await response.json();
      setImgSrc(data.message);
    } catch (error) {
      console.error(error);
    }
  }, []);

  return <img src={imgSrc} />;
};
```

After fixing the code provide and explanation to what you fixed and why it needed to be fixed.

### Response 4

> The issue in the code arises from using an `async` function directly within the `useEffect` hook, which React doesn't support because it expects the callback to return either `void` or a cleanup function, not a promise. To fix this, I moved the `async` logic into a separate function (`fetchDogImage`) inside the `useEffect` and called it. Additionally, I added the `alt` to the `img` in case the image did not load.
>
> ```js
> const DogDisplay = () => {
>   const [imgSrc, setImgSrc] = useState(
>     "https://images.dog.ceo/breeds/hound-english/n02089973_612.jpg"
>   );
>
>   useEffect(() => {
>     const fetchDogImage = async () => {
>       try {
>         const response = await fetch(
>           "https://dog.ceo/api/breeds/image/random"
>         );
>         if (!response.ok) throw new Error(`Error: ${response.status}`);
>         const data = await response.json();
>         setImgSrc(data.message);
>       } catch (error) {
>         console.error(error);
>       }
>     };
>     fetchDogImage();
>   }, []);
>
>   return <img src={imgSrc} alt="random dog image" />;
> };
> ```
