# WindPress – Cached-CSS Bug Reproduction

This repository holds a **WordPress Playground export** that demonstrates a bug in WindPress:  
> When “Enable Cached CSS” is on, the generator drops arbitrary-variant selectors (e.g. `content-['PREV\20NEWS']`), breaking the Previous / Next post navigation and other blocks.

---

## Get the demo site running

### Import in the browser (Playground UI)

1. Download wordpress-playground-windpress-bug.zip.
2. Visit <https://playground.wordpress.net>.  
3. Click ⋮ Menu → Import from .zip.
4. Login as admin ⋮ My account → Username: admin | Password: password.
5. Go to the Homepage and click on a post ⋮ Homepage → Test Post 1.
6. Click on the next/previous post navigation buttons and notice the flash of styling on each page reload (this is happening because WindPress is currently using the compiler).
7. Go to WindPress settings and toggle on "Enable Cached CSS" & click the Generate button > save.
8. Go to WindPress settings and toggle on "Enable Cached CSS" > Save.
9. Now go back to view the custom post navigation buttons (they will look broken - this is the bug - WindPress is failing to generate the final css for these styles).
10. In WindPress > Files > tailwind.config.js you will find our original tailwind config file used but with the safelist classes commented out. Uncomment the "Cart Icon Badge", "Categories", "Post-navigation (PREV)" and "Post-navigation (NEXT)" safelist classes then click the save button.
11. Go back to WindPress Settings > Performance > Generate the cached CSS > click on the "Generate" button again and hit Save (you should now see the cached CSS file increase).
12. Now go back to view the custom post navigation buttons, category label and cart icon badge (they should now be displaying their original styling). However, ideally WindPress should be able to parse these classes correctly so the final css it produces is correct without having to resort to using the safelist (this is what needs to be fixed).
