# TypeScript notes
**Contents: [Intro](#intro) | [Typewriter](#typewriter) | [TypeScript and React](#typescript-and-react)**

Typescript is a syntactical superset of ECMAScript developed by Microsoft, which adds optional static typing to the language. It cannot natively run in JS environments such as the browser, so needs to be transcompiled to JavaScript before running.


## Intro
### Why TypeScript?
- less error prone due to static typing (reducing need for manual validation / sanitisation)
- additional features that don't exist in JS
- not just a programming language, but also a powerful compiler that runs over your code and compiles it to JavaScript and provides compile-time errors, making it easier to catch errors earlier on in development
- adds autocomplete help, e.g. when accessing properties of a typed entity

> :bulb: TS features are compiled to JS 'workarounds'


## Typewriter
[Typewriter](https://frhagn.github.io/Typewriter/) is a free extension for Visual Studio that generates TypeScript files from C# code files using TypeScript Templates.

This allows you to create fully typed TypeScript representations of server side API, models, controllers etc. that automatically updates when you make changes to your C# code.

By doing this you get TypeScript Intellisense and compile-time errors when the client- and server side code differs. This speeds up your development pace and increases the quality of your applications.


## TypeScript and React
Sources: [Dedicated TypeScript section in the React docs](https://reactjs.org/docs/static-type-checking.html#typescript) | [React + TypeScript Pluralsight course](https://app.pluralsight.com/library/courses/react-apps-typescript-building/table-of-contents)

**Jump to:**
- [Configuring TypeScript](#configuring-typescript)
- [Typed function arguments + variables](#typed-function-arguments--variables)
- [Type declarations in class components](#type-declarations-in-class-components)
- [Declaring props in function components](#declaring-props-in-function-components)
- [Using Hooks with TypeScript](#using-hooks-with-typescript)

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


### Typed function arguments + variables
- TypeScript will require us to provide types for our function arguments (implicitely typed arguments will show an error). The type is specified with a colon after the argument name, e.g.:
  ```js
  componentDidCatch(error: Error, errorInfo: React.ErrorInfo) {
    ...
  }
  ```
- We can optionally declare types for local variables too, although not doing so won't yield an error:
  ```js
  const hasCats: boolean = true;
  ```


### Type declarations in class components
- We need to describe the types we want to work with for our props and state; this is commonly done by creating our own interface declarations:
  ```js
  interface Props {
    children: React.ReactNode;  // declare a prop 'children' of type ReactNode
    label: string;  // declare prop 'label' of type string
  }
  
  interface State {
    isLoading: boolean;  // declare a state variable 'isLoading' of type boolean
  }
  ```
- We can then use generics syntax to specify both of these types `<Props, State>` to be used by our component. `Props` also needs to be specified in the constructor:
  ```js
  class MyComponent extends React.Component<Props, State> {
    constructor(props: Props) {
      super(props);
      this.state = { isLoading: true };
    }
    ...
  }
  ```

### Declaring props in function components
- Declaring the contract of our props via types/interfaces has similar benefits to using [PropTypes](/notes/React-Notes.md#2-validate-props-with-proptypes), but with the added advantage that the validation happens at compile time rather than run time
- We declare the interface for our props:
  ```js
  interface Props {
    children: React.ReactNode;
    label: string;
  }
  ```
- And then use this in the declaration of the function component:
  ```js
  function MyComponent(props: Props) {
    ...
  }
  ```

#### Alternative syntax
- 💡 If preferred, we can also use **inline type definitions**, rather than declaring a named interface:
  ```js
  function MyComponent(props: { children: React.ReactNode; label: string }) {
    ...
  }
  ```
- Type definitions can also be used alongside **props destructuring**:
  ```js
  interface Props {
    children: React.ReactNode;
    label: string;
  }
  
  function MyComponent({ children, label }: Props) {
    ...
  }
  ```

### Using Hooks with TypeScript
**Type declarations and [`useState()`](/notes/React-Hooks.md#usestate)**
- If a given state variable needs to hold a complex type with specific options, this can be declared as follows:
  ```js
  interface AuthInfo {
    userData: UserData | null  // AuthInfo contains a nullable 'userData' property, which must match the 'UserData' interface below
  }

  interface UserData {
      role: "ADMIN" | "USER"  // if UserData is defined (i.e. not null) its role property must be of value 'ADMIN' or 'USER'
  }
  ```
- 👉 NB: when using the pipe operator to declare possible concrete values, the type declaration (e.g. `string` for the `role` example above) is implicit
- We can then pass the complex type to the `useState()` hook via generic type arguments (in this case `<AuthInfo>`):
  ```js
  const [authInfo, setAuthInfo] = React.useState<AuthInfo>({
    userData: null,
  });
  ```

**Type declarations when using [Context](/notes/React-Hooks.md#usecontext)**
- In the **Provider**, define your context values via an interface, which can then be passed to `createContext`:
  ```js
  interface AuthContextValues {
    authInfo: AuthInfo;
    isAuthenticated: boolean;
    setAuthInfo: React.Dispatch<React.SetStateAction<AuthInfo>>;  // definition of the setState function provided by React
    isAdmin: boolean;
  }

  // declare AuthContext to either be undefined, or of type AuthContextValues, and set a default context of undefined
  export const AuthContext = React.createContext<AuthContextValues | undefined>(undefined);
  const Provider = AuthContext.Provider;
  ```
- this needs to match what we provide as values to the `Provider` wrapper:
  ```js
  export function AuthProvider({ children }: Props) {
    ...
    return (
      <Provider value={{ authInfo, isAuthenticated, setAuthInfo, isAdmin }}>
        {children}
      </Provider>
    );
  }
  ```
- an **alternative** to using the lengthy `setState` function definition provided by React is to wrap the function returned by the `useState()` hook (`setAuthInfo` in this example) in our own local function, and use this wrapper in the `Provider` values:
  ```js
  export function AuthProvider({ children }: Props) {
    ...
    function handleAuthInfo(authInfo: AuthInfo) {
      setAuthInfo(authInfo);
    };
    
    return (
      <Provider value={{ authInfo, isAuthenticated, setAuthInfo: handleAuthInfo, isAdmin }}>
        {children}
      </Provider>
    );
  }
  ```
- then we can update the interface to a function definition that takes `AuthInfo` and returns void:
  ```js
  interface AuthContextValues {
    authInfo: AuthInfo;
    isAuthenticated: boolean;
    setAuthInfo: (authInfo: AuthInfo) => void;  // nicer
    isAdmin: boolean;
  }
  ```


👉 See [full file](https://github.com/mwarger/globomantics-react-ts/blob/m4-declaring-and-using-hooks-with-typescript-final/app/src/context/AuthProvider.tsx) which these snippets are from, for more context.








