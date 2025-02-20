
# ColorisColorpicker ("0.32.0")

This is a fork of the great repo from mdbassit/Coloris.
All credits goes to Momo, he did a great job. Unfortunately he will preserve his version of Coloris and will not allow further contributions.
That was the reason for this forked repo.
Feel free to contribute.

![image](https://github.com/MattOpen/ColorisColorpicker/assets/4366385/e32d072d-ce6e-40d8-bfa7-31a0e1a63f82)

A lightweight and elegant JavaScript color picker written in vanilla ES6.  
Convert any text input field into a color field.

[**View demo**](https://coloris.js.org/examples.html)

## Features

* Zero dependencies
* Very easy to use
* Customizable
* Themes and dark mode
* Opacity support
* Color swatches
* Multiple color formats
* Touch support
* Fully accessible
* Works on all modern browsers (no IE support)

## Features NEW since Feb 2024 (only in ColorisColorpicker)

* Configure each instance separately
* Configure with data attribute "data-config"
* enhanced initialization process
* works now with appended input fields after page load
* add cursorOffsetX and cursorOffsetY to settings

## Getting Started

### Basic usage

Download the [latest version](https://github.com/MattOpen/ColorisColorpicker/releases/latest), and add the script and style to your page:
```html
<link rel="stylesheet" href="coloris.min.css"/>
<script src="coloris.min.js"></script>
```

Then just add the data-coloris attribute to your input fields:
```html
<input type="text" data-coloris>
```

Then initialize the module:
```JavaScript
  Coloris();
```

That's it. All done!

### Customizing the color picker

The color picker can be configured by calling `Coloris()` and passing an options object to it. For example, to activate **dark** mode and disable **alpha** support, add some swatches, change button to round and left:

Important: pass a selector when calling Coloris()

The default selector is '[data-coloris]'.
If you pass the default selector, this will overwrite the coloris default settings with your own settings. Your new settings will be reflected by all instances.

```js
Coloris({
  el: '[cdata-oloris]',
  themeMode: 'dark',
  alpha: false,
  clearButton: false,
  buttonStyle: 'circle button-left',
  swatches: [
    '#264653',
    '#2a9d8f',
    '#e9c46a'
  ]
});
```

You can configure the color picker also by adding a data attribute like below.
All options were possible.
Options defined as data attribute will overwrite the settings options, but at any time after init, you can change the instance again, by calling Coloris({...})
```js
<input type="text" class="instance5" data-coloris style="background-color: transparent;" value="#00a5cc" data-config="{%22el%22:%22.instance5%22,%22buttonStyle%22:%22full-transparent%22,%22themeMode%22:%22dark%22,%22theme%22:%22default%22,%22wrap%22:true,%22showButtonThumb%22:true}">
```


Here is a list of all the available options:

```js
Coloris({
  // The default behavior is to append the color picker's dialog to the end of the document's
  // body. but it is possible to append it to a custom parent instead. This is especially useful
  // when the color fields are in a scrollable container and you want the color picker's dialog
  // to remain anchored to them. You will need to set the CSS position of the desired container
  // to "relative" or "absolute".
  // Note: This should be a scrollable container with enough space to display the picker.
  parent: '.container',

  // A custom selector to bind the color picker to. This must point to HTML input fields.
  el: '.color-field',

  // The bound input fields are wrapped in a div that adds a thumbnail showing the current color
  // and a button to open the color picker (for accessibility only). If you wish to keep your
  // fields unaltered, set this to false and no div wrapper div will be created.
  wrap: true,

  // Set to true to activate basic right-to-left support.
  rtl: false,

  // Available themes: default, large, polaroid, pill (horizontal).
  // More themes might be added in the future.
  theme: 'default',

  // Set the theme to light or dark mode:
  // * light: light mode (default).
  // * dark: dark mode.
  // * auto: automatically enables dark mode when the user prefers a dark color scheme.
  themeMode: 'light',

  // The margin in pixels between the input fields and the color picker's dialog.
  margin: 2,

  // Set the preferred color string format:
  // * hex: outputs #RRGGBB or #RRGGBBAA (default).
  // * rgb: outputs rgb(R, G, B) or rgba(R, G, B, A).
  // * hsl: outputs hsl(H, S, L) or hsla(H, S, L, A).
  // * auto: guesses the format from the active input field. Defaults to hex if it fails.
  // * mixed: outputs #RRGGBB when alpha is 1; otherwise rgba(R, G, B, A).
  format: 'hex',

  // Set to true to enable format toggle buttons in the color picker dialog.
  // This will also force the format option (above) to auto.
  formatToggle: false,

  // Enable or disable alpha support.
  // When disabled, it will strip the alpha value from the existing color string in all formats.
  alpha: true,

  // Set to true to always include the alpha value in the color value even if the opacity is 100%.
  forceAlpha: false,

  // Set to true to hide all the color picker widgets (spectrum, hue, ...) except the swatches.
  swatchesOnly: false,

  // Focus the color value input when the color picker dialog is opened.
  focusInput: true,

  // Select and focus the color value input when the color picker dialog is opened.
  selectInput: false,

  // Show an optional clear button
  clearButton: false,

  // Set the label of the clear button
  clearLabel: 'Clear',

  // Show an optional close button
  closeButton: false,

  // Set the label of the close button
  closeLabel: 'Close',

  // An array of the desired color swatches to display. If omitted or the array is empty,
  // the color swatches will be disabled.
  swatches: [
    '#264653',
    '#2a9d8f',
    '#e9c46a',
    'rgb(244,162,97)',
    '#e76f51',
    '#d62828',
    'navy',
    '#07b',
    '#0096c7',
    '#00b4d880',
    'rgba(0,119,182,0.8)'
  ],

  // Set to true to use the color picker as an inline widget. In this mode the color picker is
  // always visible and positioned statically within its container, which is by default the body
  // of the document. Use the "parent" option to set a custom container.
  // Note: In this mode, the best way to get the picked color, is listening to the "coloris:pick"
  // event and reading the value from the event detail (See example in the Events section). The
  // other way is to read the value of the input field with the id "clr-color-value".
  inline: false,

  // In inline mode, this is the default color that is set when the picker is initialized.
  defaultColor: '#000000',

  // A function that is called whenever a new color is picked. This defaults to an empty function,
  // but can be set to a custom one. The selected color and the current input field are passed to
  // the function as arguments.
  // Use in instances (described below) to perform a custom action for each instance. 
  onChange: (color, input) => undefined,

  //  renders a button next to the Coloris input. The button will show the actual color
  showButtonThumb:true,

  //  set the button style. Possible options "circle", "square", "default", "full" and "full-transparent"
  //  except full, all buttons are aligned to the right.
  //  add "button-left" and the button will be aligned to the left
  buttonStyle: 'circle button-left',

});
```

### Accessibility and internationalization

Several labels are used to describe the various widgets of the color picker, which can be read aloud by a screen reader for people with low vision. If you wish to customize or translate those labels, you need to add an "a11y" option to the global Coloris object:

```js
Coloris({
  a11y: {
    open: 'Open color picker',
    close: 'Close color picker',
    clear: 'Clear the selected color',
    marker: 'Saturation: {s}. Brightness: {v}.',
    hueSlider: 'Hue slider',
    alphaSlider: 'Opacity slider',
    input: 'Color value field',
    format: 'Color format',
    swatch: 'Color swatch',
    instruction: 'Saturation and brightness selector. Use up, down, left and right arrow keys to select.'
  }
});
```

### initialize Coloris with your own setting and overwrite default setting


```js
//  !!!"setInstance" - this wont be supported any longer!!!
Coloris.setInstance('.instance2', {...}

//  in case you will setup a single Color field or multiple matching a class selector
//  use the default initialization syntax with a different selector

      Coloris({
        el: '.instance1',
        buttonStyle: 'square button-left',
        themeMode: 'dark',
        theme: 'default',
        wrap: true,
        showButtonThumb: true
      });

      Coloris({
        el: '.instance2',
        buttonStyle: 'circle',
        themeMode: 'dark',
        theme: 'large',
        wrap: false,
        showButtonThumb: true
      });

      Coloris({
        el: '.instance3',
        theme: 'pill',
        themeMode: 'light',
        formatToggle: true,
        closeButton: true,
        clearButton: false,
        buttonStyle: 'full',
        swatches: [
          '#264653',
          '#2a9d8f',
          '#e9c46a'
        ]
      });
```

Any options that haven't been explicitly set by an instance will inherit the global values. So any common options should be set globally using the method described in the "Customizing the color picker" section above.

Every Coloris element has its own instance.
Instances can be found here:

  "Coloris.instances"

All options can now be changed per instance.

### Events

All events are triggered on the last active input field that is bound to the color picker.

| Event    | Description                                                   |
| -------- | ------------------------------------------------------------- |
| `open`   | The color picker is opened                                    |
| `close`  | The color picker is closed                                    |
| `input`  | A new color is selected                                       |
| `change` | The color picker is closed and the selected color has changed |

In addition to the events above, a `coloris:pick` event is triggered on the `document` whenever a new color is picked. Example:

```js
document.addEventListener('coloris:pick', event => {
  console.log('New color', event.detail.color);
});
```

### Manually updating the thumbnail

The color thumbnail is updated when an `input` event is triggered on the adjacent input field. If you programmatically update the value of the input field, you may need to trigger the event manually using the following code:

```js
document.querySelector('#color-field').dispatchEvent(new Event('input', { bubbles: true }));
```

### Closing the color picker

The color picker dialog can be closed by clicking anywhere on the page or by pressing the ESC on the keyboard. The later will also revert the color to its original value.

If you would like to close the dialog programmatically, you can do so by calling the `close()` method:
```js
// Close the dialog
Coloris.close();

// Close the dialog and revert the color to its original value
Coloris.close(true);
```

## Building from source

Clone the git repo:
```bash
git clone git@github.com:MattOpen/ColorisColorpicker.git
```

Enter the Coloris directory and install the development dependencies:
```bash
cd Coloris && npm install
```

Run the build script:
```bash
npm run build
```
The built version will be in the `dist` directory in both minified and full copies.

Alternatively, you can start a gulp watch task to automatically build when the source files are modified:
```bash
npm run start
```

## Contributing

If you find a bug or would like to implement a missing feature, please create an issue first before submitting a pull request (PR).

## License

Copyright (c) 2021 Momo Bassit.  
**Coloris** is licensed under the [MIT license](https://github.com/MattOpen/ColorisColorpicker/LICENSE).
