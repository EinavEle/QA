# What is auto waiting in Playwright?
Before taking actions, Playwright checks if the elements are ready to perform the requested action. It waits until all necessary checks pass, and if the timeout expires before the checks pass, Playwright throws a TimeoutError.

For example, for page.locator().click(), Playwright will ensure that:
- element is Attached to the DOM
- element is Visible
- element is Stable, as in not animating or completed animation
- element Receives Events, as in not obscured by other elements
- element is Enabled
