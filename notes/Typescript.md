# Typescript notes
Typescript is a syntactical superset of ECMAScript developed by Microsoft, which adds optional static typing to the language. It cannot natively run in JS environments such as the browser, so needs to be transcompiled to JavaScript before running.

Notes based on: [TypeScript for Beginners 2020](https://www.youtube.com/watch?v=BwuLxPH8IDs) (continue at 6:32)

### Why TypeScript?
- less error prone due to static typing (reducing need for manual validation / sanitisation)
- additional features that don't exist in JS
- not just a programming language, but also a powerful compiler that runs over your code and compiles it to JavaScript and provides compile-time errors, making it easier to catch errors earlier on in development

> :bulb: TS features are compiled to JS 'workarounds'



## Typewriter
[Typewriter](https://frhagn.github.io/Typewriter/) is a free extension for Visual Studio that generates TypeScript files from C# code files using TypeScript Templates.

This allows you to create fully typed TypeScript representations of server side API, models, controllers etc. that automatically updates when you make changes to your C# code.

By doing this you get TypeScript Intellisense and compile-time errors when the client- and server side code differs. This speeds up your development pace and increases the quality of your applications.
