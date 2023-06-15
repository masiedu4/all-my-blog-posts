---
title: "Integrate a Rich-Text Editor into Next.js Applications in Just 4 Minutes"
seoTitle: "Integrate Draft-js' Rich-Text Editor into Next.js Applications"
seoDescription: "Learn how to seamlessly integrate a Draft.js rich-text editor into your Next.js applications."
datePublished: Thu Jun 15 2023 09:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cliwwuzpt071o3wnv6ctugzgk
slug: integrate-a-rich-text-editor-into-nextjs-applications-in-just-4-minutes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1686780097798/6e3e399f-8644-410b-b761-e276b72d017b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1686780065755/b4ed4428-8aa9-47ad-ae76-313cc24aa880.png
tags: markdown, editors, draftjs, nextjs, rich-text

---

The server-side rendering (SSR) capability of Next.js adds complexity when incorporating certain client-side dependencies in your applications.

In this tutorial, we will build a simple Rich-text editor with Next.js and an NPM dependency called Draft.js. There is scanty information on the topic and it took me a while and a lot of headaches to figure this out on my own.

At the end of this tutorial, give or take, you should set this up in your Next.js application within 4 minutes.

## Overview of the tools

* Next.js
    
* Draft.js and its supporting dependencies
    

### Install Next.js

* Check out the [official documentation](https://nextjs.org/docs/getting-started/installation) to set up Next.js if you haven't already.
    

### Configuring Rich Text Editor

Install these packages

* **Draft.js & React-draft-WYSIWYG**: A React framework for building text editors
    
* **draft-js-export-HTML & draft-js-import-HTML**: Packages for serializing content
    

```javascript
npm install draft-js react-draft-wysiwyg draft-js-export-html draft-js-import-html
```

**Create an Editor component and import these dependencies.**

```javascript
import { EditorState } from "draft-js";
import dynamic from "next/dynamic";
import { stateToHTML } from "draft-js-export-html";
import { stateFromHTML } from "draft-js-import-html";
import "react-draft-wysiwyg/dist/react-draft-wysiwyg.css"; // for styles

// strictly import the Editor this way for Next.js
const Editor = dynamic(
  () => import("react-draft-wysiwyg").then((module) => module.Editor),
  {
    ssr: false,
  }
);
```

**IMPORTANT.**

In Next.js, you can use the dynamic function from the `next/dynamic` package to load components dynamically, which is useful for components that are not needed during server-side rendering (SSR).

> **For React.js, import the Editor like this**

```javascript
// FOR React.js ONLY
import { Editor } from "react-draft-wysiwyg";
```

**Rendering a basic Draft.js editor**

```javascript
import { useState } from "react";
import { EditorState } from "draft-js";
import { stateToHTML } from "draft-js-export-html";
import { stateFromHTML } from "draft-js-import-html";
import "react-draft-wysiwyg/dist/react-draft-wysiwyg.css";
import dynamic from "next/dynamic";

const Editor = dynamic(
  () => import("react-draft-wysiwyg").then((module) => module.Editor),
  {
    ssr: false,
  }
);

const MyEditor = () => {
  const [editorState, setEditorState] = useState(() =>
    EditorState.createEmpty()
  );

  const handleChange = (newState) => {
    setEditorState(newState);
  };

  return (
    <div>
      <Editor editorState={editorState} onEditorStateChange={handleChange} />
    </div>
  );
};

export default MyEditor;
```

**Overview of the code**

We define a functional component called `MyEditor`. Within this component, we use the `useState` hook to create a state variable named `editorState` and its corresponding setter function, `setEditorState`. By default, `editorState` is set to an empty state created with `EditorState.createEmpty()`. The `handleChange` function updates the state with the new editor state whenever changes occur.

In the `return` statement, we render the `Editor` component provided by the `react-draft-wysiwyg` package. We pass in the `editorState` as a prop to display the current content of the editor. Additionally, we provide the `onEditorStateChange` prop to handle changes made by the user and update the state accordingly.

> The `editorState` == the `value` prop in HTML &lt;input /&gt; as the `onEditorStateChange` == `onChange` prop

**If you do everything right and import the component on a page. You should see this.**

![Outpur for React draft editor](https://cdn.hashnode.com/res/hashnode/image/upload/v1686762172936/74741cd2-7b09-4d0c-8637-22fb856d5c1f.png align="center")

We are done configuring the editor. We can now use our editor and track every state change.

Finally, let's serialize our content to be able to save and retrieve it from a database like MongoDB, Firebase and what have you.

## Serialize content for CRUD operations

The current state of our editor is an object that won't suffice if we want to save and retrieve it from a database. Put `console.log(editorState)` in the `handleChange` function and you will see a similar output below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686777881225/2ad4e2d9-ba8f-4f73-93f3-4b48cc9919d4.jpeg align="center")

The changes will be pretty straightforward. We are going to get the current content from the state and convert it to HTML.

Update the `handleChange` function as follows.

```javascript
const handleChange = (newState) => {
    setEditorState(newState);
    const contentState = editorState.getCurrentContent();
    const htmlVersion = stateToHTML(contentState);
    console.log(htmlVersion);
  };

// the serialized version is logged in the console on every change
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686778574919/17475e28-b413-4725-bafb-4d3191f241f3.jpeg align="center")

Now, we can pass the htmlVersion as a body to any POST and PATCH request we may need.

If you are fetching the htmlVersion from a database, it has to be converted back to readable text without the HTML tags but with all the styles and properties.

We will use the `stateFromHTML` to achieve this

```javascript
  const fetchFromDataBase = async () => {
    // fetch from database using axios or fetchAPI
    const response = axios.get("url");

    const htmlVersion = response.data;

    const textVersion = stateFromHTML(htmlVersion); // converted version
  };
```

### Conclusion

Throughout the article, we covered the installation and setup of the necessary dependencies, demonstrated how to dynamically load the React-Draft-Wysiwyg component, and showcased the implementation of a basic editor with state management. Additionally, we discussed how to handle content changes and provided an outline for serialization.

Kindly leave a comment if have any queries and I will attend to them. Thank you!

For technical writing and partnerships, [send me a mail](http://mailto:michaelasiedu148@gmail.com)