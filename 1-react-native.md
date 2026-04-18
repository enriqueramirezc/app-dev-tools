# React Native Documentation Summary

## React Native Basics

React Native is an open source framework for building Android and iOS applications using React and the app platform’s native capabilities. With React Native, you use JavaScript to access your platform’s APIs as well as to describe the appearance and behavior of your UI using React components

### Views and Mobile Development

In Android and iOS development, a view is the basic building block of UI: a small rectangular element on the screen which can be used to display text, images, or respond to user input. Even the smallest visual elements of an app, like a line of text or a button, are kinds of views. Some kinds of views can contain other views.

### Native Components

In Android development, you write views in Kotlin or Java; in iOS development, you use Swift or Objective-C. With React Native, you can invoke these views with JavaScript using React components. At runtime, React Native creates the corresponding Android and iOS views for those components. Because React Native components are backed by the same views as Android and iOS, React Native apps look, feel, and perform like any other apps. We call these platform-backed components Native Components.

### Core Components

| React Native UI Component | Android View  | iOS View       | Web Analog              | Description                                                                 |
|--------------------------|--------------|----------------|--------------------------|-----------------------------------------------------------------------------|
| `<View>`                 | `<ViewGroup>`| `<UIView>`     | A non-scrolling `<div>` | A container that supports layout with flexbox, style, some touch handling, and accessibility controls |
| `<Text>`                 | `<TextView>` | `<UITextView>` | `<p>`                   | Displays, styles, and nests strings of text and even handles touch events  |
| `<Image>`                | `<ImageView>`| `<UIImageView>`| `<img>`                 | Displays different types of images                                          |
| `<ScrollView>`           | `<ScrollView>`| `<UIScrollView>`| `<div>`               | A generic scrolling container that can contain multiple components and views |
| `<TextInput>`            | `<EditText>` | `<UITextField>`| `<input type="text">`   | Allows the user to enter text                                               |

```javascript
import React from 'react';
import {View, Text, Image, ScrollView, TextInput} from 'react-native';

const App = () => {
  return (
    <ScrollView>
      <Text>Some text</Text>
      <View>
        <Text>Some more text</Text>
        <Image
          source={{
            uri: 'https://reactnative.dev/docs/assets/p_cat2.png',
          }}
          style={{width: 200, height: 200}}
        />
      </View>
      <TextInput
        style={{
          height: 40,
          borderColor: 'gray',
          borderWidth: 1,
        }}
        defaultValue="You can type in me"
      />
    </ScrollView>
  );
};

export default App;
```

React Native uses the same API structure as React components, therefore, you’ll need to understand React component APIs to get started.

## React fundamentals

React is an open source library for building user interfaces with JavaScript. React Native runs on React.

Cat component example:

```javascript
import React from 'react';
import {Text} from 'react-native';

const Cat = () => {
  return <Text>Hello, I am your cat!</Text>;
};

export default Cat;
```

To define your Cat component, first use JavaScript’s import to import React and React Native’s Text Core Component

```tsx
import React from 'react';
import {Text} from 'react-native';
```

Your component starts as a function:

```tsx
const Cat = () => {};
```

Whatever a function component returns is rendered as a React element. React elements let you describe what you want to see on the screen.

Here the Cat component will render a <Text> element:

```tsx
const Cat = () => {
  return <Text>Hello, I am your cat!</Text>;
};
```

You can export your function component with JavaScript’s export default for use throughout your app like so:

```tsx
const Cat = () => {
  return <Text>Hello, I am your cat!</Text>;
};

export default Cat;
```

`<Text>Hello, I am your cat!</Text>` is using a kind of JavaScript syntax that makes writing elements convenient: JSX.

### JSX

React and React Native use JSX, a syntax that lets you write elements inside JavaScript like so: `<Text>Hello, I am your cat!</Text>`

- JSX is JavaScript
- You can use variables inside it

```tsx
import React from 'react';
import {Text} from 'react-native';

const Cat = () => {
  const name = 'Maru';
  return <Text>Hello, I am {name}!</Text>;
};

export default Cat;
```

- Any JavaScript expression will work between curly braces, including function calls like `{getFullName("Rum", "Tum", "Tugger")}`

```tsx
import React from 'react';
import {Text} from 'react-native';

const getFullName = (
  firstName: string,
  secondName: string,
  thirdName: string,
) => {
  return firstName + ' ' + secondName + ' ' + thirdName;
};

const Cat = () => {
  return <Text>Hello, I am {getFullName('Rum', 'Tum', 'Tugger')}!</Text>;
};

export default Cat;
```

The code above would show "Hello, I am Rum Tum Tugger!" on screen.

### Custom Components

React lets you nest components inside each other to create new components. These nestable, reusable components are at the heart of the React paradigm.

```tsx
import React from 'react';
import {Text, View} from 'react-native';

const Cat = () => {
  return (
    <View>
      <Text>I am also a cat!</Text>
    </View>
  );
};

const Cafe = () => {
  return (
    <View>
      <Text>Welcome!</Text>
      <Cat />
      <Cat />
      <Cat />
    </View>
  );
};

export default Cafe;
```

- Any component that renders other components is a parent component.

### Props

- short for “properties”
- Props let you customize React components
- For example, here you pass each <Cat> a different name for Cat to render:

