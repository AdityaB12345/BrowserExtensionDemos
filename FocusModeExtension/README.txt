https://developer.chrome.com/docs/extensions/get-started/tutorial/scripts-activetab

manifest.json
- Define the icons
- Register the service worker "background.js"
- Enable the extension action
- Specify permissions: 
    - activeTab (temporary ability to access sensitive properties of and execute code on the current tab)
    - scripting (gives this extension the ability to insert/remove CSS/StyleSheet)
- Define special commands
    - Ctrl+B (Command+B for mac)
    - _execute_action key: runs same code as action.onClicked() but when commands are used

background.js (service worker)
- chrome.runtime.onInstalled(): set status to default to OFF via action badge (banner on top of extension action) 
    - uses chrome.action.getBadgeText()/setBadgeText()
- chrome.action.onClicked(): 
    - set new state of extension on current tab to be opposite of prev state (if OFF, set to ON and vice versa)
    - use chrome.scripting.insertCSS()/removeCSS() to inject/remove StyleSheet based on new state of extension on current tab




Extension "action": the extension's toolbar icon
- Defines icon appearance + behavior: what happens when the icon is clicked (run code, display popup, etc), etc

service worker: JavaScript environemnts that handle/monitor/respond to events in the background
- terminate when not needed




The extension uses the following Chrome APIs:
- chrome.scripting.insertCSS() - Injects the focus mode stylesheet when enabled
- chrome.scripting.removeCSS() - Removes the stylesheet when disabled
- chrome.action - Displays an "ON"/"OFF" badge indicating the current state

activeTab permission - Allows the extension to modify only the current tab

The focus mode can be toggled by:
- Clicking the extension icon
- Using the keyboard shortcut (Ctrl+B on Windows/Linux, Command+B on Mac)

The toggle state is maintained per-tab, allowing different tabs to have different focus mode states.