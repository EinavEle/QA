# When to use
Here too, as we learned in Selenium, a keyboard and mouse are used during tests and this is in order to:
- Mimic user behavior more accurately for testing
- Simulate custom JavaScript event listeners
- Access certain elements that require specific actions
- Enhance test coverage by testing a wider range of scenarios

But even here we will always prefer to use the actions of Playwright than to use a keyboard and mouse

# How to use
Here example for using in mouse:
```Playwright
   test(`using mouse and keyboard`, async ({page}) => {
        // Navigate to the page with the drag and drop element
        await page.goto('https://the-internet.herokuapp.com/drag_and_drop');
        // Locate the source and target elements
        const source = await page.locator('//div[@id="column-a"]');
        const target = await page.locator('//div[@id="column-b"]');
        // Get the bounding boxes of the elements
        const sourceBox = await source.boundingBox();
        const targetBox = await target.boundingBox();
        // Drag the source element to the target element
        await page.mouse.move(sourceBox!.x + sourceBox!.width / 2,
                              sourceBox!.y + sourceBox!.height / 2);
        await page.mouse.down();
        await page.mouse.move(targetBox!.x + targetBox!.width / 2,
                              targetBox!.y + targetBox!.height / 2);
        await page.mouse.up();
    })
```

In this example, we use the mouse.move() method to move the mouse cursor to the center of the source element, then call mouse.down() to start the drag operation.
We then use mouse.move() again to move the mouse to the center of the target element and call mouse.up() to complete the drag operation.
