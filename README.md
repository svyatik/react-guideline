# Arootah - Coding Style Guideline (Front-end)
A code style guide with best practices with additional notes on performance & optimizations.

Following the style guide will help maintain consistency and readability of code across a project and team, which can improve code quality and reduce errors. It can also make it easier for new developers to onboard and understand the codebase.

---

## Table of Contents

- [Style Code Guide](#code-style-guide)
    - [File Structure and Naming](#file-structure-and-naming)
    - [Formatting](#formatting)
    - [JavaScript](#javascript)
    - [React](#react)
    - [CSS Styling](#css-styling)
    - [Testing](#testing)
- [Performance & Optimizations](performance--optimizations)
- [GitHub Best Practices](#github-best-practices)
    - [Semantic Commit Messages](#semantic-commit-messages)
    - [Branches](#branches)

## Code Style Guide

---

### File Structure and Naming

- Organize your files into components, containers, actions, reducers, selectors, and utils folders.
- Each project has to be located in an isolated folder with its own redux and style system setup.
- Use **PascalCase** for component and container file names (e.g. `MyComponent.js`, `MyContainer.js`), and **camelCase** for action, reducer, selector, and util file names (e.g. `myAction.js`, `myReducer.js`, `mySelector.js`, `myUtil.js`).
- Use `index.js` files to export from a folder, and avoid importing from nested files.
- Use meaningful and descriptive names for all files and folders.

Example File Structure:

```
├── node_modules
└── src
    ├── api
    ├── assets
    ├── components
    │   ├── LoginForm
    │   ├── Project1
    │   │   ├── CustomButton
    │   │   │   ├── index.js
    │   │   │   └── styles.module.scss
    │   │   ├── ProfileForm
    │   │   │   ├── index.js
    │   │   │   └── styles.module.scss
    │   │   └── Table
    │   │       ├── index.js
    │   │       └── styles.module.scss
    │   ├── Project2
    │   ├── RegisterForm
    │   └── index.js
    ├── constants
    │   └── index.js
    ├── scenes
    │   ├── Dashboard
    │   ├── Login
    │   │   ├── index.js
    │   │   └── styles.module.scss
    │   ├── Project1
    │   │   ├── Dashboard
    │   │   │   └── index.js
    │   │   ├── Profile
    │   │   │   └── index.js
    │   │   └── Settings
    │   │       └── index.js
    │   ├── Project2
    │   └── index.js
    └── state
        ├── auth
        ├── project1
        │   ├── addExampleData
        │   │   ├── action.js
        │   │   ├── reducer.js
        │   │   └── types.js
        │   └── getExampleData
        │       ├── action.js
        │       ├── reducer.js
        │       └── types.js
        ├── project2
        ├── rootReduer.js
        └── store.js
```

### Formatting
- Use two spaces for indentation. Avoid using tabs.
- Use single quotes for strings, and double quotes for JSX attributes.


### JavaScript
- Use ES6+ features, including arrow functions, template literals, destructuring, and spread syntax.
- Use `const` and `let` instead of var for variable declarations.
- Avoid using global variables and functions.
- Use meaningful and descriptive variable and function names.
- Use functional programming techniques, such as pure functions and immutability.
- Use semicolons to terminate statements.
- Always use braces for if statements, loops, and functions.
- Use the `===` and `!==` operators for equality comparisons.
- Use trailing commas in multi-line object and array literals.
- Avoid using unnecessary parentheses in expressions.
- Use object shorthand syntax for concise object declarations.
- Use async/await syntax instead of callbacks or promises.
- Use default parameters to set default values for function arguments.
- Use the ternary operator for simple if/else statements.
- Use semicolons;

### React
- Use functional components instead of class components.
- Use the `useState` and useEffect hooks for managing component state and side effects.
- Use conditional rendering to control the display of components.
- Use `React.memo` to memoize functional components for performance optimization.
- Use the `useContext` hook to access global data without passing props down through multiple components.
- Use the `useCallback` hook to memoize callback functions and avoid unnecessary re-renders.
- Avoid using anonymous arrow functions inside JSX tree as this can cause unnecessary re-renders of the component, since a new function is created on each render.

#### Examples
##### Bad Code Example:

```
import React, { useState } from 'react';

function MyComponent(props) {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Current Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  )
}

```

This code has the following formatting issues:

* The logic is directly placed inside the onClick event handler, making it harder to read and maintain the code.
Using an anonymous arrow function inside onClick can cause unnecessary re-renders of the component, since a new function is created on each render.


##### Good Code Examples:

```
import React, { useState } from 'react';

function MyComponent(props) {
  const [count, setCount] = useState(0);

  function handleIncrement() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Current Count: {count}</h1>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
}
```
This code has the following formatting improvements:

* The handleIncrement function is defined and then passed as a reference to the onClick event handler, making the code more readable and maintainable.
The useState hook is used to manage the component's state, rather than directly modifying it, which is a best practice in React development.

### CSS Styling
 - Use CSS frameworks or libraries: Bootstrap and Antd, to speed up development and ensure consistency.
 - Use Styled Components or CSS Modules depending on the project. There are advantages or disadvantages of each of the option, for global components both can be used interchangeably.
 - Use a linter, such as stylelint, to enforce consistent and maintainable CSS styles.
 - Prefer .svg over .png (.jpg) for icons. Consider converting an .svg icon to a reusable component with props to control the size and color
 - Prefer .webp over .png (.jpg) for images.

### Testing
#### A walkthrough guide how to perform testing of React application

* Identify components to test: Determine which components need to be tested. Typically, you want to test components that have complex logic, state management, or user interactions.

* Write unit tests: Write unit tests for each component. Unit tests should cover individual functions, props, and state changes of the component.

* Write integration tests: Write integration tests to test the interaction between multiple components.

* Write end-to-end tests: Write end-to-end tests to test the entire flow of the application, from the user's perspective. Use tools like Cypress or Selenium for this.

* Mock dependencies: Use mocking libraries to mock any external dependencies, like APIs or data sources.

* Run tests regularly: Run tests regularly to ensure that they are up to date and that changes to the code don't break existing tests.

* Automate tests: Automate the testing process using continuous integration tools like Travis CI or Jenkins.

* Debug failing tests: Debug any failing tests and fix the code accordingly.

* Refactor tests: As the code evolves, refactor tests to ensure they remain accurate and up to date.


#### Example
Let's say you have a simple component that displays a message, like this:

```
import React from 'react';

function Message(props) {
  return (
    <div className="message">{props.text}</div>
  );
}

export default Message;
```

To test this component using Jest and Enzyme, you would write a test code like this:

```
import React from 'react';
import { shallow } from 'enzyme';
import Message from './Message';

describe('Message', () => {
  it('renders the message text', () => {
    const wrapper = shallow(<Message text="Hello, world!" />);
    const message = wrapper.find('.message');
    expect(message.text()).toEqual('Hello, world!');
  });
});
```

Here's what this code does:

1. We import the necessary libraries: React, Enzyme, and our component.
2. We use the Jest `describe` function to group our tests together.
3. We use the Jest `it` function to define a single test case.
4. In the test case, we create a new instance of our component using Enzyme's `shallow` function.
5. We find the element with the `.message` class using Enzyme's `find` function.
6. We use the Jest `expect` function to test that the message text is equal to "Hello, world!".

By following these steps, you can write test code for your React components using Jest and ensure that they function correctly.


## Performance & Optimizations


---


#### List of guidelines on how to write an optimized for performance React / Redux application:


* Use the latest versions of React and Redux: Always make sure you are using the late

* Use the useSelector and useDispatch hooks: Use the useSelector and useDispatch hooks provided by React-Redux to optimize your data flow. These hooks use the useSelector and useDispatch functions from Redux internally and provide a more concise syntax.

* Use memoized selectors: Use memoized selectors to avoid unnecessary computations and re-renders. Memoization is a technique of caching the results of a function so that it can be returned without re-computing if the input arguments remain the same.

* Normalize your Redux state: Normalize your Redux state to optimize data retrieval and management. Normalization is a technique of structuring your state in a way that allows you to easily query it and avoid unnecessary computations.

* Use lazy loading: Use lazy loading to improve the initial load time of your application. Lazy loading is a technique of deferring the loading of non-critical parts of your application until they are actually needed.

* Optimize images and media: Optimize your images and media by compressing them and using optimized formats such as WebP. Also, consider using lazy loading to defer the loading of images until they are needed.

* Use server-side rendering: Use server-side rendering to improve the initial load time of your application. Server-side rendering is a technique of rendering your application on the server and sending the HTML to the client, which can be displayed immediately.

* Use code splitting: Use code splitting to reduce the size of your JavaScript bundle and improve the initial load time of your application. Code splitting is a technique of splitting your JavaScript code into smaller chunks that can be loaded on demand.

* Use caching: Use caching to improve the performance of your application by avoiding unnecessary network requests. Caching is a technique of storing the results of network requests so that they can be returned immediately if the same request is made again.

* Use compression: Use compression to reduce the size of your network requests and improve the performance of your application. Compression is a technique of compressing your network requests so that they can be transferred more quickly.

* Monitor performance: Use tools such as Google Analytics and New Relic to monitor the performance of your application and identify bottlenecks. This will allow you to make targeted optimizations to improve the overall performance of your application.

* Test and debug: Use automated testing and debugging tools such as Jest, Enzyme, and React Developer Tools to ensure that your application is optimized and error-free.


## GitHub Best Practices

---

### Semantic Commit Messages
Using a semantic approach to writing commit messages can make it easier for other developers to understand the changes that were made, and can help you keep track of changes over time.

Format: `<type>(<scope>): <subject>`
`<scope>` is optional

#### Example

```
feat: add login popup
^--^  ^------------^
|     |
|     +-> Summary.
|
+-------> Type: chore, docs, feat, fix, refactor, style, or test.
```

More Examples:
- `feat`: a new feature or functionality was added
- `fix`: a bug or issue was fixed
- `chore`: changes to build process, project configuration, or other non-code related tasks
- `docs`: documentation was added or updated
- `test`: changes to test cases or testing environment
- `refactor`: refactoring production code, eg. renaming a variable


### Branches

Here are some best practices to follow when working with branches in Git:

* Use descriptive and meaningful branch names: Branch names should be descriptive and meaningful, so that other developers can easily understand what changes the branch contains.

* Create branches for each feature or bug fix: Create a new branch for each feature or bug fix you are working on. This allows you to work on multiple changes simultaneously without interfering with each other.

* Use feature branches: Use feature branches to isolate your work and avoid conflicts with other developers. This makes it easier to collaborate with others and reduces the risk of breaking the main codebase.

* Keep your branches small and focused: Keep your branches small and focused on specific tasks. This makes it easier to review and merge changes, and reduces the risk of introducing bugs or conflicts.

* Regularly merge changes from the main branch: Regularly merge changes from the main branch into your feature branches to keep them up to date and avoid conflicts. This also ensures that your changes will work with the latest version of the code.

* Use pull requests for code review: Use pull requests to request code review from other developers. This allows others to review your changes and provide feedback before they are merged into the main codebase.

* Delete branches after they are merged: Delete branches after they are merged to keep your Git repository clean and organized. This makes it easier to manage branches and reduces the risk of confusion or conflicts.

* Use a consistent branching strategy: Use a consistent branching strategy, such as Gitflow or Trunk-based development, to ensure that everyone on the team is following the same process. This makes it easier to collaborate and reduces the risk of conflicts or errors.

* Use tags to mark important commits: Use tags to mark important commits, such as releases or milestones. This makes it easier to track changes and roll back to previous versions if necessary.

* Backup important branches: Backup important branches, such as the main branch or release branches, to a remote repository or cloud storage service. This ensures that your code is safe and can be recovered if something goes wrong.
