# Gatsby Plugin Lingui Example

## Setup

1. `npm i @lingui/babel-preset-react @lingui/react @wapps/gatsby-plugin-lingui`

2. `npm i -D @lingui/cli`

3. Add to `gatsby-config.js`

   ```json
   {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/locale`,
        name: `locale`,
      },
    },
    {
      resolve: "@wapps/gatsby-plugin-lingui",
      options: {
        availableLngs: ["en", "de"],
        fallbackLng: "en",
      },
    },
   ```

4. Add `lingui.config.js` to root

   ```js
   module.exports = {
     fallbackLocale: "en",
     sourceLocale: "en",
     localeDir: "<rootDir>/locale",
     srcPathDirs: ["<rootDir>/src/components", "<rootDir>/src/pages"],
     srcPathIgnorePatterns: ["/node_modules/"],
     format: "minimal",
   }
   ```

5. Add `.babelrc` to root

   ```json
   {
     "presets": ["babel-preset-gatsby", "@lingui/babel-preset-react"]
   }
   ```

6. Add tranlations to pages and components with `<Trans>Text to translate</Trans>`

7. Add the locales query to your gatsby pages

   ```js
   export const query = graphql`
     query($lng: String!, $fallbackLng: String!) {
       locales: allLocale(
         filter: { lng: { in: [$lng, $fallbackLng] }, ns: { eq: "messages" } }
       ) {
         ...LocaleFragment
       }
     }
   `
   ```

8. Wrap you components:

   ```js
   export default withLingui()(IndexPage)
   ```

9. `npm run add-locale en de fr` to add lanuages

10. `npm run extract` to get the messages files

11. Translate the messages files

12. `npm start`

13. Profit
