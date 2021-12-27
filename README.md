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
