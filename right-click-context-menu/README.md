### this will give back the normal (windows 10) right click menu in windows 11

[google search: windows 11 right click menu]

[help page](https://pureinfotech.com/bring-back-classic-context-menu-windows-11/#:~:text=Enable%20classic%20right%2Dclick%20context%20menu%20on%20Windows%2011&text=Right%2Dclick%20the%20CLSID%20key,and%20select%20the%20Key%20option.])

1. Open Start on Windows 11.
2. Search for regedit and click the top result to open the Registry.
3. Navigate to the following path:
```
HKEY_CURRENT_USER\SOFTWARE\CLASSES\CLSID
```
4. Right-click the CLSID key, select the New menu, and select the Key option.
[![image1alttext](86ca1aa0-34aa-4e8b-a509-50c905bae2a2-regedit-2022.jpg?raw=true "image1")](#)
5. Name the key {86ca1aa0-34aa-4e8b-a509-50c905bae2a2} and press Enter.
6. Right-click the newly created key, select the New menu, and select the Key option.
[![image2alttext](InprocServer32-regedit-2022.jpg?raw=true "image2")](#)
7. Name the key InprocServer32 and press Enter.
8. Double-click the newly created key and set its value to blank to enable the classic context menu on Windows 11.
9. Click the OK button.
[![image3alttext](enable-classic-context-menu-windows-11.jpg?raw=true "image3")](#)
10. Restart the computer (important).
11. If you want to revert the changes to re-enable the modern context menu, you can follow the same instructions outlined above, but on step 4, right-click and delete the {86ca1aa0-34aa-4e8b-a509-50c905bae2a2} key and its contents.
12. Update November 25, 2022: Instructions have been received to ensure they still work.


