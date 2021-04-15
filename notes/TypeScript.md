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

- add appropriate types to your project

### Declaring components and props


### Using Hooks with TypeScript



