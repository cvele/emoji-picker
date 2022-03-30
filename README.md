# :sunglasses: Emoji Picker

Instantly add Emoji support to input fields on your website! :thumbsup:

![Example Screenshot](http://onesignal.github.io/emoji-picker/screenshot.png)

**Demo:** http://onesignal.github.io/emoji-picker/demo

# Installation & Usage:

1. In your `<head>` section, add the following *stylesheet* links. Adjust the `lib/css` path to match yours.

  ```
  <link href="lib/css/emoji.css" rel="stylesheet">
  ```

2. Before the end of your `<body>` section, add the following *JavaScript* links. This library depends on jQuery, so jQuery must also be included, before these scripts are run. Once again, adjust the `lib/js` path to match yours.

  ```
  <!-- ** Don't forget to Add jQuery here ** -->
  <script src="lib/js/emoji-picker.min.js"></script>
  <script>
    $(function() {
      // Initializes and creates emoji set from sprite sheet
      window.emojiPicker = new EmojiPicker.EmojiPicker({
        emojiable_selector: '[data-emojiable=true]',
        assetsPath: '../lib/img/'
      });
      // Finds all elements with `emojiable_selector` and converts them to rich emoji input fields
      // You may want to delay this step if you have dynamically created input fields that appear later in the loading process
      // It can be called as many times as necessary; previously converted input fields will not be converted again
      window.emojiPicker.discover();
    });
  </script>
  ```
  EmojiPicker options

| Option | Type | Default | Description |
| ------ | ---- | ------- | ----------- |
| emojiable_selector | string | `'[data-emojiable=true]'` | selector for `<input>` |
| assetsPath | string | '' | path to emoji spritesheets |
| popupButtonClasses | string | '' | classes to be appended to the icon in the rendered input|

- Usage:
  ```
  <!-- Input field -->
  <input data-emojiable="true">

  <!-- Textarea with emoji image input -->
  <textarea data-emojiable="true"></textarea>

  <!-- Textarea with emoji Unicode input -->
  <textarea data-emojiable="true" data-emoji-input="unicode"></textarea>
  ```

# Configuring Options

**I want the Emoji selector to input Unicode characters instead of images**

Add `data-emoji-input="unicode"` to your input field. Only the `unicode` value is checked for; entering anything else has no effect.

**I want to limit my input field to a certain number of characters (maxlength)**

The `maxlength` property is supported. Character input and emoji input each count as one character, so it'll stop you from entering more than the max length.

**I want classes from my original input field to be copied over to the rich emoji input area**

They are!

# Trivia

### You get:
  - Input fields converted to contenteditable rich text areas with emoji support
  - A happy face icon on the top right of each rich text area, which brings up the menu on click
  - An emoji selection menu, with recently selected emojis at the top (thanks to angular-emoji-popup's author)
  - Text area values can be easily converted between Unicode and HTML (Unicode+Image Tags)

### What happens under the hood:
  - When you call `new EmojiPicker().discover()`, all elements with the data attribute `data-emojiable="true"` are found, a contenteditable div is created after each one, and the original input field is hidden.
  - When you type text into this contenteditable div, events are triggered upon each keypress/text change as well as each emoji selection, and the contents of this contenteditable div are copied to the original (now hidden) input field
  - Text entered into this contenteditable div is plain text; selected emojis are actually `<img>` tags
  - To get the value of the contenteditable div, call `element.val()` on the underlying hidden input field. The `<img>` emojis will be converted into Unicode emojis (plain text)

### Credits:
This is a slightly modified version of [angular-emoji-popup](https://github.com/Coraza/angular-emoji-popup), which was written based on [jquery-emojiarea](https://github.com/diy/jquery-emojiarea) (converts input fields to rich emoji input areas). This version removes AngularJS as a dependency.

### Improvements from the original forks:
  - The top-right smiley face that allows you to bring up the emoji picker menu
  - The smiley face shifts left appropriately when text entered exceeds the height and causes a scrollbar to appear
  - The `maxlength` property of input fields is respected (emoji selections count as a single character)
  - CSS classes from the original input field are copied over to the new contenteditable div

We built this to power emoji selection for [OneSignal](https://onesignal.com), our multi-platform push notification service.
