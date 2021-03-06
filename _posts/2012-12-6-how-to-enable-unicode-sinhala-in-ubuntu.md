---
layout: post
title: "How to Enable Unicode Sinhala in Ubuntu"
thumbnail: /images/posts/enable-sinhala-in-ubuntu/thumbnail_200x200.png
excerpt: "This article explains the procedure that should be followed to enable Sinhala language in Ubuntu 12.10. As of this writing 12.10 is the latest version of Ubuntu. Unity is the default desktop environment in Ubuntu 12.10, and the steps explained in this article are for Unity desktop environment."
tags:
- linux
- ubuntu
- unicode
- sinhala
---

<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/sinhala_language_570x260.png" class="img-polaroid">
</p>
<p>This article explains the procedure that should be followed to enable Sinhala language in Ubuntu 12.10. As of this writing 12.10 is the latest version of Ubuntu. Unity is the default desktop environment in Ubuntu 12.10, and the steps explained in this article are for Unity desktop environment.</p>
<p>First open the terminal. Type "terminal" in Unity Launcher press the enter key.</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/1_open_terminal_300x140.png" class="img-polaroid">
</p>
<p>Next type the following command in the terminal and press enter key.</p>

{% highlight bash %}
sudo apt-get install ttf-sinhala-lklug ibus im-switch ibus-m17n m17n-db m17n-contrib
{% endhighlight %}

You will be asked to enter the administrator password. Type the password and press enter.</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/2_terminal_520x340.png" class="img-polaroid">
</p>
<p>Once you press the enter key the packages required to install Sinhala language will be downloaded and installed automatically. This process may take few minutes depending on the speed of your internet connection.</p>
<p>After the process has completed open the unity launcher, type "ibus" and press enter. The IBus Preferences dialog will be opened. </p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/3_ibus_300x383.png" class="img-polaroid">
</p>
<p>Go to the "Input Method" tab in the IBus Preferences dialog.</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/4_ibus_input_method_tab_300x383.png" class="img-polaroid">
</p>
<p>Check the "Customize active input methods" checkbox. Then click on the "Select an input method" combo box and select "Sinhala; Sinhalese - wijesekera (m17n)". Click on the "Add" button.</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/5_ibus_select_sinhala_300x373.png" class="img-polaroid">
</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/6_after_selecting_sinhala_300x383.png" class="img-polaroid">
</p>
<p>Now close the dialog box and you will be able to see a little keyboard icon near to the top right corner of the screen. Click on that icon and select "Restart".</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/7_ibus_icon_300x80.png" class="img-polaroid">
</p>
<p>Click again in the keyboard icon and you will be able to select the Sinhala language from the available input methods.</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/8_ibus_icon_select_sinhala_340x205.png" class="img-polaroid">
</p>
<p>After selecting the Sinhala language you can use Unicode Sinhala in any compatible text editor.</p>
<p class="post-image-p">
	<img src="/images/posts/enable-sinhala-in-ubuntu/9_sinhala_typing_500x120.png" class="img-polaroid">
</p>
