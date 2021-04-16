# TypeScript notes
**Contents: [Intro](#intro) | [Typewriter](#typewriter) | [TypeScript and React](#typescript-and-react)**

Typescript is a syntactical superset of ECMAScript developed by Microsoft, which adds optional static typing to the language. It cannot natively run in JS environments such as the browser, so needs to be transcompiled to JavaScript before running.


## Intro
### Why TypeScript?
- less error prone due to static typing (reducing need for manual validation / sanitisation)
- additional features that don't exist in JS
- not just a programming language, but also a powerful compiler that runs over your code and compiles it to JavaScript and provides compile-time errors, making it easier to catch errors earlier on in development

> :bulb: TS features are compiled to JS 'workarounds'


## Typewriter
[Typewriter](https://frhagn.github.io/Typewriter/) is a free extension for Visual Studio that generates TypeScript files from C# code files using TypeScript Templates.

This allows you to create fully typed TypeScript representations of server side API, models, controllers etc. that automatically updates when you make changes to your C# code.

By doing this you get TypeScript Intellisense and compile-time errors when the client- and server side code differs. This speeds up your development pace and increases the quality of your applications.


## TypeScript and React
Sources:
- [Dedicated TypeScript section in the React docs](https://reactjs.org/docs/static-type-checking.html#typescript).
- [React + TypeScript Pluralsight course](https://app.pluralsight.com/library/courses/react-apps-typescript-building/table-of-contents)

### Configuring TypeScript

#### For a new app
Most of the [common React toolchains](https://reactjs.org/docs/create-a-new-react-app.html#recommended-toolchains) offer options for creating a TypeScript React app. If using `create-react-app`:
```
npx create-react-app my-app-name --template typescript
```
- `tsconfig.json` at the root of the project provides configuration for how TS can be used in our project, and which files to include in typechecking
- common types are imported as dependencies in `package.json`:
  ```json
  "@types/jest": "^26.0.22",
  "@types/node": "^12.20.9",
  "@types/react": "^17.0.3",
  "@types/react-dom": "^17.0.3",
  ```
- project scaffolding files will have `.tsx` file extension, e.g. `index.tsx` and `App.tsx`

#### In an existing app
A common scenario is to update an existing React app to use TypeScript, allowing incremental adoption.

1. Add appropriate types to your project:
   ```
   npm add typescript @types/react @types/react-dom @types/node
   ```
   - depending on your project, you may need to add further types, e.g. `@types/react-router-dom` etc.
1. Update a file to have a `.tsx` file extension
1. Run `npm start` - this will cause `react-scripts` to detect that a TS file has been added to the project, and a `tsconfig.js` file with default values will be generated!
1. Files will be recognised for typechecking by the `.tsx` file ending

### Declaring components and props

#### Functions
- TypeScript will require us to provide types for our function arguments (implicitely typed arguments will show an error). The type is specified with a colon after the argument name, e.g.:
  ```js
  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
        ...
    }
  ```
- This consequently adds autocomplete help when accessing properties of the argument

#### Props
- Here too we need to describe the type we want to work with; usually this is done by creating our own interface declarations:
  ```js
  interface Props {
      children: React.ReactNode; // declare that there is a prop 'children' of type ReactNode
  }
  ```
- This interface can then be used in the constructor (if using class components)
  ```js
  class MyComponent extends React.Component {
      constructor(props: Props) {
          super(props);
          ...
      }
      ...
  }
  ```

#### State
- The interface for our state is declared in a similar vain as for Props:
  ```js
  interface State {
      isLoading: boolean;
  }
  ```
- Using generics, we can then specify both of these types `<Props, State>` to be used by our component:

  ```js
  class MyComponent extends React.Component<Props, State> {
    constructor(props: Props) {
        super(props);
        this.state = { isLoading: true };
    }

  ```



### Using Hooks with TypeScript



