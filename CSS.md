# CSS

## View CSS style that I dig deep into to make CSS layout works

### 5 Different Position Values:
- Static:
* Default position of CSS value is static
* Fall where you expect it to flow in the document
- Relative: 
* It is similar to absolute positioning in that you can use top, bottom, left and right to scoot an object to a specific point on the page.
* Starting point will be relative to the flow of the document
* If we apply 20px top, then it will moved “relative to its starting position”
* Helpful when you want to slightly tweak an object position rather than completely reset it altogether.
* It also doesn’t care about other items
- Inherit:
* Inherit the value of its parent
- Fixed:
* Anchor the object to the background so whenever you placed it there, it will stay.
* Nav bar, when you scroll down it will be fixed an the user never loses site of the menu
- Absolute:
* It will placed into the position where you want it to be placed, regardless on whether there is other content occupying the position.
* When something has absolute positioning, it neither affects nor is affected by other elements in the normal flow of the page.
* The reason for absolute, is that we can position precisely this item where we want it, so we do this with the top, bottom, left and right CSS properties.
* Start point was at the very top left of the browser window. ( not really, instead , it position the element relative to its first non-statically-positioned ancestors, so inherit doesn’t count here)
* So we can translate into absolute positioning, but we have get the ancestors to position something that is not static ( relative), if the ancestor is absolute then it will still move
- In summary:
1. relative positioning will allow you to tweak an elements position relative to its normal starting point.
2. Absolute positioning will allow you t tweak an elements position relative to the first non-statically-positioned ancestor.
3. Both relatively and absolutely positioned items won’t affect the static and fixed items around them. 



## Float



