https://developer.chrome.com/docs/extensions/get-started/tutorial/popup-tabs-manager

Tab manager popup to organize Chrome extension and Chrome Web store documentation tabs

manifest.json
- metadata
- icons
- extension action
    - popup.html as default popup (popup display when icon clicked)
- permissions
    - tabGroup
- host_permissions: grant elevated permissions to specific sites only
    - https://developer.chrome.com/*

popup.html: html for the popup
- uses popup.css as the stylesheet
- incorporates popup.js

popup.css: stylesheet for the popup.html popup

popup.js: script for the popup.html popup
- query the tabs, manage, group the tabs, etc