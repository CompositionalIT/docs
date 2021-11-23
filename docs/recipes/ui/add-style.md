# How Do I Use stylesheets with SAFE?
If you wish to use your own CSS or SASS stylesheets with SAFE apps, you can embed either through webpack. The full template already includes all required NPM packages you may need, and just requires a simple import. The minimal template will need a few things installed and a couple of tweaks to the webpack file in order to get things working.

## Adding the Stylesheet
First, create a Sass file in the `src/Client` folder of your solution e.g `styles.scss`.

> The same approach can be taken for normal `.css` files.

# Import the styles

Locate `App.fs` in the Client project. 

Open Fable's JS Interop module and import the file you just created.

```fsharp
open Fable.Core.JsInterop

importSideEffects "./styles.scss"
```

That's it! 


### I'm using the Minimal Template

- Begin the same as above but place the open / import in `Client.fs` instead of `App.fs`.

- Add these npm packages to your `package.json` file, either directly or with `npm install`:

    - mini-css-extract-plugin
    - sass
    - sass-loader
    - style-loader
    - css-loader

- Open your `webpack.config.js` and add the following import next to the existing ones for `HtmlWebpackPlugin` and `CopyWebpackPlugin`:

`var MiniCssExtractPlugin = require('mini-css-extract-plugin')`

- Create an instance of this plugin underneath the htmlPlugin and copyPlugin variables like so:

`var cssPlugin = new MiniCssExtractPlugin({ filename: 'style.[name].[hash].css' })`

- Finally, add a new `module` section to your `module.exports` object:

```js
module.exports = {
    //... other stuff
    module: {
        rules: [
            {
                test: /\.(sass|scss|css)$/,
                use: [
                    isProduction
                        ? MiniCssExtractPlugin.loader
                        : 'style-loader',
                    'css-loader',
                    {
                        loader: 'sass-loader',
                        options: { implementation: require('sass') }
                    }
                ]
            }
        ]
    }
};
```


## There you have it!
You can now style your app by writing to the `style.scss` file.