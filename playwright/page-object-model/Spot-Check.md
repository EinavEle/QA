Write a full test for flowing page:
https://the-internet.herokuapp.com/key_presses

Do it with spec and POM

<details><summary>  
Click here to reveal the answer.  
</summary>

 
```Playwright 
test('spot check 2', async ({page}) => {
        await page.goto('https://the-internet.herokuapp.com/key_presses')
        const keyPressesPage = new KeyPressesPage(page)
        const randomChar = getRandomUpperCaseChar()
        await keyPressesPage.pressCharToTextInput(randomChar)
        expect(await keyPressesPage.getTextFromResult()).
                                            toBe('You entered: ' + randomChar)
    })
```

```Playwright
import { Locator, Page } from "@playwright/test";
import { BasePage } from "./base-page";

export class KeyPressesPage extends BasePage {
    private textInput: Locator
    private result: Locator

    constructor(page: Page) {
        super(page)
        this.textInput = page.locator('//input[@id="target"]')
        this.result = page.locator('//p[@id="result"]')
    }

    pressCharToTextInput = async (char: string) => {
        await this.textInput.press(char)
    }
    getTextFromResult = async () => {
        return await this.result.innerText()
    }
}
```

</details>