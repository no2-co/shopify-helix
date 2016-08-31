# shopify-starterkit

Shopify-starterkit aims to cut down on the tedious aspects of developing a Shopify website.

Don't like having one huge assets folder? Need to compile your modular Sass and ES6 JavaScript into `.liquid` files? Want to upload your files on save?

Shopify-starterkit helps you maintain a more modular and scalable codebase while keeping Shopify's CDN happy by compiling everything to the theme's asset directory.

## Getting Started

### Prerequisites

- A live [Shopify](https://www.shopify.com/) website
- [Node.js](https://nodejs.org/en/) - v4.4.7+
- [gulp-cli](https://github.com/gulpjs/gulp-cli) - Allows you to run Gulp tasks using the command line
    - `npm install --global gulp-cli`

### Setup

1. Create project directory
    - `mkdir shopify-site`
2. Navigate to new directory
    - `cd shopify-site`
3. Clone this repo
    - `git clone git@github.com:skycatchfire/shopify-starterkit.git .`
4. Install NPM dependencies
    - `npm install`
5. Navigate to your `./gulp` directory and create a `vault.json` file
    - `touch vault.json`

## Configuration

Gulp tasks can be configured in `./gulp/config.json`.

Information you do not want to commit to the repo can be stored in `./gulp/vault.json`.

### gulp/config.json

The `config.json` configuration file holds all of the different configuration options for your Gulp tasks.

**Note:** Your Shopify URL is **required** in `config.json` and must not contain http or https.

```json
{
  "shopify": {
      "url": "someshopifysite.myshopify.com",
      "basePath": "./theme"
  },
}
```

### gulp/vault.json

The `vault.json` configuration file holds your Shopify API key and API password as well as any other sensitive information you do not want to commit to your repository.

**Note:** The `shopify_api_key` and `shopify_api_password` are **required** in `vault.json`.

```json
{
  "shopify_api_key": "XXXXXXXXXXXXXXXXXXX",
  "shopify_api_password": "XXXXXXXXXXXXXXXXXXX"
}
```

## Gulp Tasks

### Default Task

- `gulp` - Runs the default Gulp tasks. Tasks that are run are below:
  - `skeleton`
  - `shopify:watch`
  - `watch`

### Shopify tasks

- `gulp shopify:watch`
  - Watches for changes in the `./theme` directory. When it detects a change, your updated files will automatically be uploaded to your live Shopify website.


-  TODO: `gulp shopify:init`
  - Uploads all files found in the `./theme` directory to your live Shopify website.

### Development Tasks

- `gulp scss`
  - Compiless SCSS to CSS
  - Autoprefixes elements for older browser
  - Minifies CSS if `minify: true` in `config.json`
  - Outputs a `main.css.liquid` file to `./theme/assets`

- `gulp scripts`
  - Concatonates all files in the `./assets/scripts` directory
  - Compiles ES6 to ES5 if `ecmascript: 6` in `config.json`
  - Minifies JavaScript if `minify: true` in `config.json`
  - Outputs a `main.js.liquid` file to `./theme/assets`

- `gulp images`
  - Flattens all image folders in the `./assets/images` directory
  - Optimizes images if `minify: true` in `config.json`
  - Outputs image files to `./theme/assets`

- `gulp fonts`
  - Flattens all font folders in the `./assets/fonts` directory
  - Outputs font files to `./theme/assets`

### Other Tasks

- `gulp skeleton`
  - Moves the default theme assets to the `./theme/assets` directory
  - This task allows you to add the `./theme/assets` directory to your .gitignore file while still maintaining all of the default theme assets

- `gulp watch`
  - Watches for file changes and runs the development tasks

## Shopify Theme

The Shopify theme lives in the `./theme` directory.

This starterkit comes with Shopify's [Skeleton theme](https://github.com/Shopify/skeleton-theme). You can customize Shopify's Skeleton theme or create your own custom theme!

### Customizing your Shopify Theme

All changes to front-end styling, scripts, images, etc., can be done in the root level `./assets` directory. You should never have to edit anything in your `./theme/assets` directory.

Everything from the root level `./assets` directory will be compiled with Gulp, flattened, and placed in `./theme/assets`.

This is because Shopify's CDN does not allow for sub directories in the `./theme/assets` directory.