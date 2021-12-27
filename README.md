# npm-package

imagine you wanna create a package through a react component, in this case, I install `react` and `react-dom` as `dev-dependencies` in my-project, now any library that uses this component, needs to have react and react-dom installed, and if I put them as `dev-dependencies`, it's not going to automatically install it for them, that's good we don't want that, It would do that if we list it as `normal dependencies`, so if I had react and react-dom as normal dependencies, any project installed my component library, whichever version of react and react-dom I have listed here, will be installed automatially for them, and I don't wanna do that because there could be colliions and versions, and you never wanna have multiple versions of react in the same project, **However, we do wanna make sure, that they have `react` and `react-dom` installed** => **to do that we use `peerDependencies`**

```js
"peerDependencies": {
  "react",
  "react-dom"
}
```
