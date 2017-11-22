# Sass-Styleguide
## Introduction
The following is a complete Sass styleguide for developing maintainable, scalable and effecient web apps.

### What is Sass?
Sass (stands for Syntactically Awesome Style Sheets) is an extension of CSS base on the Ruby language.
It lets you use features that do not exist in CSS in order to write better code.

### Sass vs SCSS
Sass includes two types of syntax:
1. Sass - uses the .sass file extension
2. Scss (Sassy CSS) - uses the .scss file extension
There are some minor syntax difference between the two version. For redability and compliancy with CSS always use Scss syntax

## The Styleguide
# General
These are some general rules that should allways apply
- Use tabs for indentation
- Use `kebab-case` instead of `camelCase` or `PascalCase` for names, for example:
  ```sass
  // Do
  .tooltip-header
  $default-font-path: "../assets/fonts";
  @mixin generate-font($name){
  ```
  ```sass
  // Don't
  .tooltipHeader
  .TooltipHeader
  .TOOLTIPHEADER
  $defaultFontPath
  ```
- 

## Architecture
One of the important advantages of Sass is the ability to split our code into modules.
Spliting our code will make it easier to handle, read and maintain and will more likely prevent code duplication and css colitions.

The recommended approach is to split the code as follows:
- scss
  - :file_folder:vendors
  - :file_folder:utils
  - :file_folder:base
    - typography
    - icons
  - :file_folder:styleguide
    - :file_folder:general
      1. fonts
      2. colors
    1. main
    2. headers
    3. paragraphs
    4. links
    5. tables
    6. lists
    7. buttons
  - :file_folder:3rd-party-components

### Utils
This folder should contain general app utilities, functions and mixins.
For example, this is a general font-face mixin that simplifies the task of adding new fonts to our app: 
```scss
@mixin font-face($name, $weight-key, $weight-value, $format: $default-font-format, $extension: $default-extension) {
  $path: '#{$default-font-path}/#{$name}/#{$name}-#{$weight-value}.#{$extension}';
  @font-face {
    font-family: $name;
    font-weight: $weight-key;
    src: url($path) format($format);
  }
```
* note: sass mixins are great for readability but note that each time you include a mixin it duplicates the generated CSS code, and therefore extends the bundle size, so it should be use moderately. In this case thought, since font-face has to be duplicated anyways for each new font that we are using, it's a good practice to use.

### Vendors

### Base
#### Normalize \ Reset
Since every browser comes with it's default stylings, sometimes in order to achieve a certain style we should first override the borwser's default styling. for example, lets say we have two types of lists in our app:

```scss
// in one file:
triage-host-list {
  list-style: none;
  padding: 0;
  margin: 0;
  color: blue;
}
// and in a different section:
users-list{
  list-style: none;
  padding: 0;
  margin: 0;
  color: deeppink;
}
```
Instead of reseting the default styles each time, It is recommended to have a default Normalize \ Reset Scss file that will initialize all browser default style rules. So in our reset.scss file, in the lists section we have:
```scss
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
```
And then, since `.triage-host-list` and `.users-list` will both be placed on `<ul>`s we wouldn't have to deal with reseting:

```scss
// in one file:
.triage-host-list {
  color: blue;
}
// and in a different section:
.users-list{
  color: deeppink;
}
```

In our app, we are using bootstarp's reboot.scss file for this task. There are places that the bootstrap resets are still not exactly what we want in our app. In these cases, resetin css will be done in the styleguide. (<=Add an example here)

#### Typography
App fonts sould be saved localy in `src/assets/fonts/` (and not loaded from an external server)
This file should include all the fonts used in our app (using the `generate-fonts` mixin)
```scss
@include generate-fonts("Lato");
@include generate-fonts("Roboto");
@include generate-fonts("Sans");
...
```
### The Styleguide

### Reusable Web Components (Specificaly Angular Components)
Modern web apps use the approach of reusable, self-contained components. 

For example, Lets say I am developing a card component that will contain a header and some content.
The recommended approach is to develop it as a whole component that can be reused anywhere in my application and can also easaly be exported to other applications.
So in our Angular App we should have a `card` directory, and inside it:
- `card.component.ts`
- `card.component.scss`

In this way the users of our component can write:
```html
<app-card>
  INSIDE_CONTENT
</app-card>
```
withoud the nead to dealing with classifying elements, and writing styles themslefs.



