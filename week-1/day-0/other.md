# ZSH and iTerm2

Now that we have a smarter editor, let's make a smarter terminal!
Right now, our terminal is pretty basic white and black and it doesn't really show us much.
Let's work on upgrading this a good bit.

## iTerm2

When we rand the super installer script we installed a new program called iTerm2.
This is a drop in replacement for the built in Apple Terminal, but it has a lot more options in terms of flexibility and configuration.
So let's start by opening iTerm2.

## Installing zsh

So fare our terminal has been using a program called "bash" to run and interpret all of our input as well as the different commands like `cd`, `mkdir`, `open`, `etc`.
But, there is something better than bash (at least in my opinion) and it will really add to the speed and flexibility of our terminal experience.

The program we'll be installing is called `zsh` which is a drop in replacement for bash, but it has some extra power baked in and some better defaults when it comes to productivity.
To install `zsh`, we just need to go back to our old friend Homebrew:

```
brew install zsh
```

## Switching From bash to zsh

Even though we've installed zsh, we are still using bash as our shell prompt.
First we need to find where Homebrew installed zsh for us:

```
which zsh
```

Now our session should print out the path to `zsh` and we can highlight and copy this.
Then we can run this command to switch our default shell (this assumes that `zsh` is located at `/bin/zsh`:

```
chsh -s /bin/zsh
```

Now if you open a new terminal session with `CMD+N` or `CMD+T` your prompt should look just a little bit different.

## Fast Wins with ZSH

One of the biggest wins with ZSH is that our tab completion works ALOT better.
Now instead of getting a terrible "bonk" when you try to tab complete, zsh automatically suggests the file you are looking for.
If there are multiple files that could match your search, then it will suggest all of them and you can tab through each before selecting one with `ENTER`.
Also, one of the big wins for ZSH is that autocomplete is no longer case sensitive, this better matches the fact that by default, Mac hard drives are case-insensitive (although most servers are not).

> **NOTE** Most of these improvements are possible with bash, but zsh saves at least one hit of the TAB button per autocomplete.
> When you are in the terminal all day this adds up to a lot of saved time!

## Theming iTerm

So far, we have our autocomplete working a bit better by using ZSH, but our terminal is still kinda dull looking.
So let's make things a bit better.

- Go to https://github.com/mbadolato/iTerm2-Color-Schemes and choose a color scheme that you like for your terminal (I recommend one with really distinct colors rather than something monochrome, this will save time when scanning terminal output for errors and other messages)
- Run the following command to download the color schemes `git clone git@github.com:mbadolato/iTerm2-Color-Schemes.git ~/.term-colors`
- Open the new `.term-colors` directory: `open ~/.term-colors`
- In finder go to `schemes` and open the color scheme you chose
- Open iTerm Preferences by using `CMD+,`
    + Under "Profiles" and "Colors" click "Load Preset"
    + Find the preset you wanted from the drop down list
