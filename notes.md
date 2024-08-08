# React Native:

gives us a collection of "special" react components that are complied to native UI elements.
React-Native is like react-dom, it connects React to a specific platform (android & ios)

While the components are being compiled to their native UI forms, the javascript logic is not compiled, instead a javascript thread is created on react-native where it is hosted.

2 ways to create React native apps:

Expo CLI:
Managed app development,
convinient,
you can swith to react-native cli anytime.

React Native CLI:
bare-bone,
less convinient,
easier integration with native source code

To preview or test for IOS, we need to use xcode which only works on an IOS, more later...

To connect your local app to expo on your mobile, ensure your system and android device are on one the same wifi network.

# Styling:

No CSS, but we get inline styles or Stylesheet Objects (based on CSS syntax but only a subset of properties and features are supported)

Also, the style prop only works on some components like View and Text.

[NB:]
= View by default uses flex box.
stylings do not cascade - (child inheriting style from parent)

- By default, Views only take as much space as they need to fit thier children
- Nested Texts in Text are affected by the styling of thier parent Text component not bcos of inheritance (doesnt exist here) but because of the way react-native components are translated to native components.
- When setting a view or anyother component to "flex: 1", make sure its parent that need to be set is set to "flex:1" to avoid those collapsing isssues.
- Setting % in styling, refers to the % of the parent it is in.
- min, max, % can all be combined to achieve dynamic responsive app
- the style prop can recieve an object, an array or a callback

# IOS & Android styling differences:

some stylings do not work for both OS's and we sometimes need to write somethings differently to suite both of them.

for example, borderRadius does not work on IOS native component for <InputText />, we solve this by wrapping the text in a view and setting the style on the view instead so it works that way.

Another one (alt to android_ripple) is using the style prop and passing a callback that gets access to actions such as "pressed" to add certain styles.

For android_ripple to work well, we need to wrap our pressable inside a View.

[NB:]
To build your own button, you need to use the Pressable component and style it as you will, cos Button does not accept the style prop.

We've used modals.

Status bar can be used to adjust the bar of the view.

we can add a background color to the app in the app.json file

# Optimizing Lists:

ScrollView is only good for a short list of items because it always loads all the items even before they are displayed and if we have a very very long list, it might affect performance so we use FlatList for such instances.

# Debugging:

console.log, js debugger, react-devtools.

# We Respect Device Screen Resolutions with - SafeAreaView.

to ensure our content shows in a visible area of the view

[NB:]
Adding the statusbar component makes SafeAreaView not recognise the statusbar by default, i think RN justs leaves the faith of the statusbar to us to decide.

# Icons comes with Expo, but we need to install expo-font to use extra fonts.

npx expo install expo-font

the expo useFonts hook must be called in the root component.

# For loading we need an expo package:

expo-app-loading

so when we for example load fonts, we return the component from expo-app-loading so that it allows the prolonged display of the splash.png image until font is loaded and content displays.

FlatList
By default a flatlist has an infinite/unmeasured height, we can control this by wrapping it in a View and styling that View.

# Adaptive and Responsive UIs

# Dimensions API:

is a javascript method from react-native that we can use to access properties of the mobile device like screen width and height... then we can add stylings based on these values.

use the "useWindowDimensions" hook to monitor dynamic orientation change while using app

# Orientations:

Set orientation to default on app.json to allow flipping for landscape.

[NB:]
On Landscape, using keyboard might cover part of view (especially on IOS), to solve this, we need to wrap our view in KeyboardAvoidingView component and then in ScrollView to make it scrollable.

# Execute Platform-specific code:

We can use the "Platform" from react-native.

There are different approaches to doing this:

1. Platform.OS === 'android' / 'ios'
2. Platform.select({ios: '', android: ''})
3. Create file for a specific OS. (Card.android.js, Card.ios.js)
   [{important}: remove the android/ios xtension when you import the files]

# IOS:

for shadows to work on IOS, the container should have a background color.

# Navigation:

React Navigation is a package used for navigation.

using the native-stack comes with a template we can customize, like ash color bg and header with screen name. (edit with an option props)
We need the Stack.Navigator and all the different Stack.Screens to be navigated.

So we get special props passed to the components used in the Stack Navigator Screens ~ "navigation, route",
we can also alternatively use the useNavigation hook to use the navigation method in any component.

We can pass data through navigation by adding an object of our data in the navigation.navigate method and recieve it by using the route props in our components

# Styling Screen Headers & Backgrounds:

screenOptions props is added for a default props for all screens on the navigator, then individual option stylings take precedence if added

options prop on individual screens can also recieve a callback to add dynamic style/data to the screen.

Alternatively, we can also set the options inside the component using navigation.setOptions
Its a good practice to put the above in a useLayoutEffect (expo app complains [for max]).

My convention: So use the navigation and route props if we're directly using it in the screen component but use thier hooks if we're using it in a child component.

[NB]
When setting a remote image (uri), we need to set its width and height cos RN doesnt know its dimensions
If you need to interact with any of the header options set, just set it inside the component using the navigation.setOptions

# Drawer Navigation

Even though material tabs are a bit more specific for android, they can also be used for IOS. Bottom Tab works best for both.

# Nested Navigators

Create the navigator to be nested with its screens and pass it as a component to the point where we want the extra navigation

# Managing App Wide State

React Context & Redux (same as on web)

# Form

do not use autocorrect on email and similaer inputs

# Types:

check out sanni "awesome project" on github for type pattern.

# routing:

router.replace() doesnt give us a back button as it replaces the screen in the stack

# User Auth

firebase passwords must be at least 6 chars

In the case of token expiration, we either log the user out or reset the token

# Storing data on the Device

it works similar to storing on web localStorage.

# Native Device features (Camera, User Location, Device storage etc)

For Using Camera, rely largely on expo docs.

For IOS, we need to use the verifypermission method to successfully use the expo imagepicker
For Location, both IOS and Android requires permissions

NB: Use require if its an image on the project, but uri if its an external image.
