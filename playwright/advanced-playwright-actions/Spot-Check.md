Create a GET,POST,PUT test for next API service:
https://reqres.in/

<details><summary>  
Click here to reveal the answer.  
</summary>

 
```Playwright 
import { test, expect } from '@playwright/test'

test.describe('spot check', () => {

    test('GET', async ({ request }) => {
        const newGet = await request.get('https://reqres.in/api/users/8')
        const body = await newGet.json()
     expect(body.data['avatar'])
                     .toContain('https://reqres.in/img/faces/8-image.jpg')
        expect(body.data['email']).toContain('lindsay.ferguson@reqres.in')
        expect(body.data['first_name']).toContain('Lindsay')
        expect(body.data['last_name']).toContain('Ferguson')
        expect(newGet.ok()).toBeTruthy()
    })
    test(`POST`, async ({ request }) => {
        const newPost = await request.post('https://reqres.in/api/users', {
            data: {
                "name": "Tzahi Anidgar",
                "job": "leader"
            }
        })
        expect(newPost.ok()).toBeTruthy()
    })
    test(`PUT`, async ({ request }) => {
        const newPost = await request.put('https://reqres.in/api/users/2', {
            data: {
                "name": "Ash Ketchum",
                "job": "Pokemon Trainer"
            }
        })
        expect(newPost.ok()).toBeTruthy()
    })
})
```
</details>