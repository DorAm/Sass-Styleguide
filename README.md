# Sass-Styleguide
## Introduction
The following is a complete Sass styleguide for developing maintainable, scalable and effecient web apps using Sass.

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
  
Modern web apps use the approach of reusable, self-contained components. 
In order to m
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



