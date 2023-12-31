# @cmckenna/use-async-modal

Show promised based modal imperatively using hook for React.js.

![npm](https://img.shields.io/npm/v/use-async-modal?style=flat-square) ![NPM](https://img.shields.io/npm/l/use-async-modal?style=flat-square) [![Test](https://github.com/cmcken22/use-async-modal/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/cmcken22/use-async-modal/actions/workflows/test.yml) ![Libraries.io dependency status for GitHub repo](https://img.shields.io/librariesio/github/cmcken22/use-async-modal?style=flat-square) ![npm bundle size](https://img.shields.io/bundlephobia/min/use-async-modal?style=flat-square) ![npm peer dependency version](https://img.shields.io/npm/dependency-version/use-async-modal/peer/react?style=flat-square)


# About
## This is basically the same repo as [Harasz/use-async-modal](https://github.com/Harasz/use-async-modal/blob/main/README.md) except now you can pass props to the modal upon opening! :sunglasses:

&nbsp;
&nbsp;

# Table of Contents

1. [Installation](#installation)
2. [Usage](#usage)
3. [Demos](#demos)
4. [Contributing](#contributing)
5. [License](#license)

## Installation

You can install package using [npm](https://www.npmjs.com/package/use-async-modal) or [yarn](https://yarnpkg.com/):

```bash
npm i @cmckenna/use-async-modal

yarn add @cmckenna/use-async-modal
```

## Usage

First, we will need a component modal to show:

```JSX
export const Dialog = ({ onResolve, title, acceptBtnText, cancelBtnText }) => {
  return (
    <div>
      <button onClick={() => onResolve({ accepted: true })}>{acceptBtnText ?? 'Accept'}</button>
      <button onClick={() => onResolve({ accepted: false })}>{cancelBtnText ?? 'Cancel'}</button>
    </div>
  );
};
```

Then in the component we want to open a modal, we need to use `useModal` hook from `use-async-modal` package. It is necessary to add only once the `ModalContainer` component from `use-async-modal` package as high as possible in your app.

```JSX
import { useModal, ModalContainer } from "use-async-modal";
import { Dialog } from "./Dialog";

export const App = () => {
    const showModal = useModal({
    Component: Dialog,

    /*
        Type: Function
        Desc: It will be invoked when the window is closed.
        Options:
          - resolved: value passed to onResolve.
    */
    onClose: ({ resolved }) => {},

    /*
        Type: Function
        Desc: It will be invoked when the window is opened.
        Options:
          - containerId: string containing attribute id for overlay in DOM,
          - containerRef: HTMLDivElement ref to overlay.
    */
    onOpen: ({ containerId, containerRef }) => {},

    /*
        Type: Object
        Desc: Inline styles applied to overlay.
    */
    overlayStyles: {
      backgroundColor: "red",
      margin: "1px"
    },

    /*
        Type: String
        Desc: Classes to be applied to overlay.
        Accept multiple classes names separated
        by space ex. "px-1 mx-2 bg-green".
    */
    overlayClassName: "px-1",

    /*
        Type: Bool
        Desc: If set to true, dialog will close
        after escape key down.
        Default value: false
    */
    closeOnEsc: true,

    /*
        Type: Bool
        Desc: If set to true, the dialog will
        close when the overlay was clicked.
        Default value: false
    */
    closeOnOverlayClick: true,

    /*
        Type: same as onResolve
        Desc: The value passed to the onResolve
        function when the dialog was closed with
        the Escape key or an overlay click.
    */
    defaultResolved: { accepted: false },

    /*
        Type: String
        Desc: Classes to be applied to overlay
        after closing. Accept multiple classes
        names separated by space.
    */
    overlayClassNameOnClose: "fade-out",

    /*
        Type: same as onResolve
        Desc: Classes to be applied to overlay
        when open. Accept multiple classes names
        separated by space.
    */
    overlayClassNameOnOpen: "fade-in",

    /*
        Type: Number (unit: ms)
        Desc: Delayed closing time expressed
        in milliseconds.
    */
    closeTimeoutMs: 1000,

    /*
        Type: Bool (default: true)
        Desc: Locking the scrollbar on the page
        when the model is open.
    */
    blockBodyScroll: true,
  });

  async function handleClick() {
    const status = await showModal({ 
      title: 'Hello World',
      acceptBtnText: 'Ok',
      cancelBtnText: 'Deny'
    });
    // { accepted: true } or { accepted: false }
  }

  /*
        necessary to add <ModalContainer /> once at the top of app
  */
  return (
    <>
      <ModalContainer />
      <button onClick={handleClick}>Open dialog</button>
    </>
  );
};

```

As a hook argument we pass an object with properties `Component` which is our modal component. `showModal` is a function that return promise with our value passed to function `onResolve` in `Dialog` component.

More [examples](https://github.com/Harasz/use-async-modal/tree/main/examples) of usage.

## Demos

[Confirm dialog](https://codesandbox.io/s/use-async-modal-confirm-dialog-lbb7l)

[Information dialog](https://codesandbox.io/s/use-async-modal-information-dialog-nsrpe)

[Dialog with input](https://codesandbox.io/s/use-async-modal-dialog-with-input-jxobn)

[Animated dialog](https://codesandbox.io/s/use-async-modal-animated-dialog-808yp)

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://github.com/cmcken22/use-async-modal/blob/main/LICENSE)
