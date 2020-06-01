# react-ridge-state :weight_lifting_woman: ⚡️ :weight_lifting_man:

**Simple** :muscle: **fast** ⚡️ and **small** :balloon: (0.7kb) global state management for React which can be used outside of a React component too!

```
yarn add react-ridge-state
```

or

```
npm install react-ridge-state --save
```

## Why another state library :thinking:

We were frustrated that the current solutions could often only be used from React or have too complicated APIs. We wanted a lightweight solution with a smart API that can also be used outside React components.

## Features :woman_juggling:

- React / React Native
- Simple
- Fast
- Very tiny
- 100% Typesafe
- Hooks
- Use outside React components

## Roadmap :running_woman: :running_man:

- Custom selectors for deep state selecting

## Getting started :clap: :ok_hand:

### Create a new state

```typescript
import { newRidgeState } from "react-ridge-state";
interface CartProduct {
  id: number;
  name: string;
}
export const cartProductsState = newRidgeState<CartProduct[]>([
  { id: 1, name: "Product" },
]);
```

### Use state inside components

```typescript
import { cartProductsState } from "../cartProductsStatee";

const [cartProducts, setCartProducts] = cartProductsState.use();
```

### Use state outside of React

```typescript
import { cartProductsState } from "../cartProductsStatee";
cartProductsState.get();
```

### Set state outside of React

```typescript
import { cartProductsState } from "../cartProductsStatee";
cartProductsState.set([{ id: 1, name: "NiceProduct" }]);

// if you want previous state
cartProductsState.set((prevState) => [
  ...prevState,
  { id: 1, name: "NiceProduct" },
]);

// if you want want to be sure state is rendered everywhere
cartProductsState.set(
  (prevState) => [...prevState, { id: 1, name: "NiceProduct" }],
  (newState) => {
    console.log("New state is rendered everywhere");
  }
);
```

### Persistency

It's possible to add persistency to your state. (add try/catch if you use localStorage in real app)

```typescript
const authStorageKey = "auth";
const authState = newRidgeState<AuthState>(
  getInitialState() || emptyAuthState,
  { onSet }
);

// getInitialState fetches data from localStorage
function getInitialState() {
  let initialState = undefined;
  const item = localStorage.getItem(authStorageKey);
  if (item) {
    initialState = JSON.parse(item);
  }
}

// onSet is called after state has been set
function onSet() {
  // save to local storage
  localStorage.setItem(authStorageKey, JSON.stringify(newState));
}
```

## About us

We want developers to be able to build software faster using modern tools like GraphQL, Golang, React Native without depending on commercial providers like Firebase or AWS Amplify.

Checkout our other products too! :ok_hand: https://github.com/web-ridge