```tsx
import React from 'react';
import {Text, View} from 'react-native';

type CatProps = {
  name: string;
};

const Cat = (props: CatProps) => {
  return (
    <View>
      <Text>Hello, I am {props.name}!</Text>
    </View>
  );
};

const Cafe = () => {
  return (
    <View>
      <Cat name="Maru" />
      <Cat name="Jellylorum" />
      <Cat name="Spot" />
    </View>
  );
};

export default Cafe;
```

This would show on screen:

```pseudo
Hello, I am Maru!
Hello, I am Jellylorum!
Hello, I am Spot!
```

Most of React Native’s Core Components can be customized with props, too. For example, when using Image, you pass it a prop named source to define what image it shows

```tsx
...
      <Image
        source={{
          uri: 'https://reactnative.dev/docs/assets/p_cat1.png',
        }}
...
```

### State

State is like a component’s personal data storage. State is useful for handling data that changes over time or that comes from user interaction. State gives your components memory!

The following example takes place in a cat cafe where two hungry cats are waiting to be fed. Their hunger, which we expect to change over time (unlike their names), is stored as state. To feed the cats, press their buttons—which will update their state.

```tsx

import React, {useState} from 'react';
import {Button, Text, View} from 'react-native';

type CatProps = {
  name: string;
};

const Cat = (props: CatProps) => {
  const [isHungry, setIsHungry] = useState(true);

  return (
    <View>
      <Text>
        I am {props.name}, and I am {isHungry ? 'hungry' : 'full'}!
      </Text>
      <Button
        onPress={() => {
          setIsHungry(false);
        }}
        disabled={!isHungry}
        title={isHungry ? 'Give me some food, please!' : 'Thank you!'}
      />
    </View>
  );
};

const Cafe = () => {
  return (
    <>
      <Cat name="Munkustrap" />
      <Cat name="Spot" />
    </>
  );
};

export default Cafe;
```

First, you will want to import useState from React: `import React, {useState} from 'react';`

Then you declare the component’s state by calling useState inside its function. In this example, useState creates an isHungry state variable:

```tsx
const Cat = (props: CatProps) => {
  const [isHungry, setIsHungry] = useState(true);
  // ...
};
```

Calling useState does two things:

it creates a “state variable” with an initial value—in this case the state variable is isHungry and its initial value is true
it creates a function to set that state variable’s value—setIsHungry

It doesn’t matter what names you use. But it can be handy to think of the pattern as [<getter>, <setter>] = useState(<initialValue>).

Next you add the Button Core Component and give it an onPress prop:

```tsx
<Button
  onPress={() => {
    setIsHungry(false);
  }}
  //..
/>
```

when someone presses the button, onPress will fire, calling the setIsHungry(false)

Finally, put your cats inside a Cafe component:

```tsx
const Cafe = () => {
  return (
    <>
      <Cat name="Munkustrap" />
      <Cat name="Spot" />
    </>
  );
};
```

### Handling Text Input

you could validate the text inside while the user types. For more detailed examples, see the React docs on controlled components, or the reference docs for TextInput.

A TextInput is one of many ways for the user to interact with your app. For examples of other ways to handle input, see the documentation on how to handle touches.

### Using a ScrollView

generic scrolling container that can contain multiple components and views. 

```tsx
import React from 'react';
import {Image, ScrollView, Text} from 'react-native';

const logo = {
  uri: 'https://reactnative.dev/img/tiny_logo.png',
  width: 64,
  height: 64,
};

const App = () => (
  <ScrollView>
    <Text style={{fontSize: 96}}>Scroll me plz</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{fontSize: 96}}>If you like</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{fontSize: 96}}>Scrolling down</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{fontSize: 96}}>What's the best</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{fontSize: 96}}>Framework around?</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{fontSize: 80}}>React Native</Text>
  </ScrollView>
);

export default App;
```

### Using List Views

The FlatList component displays a scrolling list of changing, but similarly structured, data. FlatList works well for long lists of data, where the number of items might change over time. Unlike the more generic ScrollView, the FlatList only renders elements that are currently showing on the screen, not all the elements at once.

The FlatList component requires two props: data and renderItem.

```tsx
import React from 'react';
import {FlatList, StyleSheet, Text, View} from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 22,
  },
  item: {
    padding: 10,
    fontSize: 18,
    height: 44,
  },
});

const FlatListBasics = () => {
  return (
    <View style={styles.container}>
      <FlatList
        data={[
          {key: 'Devin'},
          {key: 'Dan'},
          {key: 'Dominic'},
          {key: 'Jackson'},
          {key: 'James'},
          {key: 'Joel'},
          {key: 'John'},
          {key: 'Jillian'},
          {key: 'Jimmy'},
          {key: 'Julie'},
        ]}
        renderItem={({item}) => <Text style={styles.item}>{item.key}</Text>}
      />
    </View>
  );
};

export default FlatListBasics;
```

## Environment Setup

Using Expo framework is recommended

### Using Expo

Expo is a framework of tools and services for React Native that focuses on helping you build, ship, and iterate on your app, to use preview deployment workflows that are popular with web development, and to automate your development workflows. Expo also makes it possible to build React Native apps without ever touching Xcode or Android Studio, and it doesn't get in the way if you want to use those tools.
