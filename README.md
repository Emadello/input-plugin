Install:

cordova plugin add cordova-plugin-nativeinput

# forked from AppGyver Native Input Plugin

This plugin renders a native view (panel) at the bottom of the webview that contains:
 | leftButton - inputField - rightButton |

This allows for apps with chat views to have a better user experience where
the input field is native and moves up and down with soft-keyboard.

All components can be styled using css:
```
/*default values*/

/*default css class for the inputField*/
.nativeInput {
  background-color: white;
  color:black;
}

/*default css class for the panel */
.nativeInput-panel {
  background-color: white;
}

/*default class for the left button */
.nativeInput-leftButton {
  background-color: whitesmoke;
}

.nativeInput-leftButton:pressed {
  background-color: #C0C0C0;
}

/*default class for the right button */
.nativeInput-rightButton {
  background-color: whitesmoke;
}

.nativeInput-rightButton:pressed{
  background-color: #C0C0C0;
}
```

## Usage
### cordova.plugins.NativeInput.show(params)

```
params = {
      leftButton:{
        styleCSS: 'text:Up;color:blue;background-color:gray;'
      },
      rightButton: {
        styleClass: 'myRightButtonClass',
        cssId: 'myRightButton'
      },
      panel: {
        styleClass: 'grey-panel'
      },
      input:{
        placeHolder: 'Type your message here',
        type: 'normal',
        lines: 1,
        styleClass: 'myInputClass'
      }
 }

 cordova.plugins.NativeInput.show(params);
```

#### leftButton / rightButton
There are the buttons that can be displayed at the left and/or right of the input field.
You can specify the native css using a class, id or in-line css.
```
{
  styleId:'',
  styleClass:'',
  styleCSS:''
}
```
When one of the buttons is tapped the event can be handled using:

```
cordova.plugins.NativeInput.onButtonAction(function(side){
  if("left" === side){
    console.log("left button tapped");
  }
  if("right" === side){
    console.log("right button tapped");
  }
});
```

#### panel
This is the panel that goes behind the input field and buttons.
You can use css to configure it's look and feel.
The default style is with white background.


#### input
The actual input field.
You can use css to configure it's look and feel (styleId, styleClass and styleCSS).

You can also configure the following options:

* type - string - Defines the behaviour of the input field and the soft keyboard. Possible values: ('uri', 'normal', 'email', 'number')

* placeHolder - Text that appears in the input field while it is empty.

* lines - (Android Only) Number of lines that the input field will support. When you specify 1 the input field is confifure as single line.
When lines > 1 the input field is configure as mult-line and will grow in size as the user adds more lines to the text.

### cordova.plugins.NativeInput.hide()
Hide the whole panel including: buttons, input field and etc.
```
cordova.plugins.NativeInput.hide();
```

### cordova.plugins.NativeInput.onKeyboardAction(autoCloseKeyboard, handler);

* autoCloseKeyboard - If the keyboard should be closed after the "action button"
is tapped.

```
cordova.plugins.NativeInput.onKeyboardAction(true, function(action){
  ...
});

```
* autoCloseKeyboard: When true it will close the keyboard after any keyboard action is triggered.
* handler: The handle function can be called multiple times when a keyboard action has occurred.
The handler function receives a parameter action with the possible values: done, go, next, send, newline

### cordova.plugins.NativeInput.onButtonAction(handler);
```
cordova.plugins.NativeInput.onButtonAction(function(side){
  if("left" === side){
    console.log("left button tapped");
  }
  if("right" === side){
    console.log("right button tapped");
  }
});
```

The handler function can be called multiple fimes when a button is tapped. It receives a parameter side with the possible values: left, right

### cordova.plugins.NativeInput.closeKeyboard()
Close the soft keyboard.
```
cordova.plugins.NativeInput.closeKeyboard();
```

### cordova.plugins.NativeInput.onChange(handler)
```
cordova.plugins.NativeInput.onChange(function(value){
  ... //do something with the new value
});
```
The handler function will be called multiples times when the content of the input field changes.

### cordova.plugins.NativeInput.getValue(handler)
```
cordova.plugins.NativeInput.getValue(function(value){
  ... //do something with the value
});
```
The handler function will be called once with the current value of the input field.
