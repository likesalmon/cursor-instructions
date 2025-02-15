# /instructions/expo-tabs.md

Learn how to use the Tabs layout in Expo Router.

## Description: Learn how to use the Tabs layout in Expo Router

Tabs are a common way to navigate between different sections of an app. Expo Router provides a tabs layout to help you create a tab bar at the bottom of your app.

## Get started

You can use file-based routing to create a tabs layout. Here's an example file structure:

```text
app/
├── _layout.tsx
├── (tabs).tsx
  ├── _layout.tsx
  ├── index.tsx
  ├── settings.tsx
```

This file structure produces a layout with a tab bar at the bottom of the screen. The tab bar will have two tabs: **Home** and **Settings**:

You can use the **app/\_layout.tsx** file to define your app's root layout:

```tsx app/_layout.tsx
import { Stack } from "expo-router/stack";

export default function Layout() {
  return (
    <Stack>
      <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
    </Stack>
  );
}
```

The **(tabs)** directory is a special directory name that tells Expo Router to use the `Tabs` layout.

From the file structure, the **(tabs)** directory has three files. The first is **(tabs)/\_layout.tsx**. This file is the main layout file for the tab bar and each tab. Inside it, you can control how the tab bar and each tab button look and behave.

```tsx app/(tabs)/_layout.tsx
import { House } from "~/lib/icons/House";
import { Settings } from "~/lib/icons/Settings";

import { Tabs } from "expo-router";

export default function TabLayout() {
  return (
    <Tabs screenOptions={{ tabBarActiveTintColor: "violet-950" }}>
      <Tabs.Screen
        name="index"
        options={{
          title: "Home",
          tabBarIcon: ({ color }) => (
            <House className={`size-6 active:text-${color}`} />
          ),
        }}
      />
      <Tabs.Screen
        name="settings"
        options={{
          title: "Settings",
          tabBarIcon: ({ color }) => (
            <Settings className={`size-6 active:text-${color}`} />
          ),
        }}
      />
    </Tabs>
  );
}
```

Finally, you have the two tab files that make up the content of the tabs: **app/(tabs)/index.tsx** and **app/(tabs)/settings.tsx**.

```tsx app/(tabs)/index.tsx & app/(tabs)/settings.tsx
import { StyleSheet, Text, View } from "react-native";

export default function Tab() {
  return (
    <View className="flex-1 items-center justify-center">
      <Text>Tab [Home|Settings]</Text>
    </View>
  );
}
```

The tab file named **index.tsx** is the default tab when the app loads. The second tab file **settings.tsx** shows how you can add more tabs to the tab bar.

## Screen options

The tabs layout wraps the [Bottom Tabs Navigator](https://reactnavigation.org/docs/bottom-tab-navigator) from React Navigation. You can use the [options presented in the React Navigation documentation](https://reactnavigation.org/docs/bottom-tab-navigator/#options) to customize the tab bar or each tab.

## Advanced

### Hiding a tab

Sometimes you want a route to exist but not show up in the tab bar. You can pass `href: null` to disable the button:

```tsx app/(tabs)/_layout.tsx
import { Tabs } from "expo-router";

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen
        name="index"
        options={{
          /* @info Adding <CODE>href: null</CODE> in this tab's <CODE>options</CODE> will not show this tab in the tab bar.*/
          href: null,
          /* @end */
        }}
      />
    </Tabs>
  );
}
```

### Dynamic routes

You can use a dynamic route in a tab bar. For example, you have a `[user]` tab that shows a user's profile. You can use the `href` option to link to a specific user's profile.

```tsx app/(tabs)/_layout.tsx
import { Tabs } from 'expo-router';

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen
        {/* Name of the dynamic route.*/}
        name="[user]"
        options={{
          {/* Ensure the tab always links to the same href.*/}
          href: '/evanbacon',
          {/* OR you can use the href object.*/}
          href: {
            pathname: '/[user]',
            params: {
              user: 'evanbacon',
            },
          },
        }}
      />
    </Tabs>
  );
}
```

> **Note**: When adding a dynamic route in your tab layout, ensure that the dynamic route defined is unique. You cannot have two screens for the same dynamic route. For example, you cannot have two `[user]` tabs. If you need to have multiple dynamic routes, create a custom navigator.
