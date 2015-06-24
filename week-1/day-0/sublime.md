# Sublime Text

Your editor is going to be your best friend so we need to make sure that is is ready for everything that we'll be throwing at it throughout this course.
The first thing that we will do is cover some of the basic shortcuts that are built in to Sublime Text and we will explore our new home.

## General Keyboard Shortcuts

The basic keyboard shortcuts that you are used to will still work, but let's review a couple of them before moving on to specific ones for Sublime.

- `CMD+C`
- `CMD+P`
- `CMD+X`
- `CMD+S`
- `CMD+Z`
- `CMD+SHIFT+Z`
- `CMD+Shift+S`
- `CMD+F`
- `CMD+W`
- `CMD+Q`
- `CMD+TAB`
- `CMD+Tilde`

## Navigating Text

When working with text and our text editor, it is extremely slow to move away from the keyboard for anything except long scrolling or navigating web pages.
So, let's work on how we can use our arrow keys plus a few tricks to move around our documents.

- `CMD`
- `Alt`
- `Shift`
- `FN`
- `Delete`

## Sublime Shortcuts

Now that we know our home base of shortcuts, let's get used to some of the shortcuts that Sublime Text offers to us.

- `CMD+D`
- `CMD+SHIFT+D`
- `CMD+G`
- `CMD+CTRL+G`
- `CMD+K CMD+B`
- `CMD+J`
- `CMD+CTRL+UP`
- `CMD+CTRL+DOWN`
- `CMD+SHIFT+T`

## Sublime Commands

Now that we have some of the navigation down, we can look at working on making Sublime text really start bending to our needs.

- `CMD+P`
- `CMD+SHIFT+P`

## Installing Package Control

Out of the box, Sublime Text is INCREDIBLY powerful.
But, with the help of some after market parts we can make our editor even more useful.
First we will need to install a package manager.
Just like Mac has Brew, Sublime Text has Package Control.

To install it, let's follow the instructions from the [Package Control Website](https://packagecontrol.io/installation):

- Access the Sublime Console using `CTRL+Tilde`
- Paste in the following code from the link above
- Close and restart Sublime Text

## Installing Our First Set of Packages

Now that we have our package manager installed, we can install our first packages to get up and running.

To install a package open the command palate and then start typing in `install` until you see an entry for "Package Control: Install Package".
Now we can search the HUGE list of available packages for ones that will improve our productivity.
To get started let's install:

- Dayle Rees Colour Schemes
- Case Conversion
- Change Quotes
- Color Picker
- Git (make sure this is not "Sublime Git")
- Change Quotes
- Git Gutter
- Markdown Preview
- Markdown Editing
- Sidebar Enhancements
- Origami
- Spacegray
- SASS
- SCSS

That's a whole lot and we will be installing more as the course keeps going.
But this will get us started and will allow us to work with our editor much smarter!

## User Settings

Now to make our editor look a bit better and perform a bit better, there are a few user settings that we can add.
To open up your personal settings for Sublime use the shortcut `CMD+,`.
Here in this file, select all of the text and paste in the following:

```json
{
    "close_windows_when_empty": true,
    "color_scheme": "Packages/Dayle Rees Color Schemes/sublime/halflife.tmTheme",
    "ensure_newline_at_eof_on_save": true,
    "font_size": 16,
    "ignored_packages":
    [
        "Vintage",
        "Markdown"
    ],
    "line_padding_bottom": 8,
    "line_padding_top": 8,
    "theme": "halflife.sublime-theme",
    "trim_trailing_white_space_on_save": true
}
```

This will theme your editor, add some spacing, change the font size, and add some extra code style helpers.
