---
layout: post
title: Setting Your Input Format To Dvorak
date: 2013-05-01 12:00
comments: false
external-url:
categories: [dvorak]
---

In the first part of this series I promised this follow-up would have some
resources for folks who already use or who might like to start using the
fabulous Dvorak keyboard layout.

After amassing a trove of Dvorak resources it became obvious that fitting them
all into one post would be... hard to read. Instead, I'll be splitting up the
resources into separate posts based on a topic. This one, as the title suggests
is all about input formats.

If you have any contributions you'd like to make or questions you'd like to ask,
don't hesitate to ping me on Twitter or Freenode IRC (I'm carwin in both places).

## OS X

These instructions are grouped by most similar, there may be some minor differences.

### Snow Leopard / Lion / Mountain Lion

  1. Open System Preferences and click on Language & Text
  2. Choose Input Sources next and enable Dvorak.
  3. You'll likely want to change the keyboard layout for the login screen as well, to do so:
    - _System Preferences_
    - _Accounts_
    - _Login Options_
    - _Show input menu in login window_
    - After setting that option and changing it once from the login screen you
      shouldn't have to bother with it again.

### Tiger and earlier

  1. Open System Preferences and click on International
  2. Choose Input Menu and enable Dvorak.

Apple provides two different Dvorak options, not including the left/right hand
variants. The first is the regular US Dvorak and the second is Dvorak QWERTY,
aka: Big Fat Cheater's Dvorak.

BFC Dvorak's defining feature is that your keyboard layout will switch back to
QWERTY while you hold the `⌘` key, in effect keeping your shortcut habits intact.
If you're serious about using Dvorak, this input format will only slow you down.

You can leave other input sources available, but for your own sanity, make
sure you set the _"Use the same one in all documents"_ option.

_I'm missing images of older OS X environments, send me an email if you've got some!_

## Linux Consoles

