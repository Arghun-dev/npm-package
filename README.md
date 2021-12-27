# npm-package

imagine you wanna create a package through a react component, in this case, I install `react` and `react-dom` as `dev-dependencies` in my-project, now any library that uses this component, needs to have react and react-dom installed, and if I put them as `dev-dependencies`, it's not going to automatically install it for them, that's good we don't want that, It would do that if we list it as `normal dependencies`, so if I had react and react-dom as normal dependencies, any project installed my component library, whichever version of react and react-dom I have listed here, will be installed automatially for them, and I don't wanna do that because there could be colliions and versions, and you never wanna have multiple versions of react in the same project, **However, we do wanna make sure, that they have `react` and `react-dom` installed, because, this is a react component library** => **to do that we use `peerDependencies`**

```js
"peerDependencies": {
  "react",
  "react-dom"
}
```

And I need a way to see the component as I'm developing, as I'm writing the code, I always wanna make sure that I see what it is I'm building, as I'm building it, so I can test it out and make sure that it's working, one way to do that is to create a new react application that simply installs this locally on my machine, so you have a react application, that you create with something like `create-react-app` and then you install this library (the libary you are building) locally on the machine, however I would have to constantly rebuild the app every single time I wanted an update and then I'd have to reinstall on the application that's ingesting this component library and it can be extremely tedious to do that, and I don't wanna to do that. Instead I want to use a tool that makes it as easy as possible for me to develop a component library, and for that I'm going to use `storybook`.

To do that first you have to install `storybook`.

`$. npx sb init`

If you read about `storybook`, it says that:

**Storybook is an open source tool for developing UI components in isolation for React, Vue, Angular, and more. It makes building stunning UIs organized and efficient.**

If you run the command `$. npx sb init`

Since, we've set up our project structure and have react and react-dom, listed as dev dependencies, when I run this command, it should detect that we're inside of a react project, and it should all work automatically, so I'm going to go to my terminal or my command line interface and I'm going to paste `$. npx sb init`.

and to run the storybook you should write => `$. npm run storybook`

**Tip: in a normal react application, the `index.js` file typically ends up being the file that compiles the entire react application and then injects it into your `index.html`, however, when you're building a react component library, there is no `index.html` file, and so you're not going to be injecting any type of application into any html files, so the job of `index.js` file inside of a react component library is very different that in a react application, for our case here what it's going to do is export all of the components that I want any application that may be use this library to be able to import, now in my case for the library that I'm building, I only want them to be able to import one component and that's the Requirement component** 

and after you made all of these, and you can see you files stories inside storybook.

Now the question is how can I build this to a dist folder, that I can then publish to `npm` => use `rollup`

**rollup: ** `Rollup is a moduule bundler for JavaScript which compiles small pieces of code into something larger and more complex, such as a library or application`

to install rollup: `$. npm i -D rollup rollup-plugin-babel @rollup/plugin-node-resolve rollup-plugin-peer-deps-external`

as you can see here, we have `rollup-plugin-peer-deps-external` => this just ensures that we exclude any peer dependencies from our bundle, we have react and react-dom as peer dependencies we want to make sure that we do not add the react and react-dom source code to our bundle, so that babel plugin that I was talking about is `babel-preset-react`.

so `$. npm i -D @babel/preset-react`

now to config rollup create a new file called `rollup.config.js` in the root of the project.

rollup.config.js

```js
import babel from 'rollup-plugin-babel';
import resolve from '@rollup/plugin-node-resolve';
import external from 'rollup-plugin-peer-deps-external';

export default [
  {
    input: './src/index.js',
    output: [
      {
        file: 'dist/index.js',
        format: 'cjs'
      },
      {
        file: 'dist/index.es.js',
        format: 'es',
        exports: 'named'
      }
    ],
    plugins: [
      babel({
        exclude: 'node_modules/**',
        presets: ['@babel/preset-react']
      }),
      external(),
      resolve()
    ]
  }
]
```
