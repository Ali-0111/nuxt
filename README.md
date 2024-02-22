nuxt.config.ts

```
import { defineNuxtConfig } from 'nuxt/config';
import HtmlWebpackPlugin from 'html-webpack-plugin';
import HtmlWebpackInlineSourcePlugin from 'html-webpack-inline-source-plugin';

export default defineNuxtConfig({
  // devtools: { enabled: true },
  // debug: true,
  css: ['~/assets/scss/tailwind.scss'],
  builder: 'webpack',
  webpack: {
    plugins: [
      new HtmlWebpackPlugin({
        filename: 'output.html', // output file name that will be created
        template: 'output-template.html', // template file to use for insertion
        inlineSource: '.(js|css)$', // embed all javascript and css inline
        inject: 'body' // inject script at the end of document body
      })
      // new HtmlWebpackInlineSourcePlugin()
    ]
  },
  hooks: {
    // may be needed for successful bundling
    'webpack:config'(configs) {
      configs[0].module.rules.push(
        {
          test: /\.vue$/,
          loader: 'vue-loader'
        },
        {
          test: /\.html$/,
          loader: 'html-loader'
        },
        {
          test: /\.tsx?$/,
          use: 'ts-loader',
          exclude: /node_modules/
        },
        {
          test: /\.css$/,
          use: ['style-loader', 'css-loader']
        },
        {
          test: /\.(png|jpg|gif|webp|svg)$/,
          loader: 'url-loader'
        },
        {
          test: /\.s[ac]ss$/i,
          use: [
            // Creates `style` nodes from JS strings
            'style-loader',
            // Translates CSS into CommonJS
            'css-loader',
            // Compiles Sass to CSS
            'sass-loader'
          ]
        }
      );
    }
  },
  app: {
    head: {
      charset: 'utf-8',
      htmlAttrs: {
        lang: 'en'
      },
      viewport: 'width=device-width, initial-scale=1',
      link: [{ rel: 'icon', type: 'image/x-icon', href: '/favicon.png' }]
    }
  },
  modules: [
    '@nuxtjs/color-mode',
    '@nuxt/image',
    'nuxt-icon',
    '@nuxtjs/tailwindcss',
    '@nuxtjs/eslint-module',
    '@nuxtjs/stylelint-module',
    'nuxt-swiper'
  ],
  colorMode: {
    classSuffix: '',
    preference: 'system', // default value of $colorMode.preference
    fallback: 'light', // fallback value if not system preference found
    hid: 'nuxt-color-mode-script', // unique identifier for the color-mode script tag.
    globalName: '__NUXT_COLOR_MODE__',
    componentName: 'ColorScheme',
    classPrefix: '',
    storageKey: 'app-color-mode'
  },

```

package.json

```
{
  "name": "boo",
  "private": true,
  "type": "module",
  "scripts": {
    "build": "nuxt build",
    "dev": "nuxt dev",
    "generate": "nuxt generate",
    "preview": "nuxt preview",
    "postinstall": "nuxt prepare",
    "lint:style": "npx stylelint '**/*.{css,scss}'",
    "lint:js": "eslint --ext \".ts,.vue\" --ignore-path .gitignore .",
    "lint:prettier": "prettier --check .",
    "lint": "yarn lint:js && yarn lint:prettier",
    "lintfix": "prettier --write --list-different . && yarn lint:js --fix && yarn lint:style --fix"
  },
  "devDependencies": {
    "@babel/eslint-parser": "^7.23.3",
    "@nuxt/image": "^1.0.0-rc.3",
    "@nuxtjs/color-mode": "^3.3.2",
    "@nuxtjs/eslint-module": "^4.1.0",
    "@nuxtjs/stylelint-module": "^5.1.0",
    "@nuxtjs/tailwindcss": "^6.10.4",
    "eslint": "^8.56.0",
    "eslint-config-prettier": "^9.1.0",
    "eslint-plugin-nuxt": "^4.0.0",
    "eslint-plugin-prettier": "^5.1.3",
    "eslint-plugin-vue": "^9.20.1",
    "html-loader": "^5.0.0",
    "html-webpack-inline-source-plugin": "^1.0.0-beta.2",
    "html-webpack-plugin": "^5.6.0",
    "json-joy": "9.8.0",
    "nuxt": "^3.9.1",
    "nuxt-icon": "^0.6.8",
    "nuxt-swiper": "^1.2.2",
    "postcss-custom-properties": "^13.3.5",
    "prettier": "^3.2.2",
    "sass": "^1.71.1",
    "sass-loader": "^14.1.1",
    "style-loader": "^3.3.4",
    "stylelint": "13.x",
    "stylelint-config-standard": "21.x",
    "stylelint-csstree-validator": "1.x",
    "stylelint-scss": "3.x",
    "ts-loader": "^9.5.1",
    "url-loader": "^4.1.1",
    "vue": "^3.4.10",
    "vue-eslint-parser": "^9.4.0",
    "vue-loader": "^17.4.2",
    "vue-router": "^4.2.5"
  },
  "dependencies": {
    "@nuxt/webpack-builder": "^3.10.2",
    "axios": "^1.6.7",
    "vue-dompurify-html": "^5.0.1"
  }
}
```