The examples below are specifically from Arch Linux, but every flavor will have
a keymap file stored somewhere. A typical path is something like this
(although Arch is cool and won't make you find it):

`/usr/lib/kbd/keytables/dvorak.map`

### On the fly in a TTY

{% highlight ruby %}
# Replace 'dvorak' with the path to your keymap
> loadkeys dvorak
{% endhighlight %}

### Permanent solution for console keymap

{% highlight ruby %}
# /etc/vconsole.conf in Arch Linux
KEYMAP="dvorak"
{% endhighlight %}

Now when you boot into a TTY you'll be all set, which is pretty handy when it
comes time to enter login credentials.

## Chrome OS and ChromiumOS

  1. The first time you login to Chrome OS you're given the option to set your
     keyboard layout before doing anything else. Nice!
  2. If you've already set up Chrome OS with QWERTY or AZERTY, simply navigate
     to the following URL and choose Dvorak as the input method:
  `chrome://settings/languages`
  3. Yet a third way to edit you keyboard layout is to click through the UI of
     the operating system:
    - Click in the bottom right corner and choose _Settings_
    - When the resulting window appears, choose _Keyboard settings_.
    - Finally, select **US Dvorak keyboard** and click _Done_.

<details>
  <summary>Visual Walkthrough</summary>
  First time setup:
  ![cros1](/images/cros-dvorak1.png)
  Navigating the UI:
  ![cros2](/images/cros-dvorak2.png)
  ![cros3](/images/cros-dvorak3.png)
  ![cros4](/images/cros-dvorak4.png)
</details>

## Android (4.x)

This is actually a bit tricky since Android doesn't come with Dvorak enabled
although it is available. What you need to do is actually set up a
custom keyboard input.

  1. Navigate to _Settings_ and choose **Language & Input**
  2. Scroll down to _Keyboard & Input Methods_ and click your current keyboard
     layout. More than likely this is still **Default**.
  3. Scroll all the way to the bottom and choose **Advanced settings**.
  4. On the _Advanced settings_ page, choose **Custom input styles**.
  5. Click **Add style** at the bottom of the next screen.
  6. A popup box will appear, keep your Language the way it is unless you'd
     like to change it to something else, but select _Dvorak_ from
     the _Layout_ dropdown menu and click **Add**.

<details>
  <summary>Visual Walkthrough</summary>
  ![android1](/images/android-dvorak1.jpg)
  ![android2](/images/android-dvorak2.jpg)
  ![android3](/images/android-dvorak3.jpg)
  ![android4](/images/android-dvorak4.jpg)
  ![android5](/images/android-dvorak5.jpg)
  ![android6](/images/android-dvorak6.jpg)
</details>


That's it! After you click add the system will ask you if you'd like to enable
the new input format you created (Protip: you do) and you're off to the races!

## Windows XP

  1. Go to the Control Panel
  2. Click Regional and Language Options
  3. Click on the Languages tab
  4. On the Languages tab, click Details...
  5. In the resulting window, choose Add....
  6. Yet another window appears. In this one, check the Keyboard
     layout/IME: checkbox and select United States-Dvorak from the dropdown menu.
  7. Hit okay and the window will close, bringing you back to the window we saw
     in step 5. Make sure United States-Dvorak is selected and click Apply.
  8. Finally, select United States-Dvorak from the dropdown above.

<details>
  <summary>Visual Walkthrough</summary>
  ![xp1](/images/xp-dvorak1.png)
  ![xp2](/images/xp-dvorak2.png)
  ![xp3](/images/xp-dvorak3.png)
  ![xp4](/images/xp-dvorak4.png)
  ![xp5](/images/xp-dvorak5.png)
  ![xp6](/images/xp-dvorak6.png)
  ![xp7](/images/xp-dvorak7.png)
  ![xp8](/images/xp-dvorak8.png)
</details>

Interestingly, Microsoft provides directions for changing your keyboard layout
without ever touching your mouse: [link](http://www.microsoft.com/enable/training/windowsxp/keyboardlayout.aspx)

## Windows Vista

  1. Press the **Windows Key** + U
  2. Navigate to _Explore all Settings_ and choose **Make the keyboard easier to use.**
  3. Scroll down to _See Also_ and choose **Add a Dvorak keyboard and change 
     other keyboard input settings**.
  4. Switch to the **Keyboards and Languages** tab and choose **Change keyboards**.
  5. Switch to the **General** tab and click **Add**.
  6. Scroll down and expand **English (United States)** and **Keyboard**. 
     Click to fill one of the **United States-Dvorak** layout options.
  7. Finish by clicking **OK**.

<details>
  <summary>Visual Walkthrough</summary>
  ![vista1](/images/vista-dvorak1.png)
  ![vista2](/images/vista-dvorak2.png)
  ![vista3](/images/vista-dvorak3.jpeg)
  ![vista4](/images/vista-dvorak4.jpeg)
  ![vista5](/images/vista-dvorak5.jpeg)
  ![vista6](/images/vista-dvorak6.jpeg)
  ![vista7](/images/vista-dvorak7.jpeg)
  ![vista8](/images/vista-dvorak8.jpeg)
</details>

[~source](http://grok.lsu.edu/article.aspx?articleid=7852)

## Windows 7

  1. From the **Start** menu click **Control Panel**.
  2. In the Control Panel folder click the **Clock, Language, and Region** link
  3. Click the **Region and Language** control panel
  4. Click the **Keyboards and Languages** tab.
  5. Click the **Change Keyboard...** button
  6. On the **General** tab, press the **Add** button.
  7. Scroll down to **English (United States)**, expand it then check the box 
     for **United States - Dvorak**.
  8. Press **OK** buttons close the dialog boxes to finish.

<details>
  <summary>Visual Walkthrough</summary>
  ![win71](/images/win7-dvorak1.png)
</details>

[~source](http://windowstipoftheday.blogspot.com/2011/06/windows-7-using-dvorak-keyboard-layout.html)
