---
layout: post
title: Putting a Paypal link into a form loaded with colorbox using Drupal 7's FAPI
date: 2012-01-11 4:34
comments: false
external-url:
categories: [drupal, forms]
---

![Image](http://media.tumblr.com/tumblr_lxpc7tX4eO1qb67o2.jpg)

I hope my face relays the angst involved with this concept.

Here's what I wanted out of Drupal today:
 1. Have a main menu item load in a modal pop-up (Colorbox) instead of directing
    you to a page.
 2. Specifically, load the contact form link as a pop-up (and maybe newsletter
    subscriptions as well).

Apparently this is a huge pain in the assbutt.

Here's how to do it:

 - Crack open your theme.template file and add something like this in your
   `theme_preprocess_page()` with `drupal_add_js` in your doc ready function:

{% highlight js linenos %}
jQuery("#menu-532-1 a")
  .attr("href","http://yoursite.com/colorbox/form/form_id?width=500&amp;height=500&amp;iframe=false#form_id")
  .colorbox();
{% endhighlight %}

Thank your lucky stars you didn't dick around with this for hours.

Something to note is that this will not work for forms other than Contact,
User Register/Login and a few others. Webforms and the like require a highly
more annoying solution involving adding the form block to an invisible region in
the template and then pulling the form into colorbox manually with jquery. It
doesn't look pretty and also isn't the focus of this – so back to the
matter at hand.

Now is the trickiness - I needed to add some stuff to that pop-up, but the way I
did it I was only loading the form itself, which means I needed to modify the
form with Drupal's awesome Forms API (FAPI).

I created a module called `helper` to store my hooks and added this:

{% highlight ruby linenos %}
function helper_form_contact_site_form_alter(&amp;$form, &amp;$form_state, $form_id){<br/>
  $form['some_text'] = array(<br/>
    '#type' => 'item',
    '#markup' => '<p>markup</p>',
  );
}
{% endhighlight %}

Ok, yeah, that was easy. But now I need a Paypal donation link. Typically these
come as forms that you copy/pasta into your site. ~~But you can't hook a form
into another form, that's stupid.~~

Here's a link structure you can use in a form field's #markup:

{% highlight html linenos %}
<a href="https://www.paypal.com/cgi-bin/webscr?cmd=_xclick&amp;business=you@whatever.com&amp;item_name=Item%20Name%20With%20Spaces">
  <img src="https://www.paypal.com/en_US/i/btn/x-click-but21.gif" />
</a>
{% endhighlight %}
