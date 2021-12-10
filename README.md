# Detached elements

When looking for a problem, we noticed the following.

For example, if you create a new project using the vue create command
in the Home.vue file, in the setup method, create an array steps containing, for example, {id: n} objects.

In the template, use v-for for each element of the steps array to create a div (let's call them the first level DIV).

Inside, we form several DIVs or other elements
and if one of the generated elements is a simple tag that does not contain calculations or a derivative, for example \<br>, \<div> 123 \</div>, \<span> a \</span>, then in some situations these elements are removed from the DOM model, but not are deleted from memory.

For example, if you clear the steps array, fill it with new values, or go to the About page.

If it contains only elements of the form \<div> {{index}} \<div> or \<div: key = "'s.id"> 123 </div> then they are normally removed from the DOM and from memory.

We also noticed that there are 2 options for clearing steps:
1. when steps is filled inside setup, then all the first-level elements and their contents freeze.
2. when steps is filled in onMount or later on by pressing a button, then when the steps array is cleared, only one element of the first level and its contents hang.

If you display many child elements inside the first-level elements, and do this on several pages using dynamic routing, then this leads to excessive memory consumption.