# How Do I Use stylesheets with SAFE?
If you wish to use your own CSS or SASS stylesheets with SAFE apps, you can embed either through webpack. The template already includes all required NPM packages you may need, so you will only need to configure webpack to reference your stylesheet and include in the outputs.

## Adding the Stylesheet
First, create a CSS file in the `src/Client` folder of your solution e.g `styles.css`.

> The same approach can be taken for `.scss` files.

# Import the styles

Locate `App.fs` in the Client project. 

Open Fable's JS Interop module and import the file you just created.

```fsharp
open Fable.Core.JsInterop

importSideEffects "./styles.scss"
```

That's it! 


### I'm using the Minimal Template

In this case do the same as above but in `Client.fs` instead of `App.fs`.


## There you have it!
You can now style your app by writing to the `style.css` file.