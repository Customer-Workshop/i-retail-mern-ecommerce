# MERN Ecommerce

## Description

An ecommerce store built with MERN stack, and utilizes third party API's. This ecommerce store enable three main different flows or implementations:

1. Buyers browse the store categories, products and brands
2. Sellers or Merchants manage their own brand component
3. Admins manage and control the entire store components 

### Features:

  * Node provides the backend environment for this application
  * Express middleware is used to handle requests, routes
  * Mongoose schemas to model the application data
  * React for displaying UI components
  * Redux to manage application's state
  * Redux Thunk middleware to handle asynchronous redux actions

## Demo

This application is deployed on Vercel Please check it out :smile: [here](https://mern-store-gold.vercel.app).

See admin dashboard [demo](https://mernstore-bucket.s3.us-east-2.amazonaws.com/admin.mp4)

## Docker Guide

To run this project locally you can use docker compose provided in the repository. Here is a guide on how to run this project locally using docker compose.

Clone the repository
```
git clone https://github.com/mohamedsamara/mern-ecommerce.git
```

Edit the dockercompose.yml file and update the the values for MONGO_URI and JWT_SECRET

Then simply start the docker compose:

```
docker-compose build
docker-compose up
```

## Database Seed

* The seed command will create an admin user in the database
* The email and password are passed with the command as arguments
* Like below command, replace brackets with email and password. 
* For more information, see code [here](server/utils/seed.js)

```
npm run seed:db [email-***@****.com] [password-******] // This is just an example.
```

## Install

`npm install` in the project root will install dependencies in both `client` and `server`. [See package.json](package.json)

Some basic Git commands are:

```
git clone https://github.com/mohamedsamara/mern-ecommerce.git
cd project
npm install
```

## ENV

Create `.env` file for both client and server. See examples:

[Frontend ENV](client/.env.example)

[Backend ENV](server/.env.example)


## Vercel Deployment

Both frontend and backend are deployed on Vercel from the same repository. When deploying on Vercel, make sure to specifiy the root directory as `client` and `server` when importing the repository. See [client vercel.json](client/vercel.json) and [server vercel.json](server/vercel.json).

## Start development

```
npm run dev
```

## Bug Fixes (buggy branch)

The `buggy` branch contained 8 planted bugs across the React/Redux frontend and Express/MongoDB backend. All have been identified and fixed:

| # | File | Line | Root Cause | Fix |
|---|------|------|-----------|-----|
| 1 | `server/routes/api/auth.js` | 48 | Inverted password check — correct passwords rejected, wrong ones accepted | `if (isMatch)` → `if (!isMatch)` |
| 2 | `server/routes/api/product.js` | 60 | Product search returns only deactivated products | `isActive: false` → `isActive: true` |
| 3 | `server/routes/api/cart.js` | 90 | Inventory increases instead of decreasing when items are added to cart | `$inc: { quantity: item.quantity }` → `quantity: -item.quantity` |
| 4 | `server/routes/api/wishlist.js` | 56 | Wishlist query missing user filter — returns all users' items | Added `user` to `Wishlist.find()` query |
| 5 | `server/utils/store.js` | 98 | Tax calculation missing `* 100` multiplier in `caculateItemsSalesTax` | Restored `* 100` to match `caculateTaxAmount` |
| 6 | `client/app/containers/Cart/actions.js` | 99 | Cart total computed as `price + quantity` instead of `price * quantity` | `+` → `*` |
| 7 | `client/app/containers/Cart/reducer.js` | 42 | Removing a cart item also removes the next item | `slice(itemIndex + 2)` → `slice(itemIndex + 1)` |
| 8 | `client/app/containers/Order/actions.js` | 207 | Order total hardcoded to `0` — every order submitted as $0 | `total: 0` → `total` |

## Languages & tools

- [Node](https://nodejs.org/en/)

- [Express](https://expressjs.com/)

- [Mongoose](https://mongoosejs.com/)

- [React](https://reactjs.org/)

- [Webpack](https://webpack.js.org/)


### Code Formatter

- Add a `.vscode` directory
- Create a file `settings.json` inside `.vscode`
- Install Prettier - Code formatter in VSCode
- Add the following snippet:  

```json

    {
      "editor.formatOnSave": true,
      "prettier.singleQuote": true,
      "prettier.arrowParens": "avoid",
      "prettier.jsxSingleQuote": true,
      "prettier.trailingComma": "none",
      "javascript.preferences.quoteStyle": "single",
    }

```

