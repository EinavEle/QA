To follow our guidelines of hybrid testing, meaning combining API calls with UI actions and validations, we have provided you with example code that shows how we can transfer the session from the APIto the UI.
This code is a simple script and does not follow the guidelines of correct architecture, encapsulation, separations of concerns and many other things.
You should not use this code in your project as is but use it to understand the process and implement on your own.

In the example you can see how the user 'Assaf' is logged in via API.
When we start a new browser context we transfer the storage state from the API.
Then when we navigate to the site we validate that 'Assaf' is logged in.
We've also made an API call to add an item to the wishlist and we can see it in the UI.

```
test("has title", async ({ browser, request }) => {
  const res = await request.post(
    "https://www.terminalx.com/pg/MutationUserLogin",
    {
      data: {
        username: "assaf@assaf.com",
        password: "A$$@f123",
      },
    }
  );
  const state = await request.storageState();
  await request.post(
    "https://www.terminalx.com/pg/MutationAddProductsToWishlist",
    {
      data: { sku: ["Z755900001"], attributes: ["93"], values: ["4"] },
    }
  );
  const context = await browser.newContext({ storageState: state });
  const page = await context.newPage();
  await page.goto("https://www.terminalx.com/");
  await expect(page.locator("//button//span[text()='assaf']")).toBeVisible();
});
});
```
