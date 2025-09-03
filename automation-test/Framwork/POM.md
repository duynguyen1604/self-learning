# Page Object Model (POM) với Playwright

## 1. Page Object Model là gì?
- Khi test một ứng dụng web, thường có rất nhiều **selector** và **hành động** lặp lại.  
- Nếu viết thẳng trong file test, code sẽ dài và khó bảo trì.  
- **Page Object Model (POM)** là cách gom các selector và hành động của **một trang web** vào trong **một class riêng**.  

👉 Lợi ích:  
- Dễ bảo trì: thay đổi selector 1 lần trong Page Object là áp dụng cho toàn bộ test.  
- Dễ tái sử dụng: có thể gọi lại các hàm (method) nhiều lần ở nhiều test khác nhau.  
- Test ngắn gọn, dễ đọc.

Ví dụ:  
- Trang **LoginPage** chứa các nút nhập username, password, nút Login.  
- Trang **CartPage** chứa các nút Add to cart, Remove, Checkout.  

---

## 2. Cách dùng POM hiệu quả
1. **Một class cho một trang**  
   Ví dụ: `LoginPage.ts`, `HomePage.ts`, `CartPage.ts`.

2. **Đặt tên method theo hành động thực tế**  
   - `login(username, password)`  
   - `addProductToCart(productName)`  
   - `checkout()`  

3. **Tách biệt thao tác và kiểm tra (assertion)**  
   - File Page Object: chỉ chứa thao tác (click, nhập liệu, mở trang).  
   - File test: chứa `expect(...)` để kiểm tra kết quả.  

---
## 3. Kế Thừa (Extend) trong POM

Trong mô hình Page Object Model, chúng ta có thể sử dụng **kế thừa
(extends)** để tái sử dụng code giữa các trang.\
Ví dụ: Tất cả các trang trong hệ thống đều có **header**, **footer**,
hoặc **menu điều hướng** giống nhau.\
Thay vì viết lại nhiều lần, ta có thể tạo **BasePage** để chứa các thành
phần và hàm dùng chung.

---

## 4. Ví dụ: BasePage

``` typescript
// basePage.ts
import { Page, Locator } from '@playwright/test';

export class BasePage {
  readonly page: Page;
  readonly header: Locator;
  readonly footer: Locator;

  constructor(page: Page) {
    this.page = page;
    this.header = page.locator('header');
    this.footer = page.locator('footer');
  }

  async goto(url: string) {
    await this.page.goto(url);
  }

  async getHeaderText() {
    return await this.header.textContent();
  }
}
```

---

## 5. Trang con kế thừa BasePage

``` typescript
// loginPage.ts
import { BasePage } from './basePage';

export class LoginPage extends BasePage {
  readonly usernameInput = this.page.locator('#username');
  readonly passwordInput = this.page.locator('#password');
  readonly loginButton = this.page.locator('#login');

  constructor(page) {
    super(page);
  }

  async login(username: string, password: string) {
    await this.usernameInput.fill(username);
    await this.passwordInput.fill(password);
    await this.loginButton.click();
  }
}
```

---

## 6. Sử dụng trong Test

``` typescript
import { test, expect } from '@playwright/test';
import { LoginPage } from '../pages/loginPage';

test('Đăng nhập thành công', async ({ page }) => {
  const loginPage = new LoginPage(page);
  await loginPage.goto('https://login');
  await loginPage.login('admin', '123456');

  expect(await loginPage.getHeaderText()).toContain('Welcome');
});
```

---
