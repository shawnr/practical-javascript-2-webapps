# Using Vue Devtools

One of the helpful aspects of Vue.js is that there is a specialized tool called [Vue Devtools](https://github.com/vuejs/vue-devtools#vue-devtools) that we can use to help us debug our Vue.js applications. Vue Devtools can be installed in Chrome, Firefox, or Safari (via a workaround), and it is incredibly useful for debugging applications.

Install Vue Devtools for your browser of choice:

* [Chrome Extension](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd)
* [Firefox Addon](https://addons.mozilla.org/en-US/firefox/addon/vue-js-devtools/)
* [Safari Workaround](https://github.com/vuejs/vue-devtools/blob/master/docs/workaround-for-safari.md)

Once you have installed Vue Devtools into your browser, you can test the tool by loading your Vue project. Open the Developer Tools panel in your your browser and you should see the Vue Devtools tab available. (Consult the documentation for the specific browser you are using if you have trouble finding this tab.)


![Vue Devtools In Action](/img/vue-devtools1.png)
<br>Vue Devtools in action.

When we bring up the Vue Devtools tab, we can inspect the Vue application to see the current values of all the components we've defined in our application. In the example screenshot above, we can see that we have one component (the Editor) and it has a single data value. This data value can be changed by typing into the editor textarea, and the changes will be computed and reflected on the right side of the screen. We can see how the Vue Devtools information updates in real-time as we type.

