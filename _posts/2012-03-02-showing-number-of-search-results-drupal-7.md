---
layout: post
title: Showing the number of results that a search returns in Drupal 7
date: 2012-03-02 8:11
comments: false
external-url:
categories: [drupal7]
---

The boss handed me a search result page design that included a
"Showing x results" element. I bet you can guess that Drupal doesn't do that
with any available hook function or available variables/constants.

Searches in D7 can be themed from two files, `search-results.tpl.php` and
`search-result.tpl.php`. The first themes the results of the second which themes
individual search results. Handy!

Sadly, like I mentioned earlier, there's no default function for what I want to
do so I had to use a `template_preprocess_search_results()` function in my
template.php file. Make sure if you’re going to copy my code that you replace
the word "template" in that function with the machine name of your theme.

{% highlight ruby linenos %}
function yourtheme_preprocess_search_results(&$variables) {
  $variables['search_results'] = '';
  if (!empty($variables['module'])) {
    $variables['module'] = check_plain($variables['module']);
  }
  $search_count = array();
  foreach ($variables['results'] as $result) {
    $search_count[] = $result;
    $variables['search_results'] .= theme('search_result', array('result' => $result, 'module' => $variables['module']));
  }
  $search_count = count($search_count);
  $variables['count'] = $search_count;
  $variables['pager'] = theme('pager', array('tags' => NULL));
  $variables['theme_hook_suggestions'][] = 'search_results__' . $variables['module'];
}
{% endhighlight %}

This is pretty much the same as the standard version of the function except that
I created an empty array, and then populated it with results in that `foreach()`
function. Then I used PHP’s `count()` to see how many keys were in the array.
That’s the number of results.

The last part, `$variables['count']` is the special piece which makes it
available in the `search-results.tpl.php` file. So in that file, you can just
print `$count` anywhere and blamo, I have a display of the number of
results of a search.
