# Expo framework

As mentioned in the previous section, Expo is a framework of tools and services for React Native. Expo makes it possible to build React Native apps without ever touching Xcode or Android Studio.

## Creating a Basic Application

Say we wanted to turn the following code into a user-application:

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

For that, we'd first need to create an expo project on our current directory (`npx create-expo-app MyApp --template blank`), then inspect the folder (`cd MyApp`) and create an `App.tsx` file with the code on the root of the project folder.

Once that's done, the next step would be to start the dev server: `npx expo start`. This command will generate a QR code on terminal that we could then scan in order to test the app with Expo Go on our phone.

You can also run it on an Android emulator (such as Android Studio) by pressing `a`, or an iOS simulator (only on Mac) by pressing `i`.

```bash
› Using Expo Go
› Press s │ switch to development build

› Press a │ open Android
› Press w │ open web

› Press j │ open debugger
› Press r │ reload app
› Press m │ toggle menu
› shift+m │ more tools
› Press o │ open project code in your editor

› Press ? │ show all commands
```

## Expo Project Templates

- `npx create-expo-app <appname>` creates a  file-based routing template. in that case, the entry point would be `app/(tabs)/index.tsx`. I.e, that's where we should put the code.

- `npx create-expo-app <appname> --template blank` creates a simpler version. Here, we just have to replace `App.js` for `App.tsx`.

### File-Based Routing

Expo Router turns files inside an `app/` directory into routes automatically.

Best for multi-screen apps, anything that needs navigation (tabs, stacks, drawers), or apps targeting both mobile and web.

- Refactoring is easier since you can move files around without updating routing imports or components.
- More boilerplate

### Blank Template

Best for prototypes, single-screen tools or learning React Native basics

- Less overhead for simple apps.
- You have to wire up navigation yourself if you need it.

If an app has more than 1 screen file-based routing is best.

`MyApp/` contains a project example that uses file-based routing. `NotherApp/` contains a project using a blank template.

