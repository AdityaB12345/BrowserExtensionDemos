https://developer.chrome.com/docs/extensions/get-started/tutorial/service-worker-events

For navigating the Chrome API reference pages quickly using the omnibox

manifest.json
- metadata
- icons
- main service worker: service-worker.js
    - two main features: sw-omnibox.js and sw-tips.js --> handle using "modules" that the main service-worker.js will import
- Register event listeners: all event listeners must be statically registered in global scope of service workers
    - register omnibox event listener with keyword trigger "api" (typing this keyword triggers the omnibox)
- permissions
    - storage: for persistent storage across service worker sessions (workers will be shut down if not needed)
    - alarms: for delayed/recurring tasks
- content scripts: content.js

service-worker.js: main service worker since manifest only takes a single JS file for service worker
- imports other service workers as modules

sw-omnibox.js: service worker mdoule for omnibox feature
- chrome.runtime.onInstalled(): use chrome.storage.local to set initial api ref page suggestions (tabs, storage, and scripting pages)
- chrome.omnibox.onInputChanged(): display suggestions after user starts typing
    - relies on statically registered omnibox event listener
- chrome.omnibox.onInputEntered(): open the Chrome API reference page based on what input the user entered
- updateHistory(): save omnibox input to storage.local so that recent searches can be used as future suggestions

sw-tips.js: service worker module for tips feature
- fetch tips, pick one at random, and save it to storage
- trigger alarm once per day to update tips. 
- alarms not saved when Chrome is closed, so need to check for alarm and create if needed
- message handler/listener: sends reply of the tip to the content script when the content script sends a request message to sw-tips.js

content.js: content script
- send message to service worker sw-tips.js to request for the tip --> once received, display it on the api reference pages