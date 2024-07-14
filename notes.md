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

# IOS & Android styling differences:

some stylings do not work for both OS's and we sometimes need to write somethings differently to suite both of them.

for example, borderRadius does not work on IOS native component for <InputText />, we solve this by wrapping the text in a view and setting the style on the view instead so it works that way.

Another one (alt to android_ripple) is using the style prop and passing a callback that gets access to actions such as "pressed" to add certain styles.

For android_ripple to work well, we need to wrap our pressable inside a View.

[NB:]
To build your own button, you need to use the Pressable component and style it as you will, cos Button does not accept the style prop.

We've used modals.

Status bar can be used to adjust the bar of the view.

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

# Execute Platform-specific code
