# Assertions
- Playwright bao gồm các khẳng định kiểm tra dưới dạng expect hàm.
- Luôn ưu tiên dùng auto-retrying assertions khi kiểm tra trạng thái UI hoặc page.
- Khi cần kiểm tra giá trị hoặc logic thuần (không phụ thuộc trạng thái UI), dùng non-retrying assertion.

#### A. Auto-retrying assertions
- Những lệnh assert này sẽ tự động lặp lại cho đến khi:
  + Assertion thành công hoặc hết timeout (mặc định là 5 giây).
- Điều này rất hữu ích với UI test vì trang web thường load dữ liệu bất đồng bộ, trạng thái element có thể thay đổi sau vài giây.
Lợi ích:
  + Giảm tình trạng test flakiness (thỉnh thoảng fail do đợi không đủ lâu).
  + Không cần tự viết vòng lặp chờ, Playwright xử lý giúp.

| **Assertion**                | **Mô tả**                                      | **Ví dụ**                              |
|-----------------------------|-----------------------------------------------|-----------------------------------------------------------------|
| `toBeAttached()`            | Phần tử có trong DOM                          | `await expect(locator).toBeAttached();`                         |
| `toBeChecked()`             | Checkbox hoặc radio button được check         | `await expect(locator).toBeChecked();`                          |
| `toBeDisabled()`            | Phần tử bị disable                            | `await expect(locator).toBeDisabled();`                         |
| `toBeEditable()`            | Phần tử có thể chỉnh sửa được (input)         | `await expect(locator).toBeEditable();`                         |
| `toBeEmpty()`               | Container không có phần tử con                | `await expect(locator).toBeEmpty();`                            |
| `toBeEnabled()`             | Phần tử được enable                           | `await expect(locator).toBeEnabled();`                          |
| `toBeFocused()`             | Phần tử đang được focus                       | `await expect(locator).toBeFocused();`                          |
| `toBeHidden()`              | Phần tử không hiển thị (ẩn)                   | `await expect(locator).toBeHidden();`                           |
| `toBeInViewport()`          | Phần tử trong vùng nhìn thấy (viewport)       | `await expect(locator).toBeInViewport();`                       |
| `toBeVisible()`             | Phần tử hiển thị trên page                    | `await expect(locator).toBeVisible();`                          |
| `toContainText()`           | Phần tử chứa đoạn text                        | `await expect(locator).toContainText('Welcome');`               |
| `toHaveAttribute()`         | Phần tử có attribute xác định                 | `await expect(locator).toHaveAttribute('href', '/home');`       |
| `toHaveClass()`             | Phần tử có class xác định                     | `await expect(locator).toHaveClass(/active/);`                  |
| `toHaveCount()`             | List có số phần tử đúng                       | `await expect(locator).toHaveCount(5);`                         |
| `toHaveCSS()`               | Phần tử có style CSS xác định                 | `await expect(locator).toHaveCSS('display', 'block');`          |
| `toHaveId()`                | Phần tử có id xác định                        | `await expect(locator).toHaveId('submit-button');`              |
| `toHaveJSProperty()`        | Phần tử có thuộc tính JS                      | `await expect(locator).toHaveJSProperty('value', '123');`       |
| `toHaveRole()`              | Phần tử có role ARIA                          | `await expect(locator).toHaveRole('button');`                   |
| `toHaveScreenshot()`        | Phần tử khớp ảnh chụp màn hình                | `await expect(locator).toHaveScreenshot('button.png');`         |
| `toHaveText()`              | Phần tử có đoạn text đúng                     | `await expect(locator).toHaveText('Submit');`                   |
| `toHaveValue()`             | Input có giá trị xác định                     | `await expect(locator).toHaveValue('John Doe');`                |
| `toHaveValues()`            | Select có các option được chọn                | `await expect(locator).toHaveValues(['option1', 'option2']);`   |
| `page.toHaveScreenshot()`   | Page khớp ảnh chụp màn hình                   | `await expect(page).toHaveScreenshot('homepage.png');`          |
| `page.toHaveTitle()`        | Page có title chính xác                       | `await expect(page).toHaveTitle('Dashboard');`                  |
| `page.toHaveURL()`          | Page có URL chính xác                         | `await expect(page).toHaveURL('');`     |
| `response.toBeOK()`         | HTTP response status 200-299                  | `await expect(response).toBeOK();`                              |
#### B. Non-Retrying Assertions
- Những assertion này không retry.
- Kiểm tra ngay lập tức và trả về kết quả.
- Dùng cho các kiểm tra giá trị tĩnh, không liên quan UI thay đổi theo thời gian.
- Dùng sai chỗ dễ dẫn đến test flaky.

| **Assertion**                        | **Mô tả**                                 | **Ví dụ**                                  |
|-------------------------------------|-------------------------------------------|----------------------------------------------------------|
| `toBe()`                            | Giá trị bằng nhau                         | `expect(value).toBe(42);`                               |
| `toBeCloseTo()`                     | Giá trị số gần đúng                       | `expect(value).toBeCloseTo(3.14, 2);`                    |
| `toBeDefined()`                     | Giá trị không undefined                   | `expect(value).toBeDefined();`                           |
| `toBeFalsy()`                       | Giá trị falsy (`false`, `0`, `null`...)   | `expect(value).toBeFalsy();`                             |
| `toBeGreaterThan()`                | Giá trị lớn hơn                           | `expect(value).toBeGreaterThan(10);`                     |
| `toBeGreaterThanOrEqual()`         | Giá trị lớn hơn hoặc bằng                 | `expect(value).toBeGreaterThanOrEqual(10);`              |
| `toBeInstanceOf()`                  | Là instance của class                     | `expect(value).toBeInstanceOf(MyClass);`                 |
| `toBeLessThan()`                    | Giá trị nhỏ hơn                           | `expect(value).toBeLessThan(20);`                        |
| `toBeLessThanOrEqual()`            | Giá trị nhỏ hơn hoặc bằng                 | `expect(value).toBeLessThanOrEqual(20);`                 |
| `toBeNaN()`                         | Giá trị là `NaN`                          | `expect(value).toBeNaN();`                               |
| `toBeNull()`                        | Giá trị là `null`                         | `expect(value).toBeNull();`                              |
| `toBeTruthy()`                      | Giá trị truthy                            | `expect(value).toBeTruthy();`                            |
| `toBeUndefined()`                   | Giá trị `undefined`                       | `expect(value).toBeUndefined();`                         |
| `toContain()`                       | Chuỗi hoặc mảng chứa phần tử              | `expect(array).toContain('item');`                       |
| `toContainEqual()`                  | Mảng chứa phần tử tương tự                | `expect(array).toContainEqual({ id: 1 });`               |
| `toEqual()`                         | So sánh deep equality                     | `expect(obj).toEqual({ a: 1, b: 2 });`                   |
| `toHaveLength()`                    | Mảng hoặc chuỗi có độ dài                 | `expect(array).toHaveLength(3);`                         |
| `toHaveProperty()`                  | Object có property                        | `expect(obj).toHaveProperty('name');`                    |
| `toMatch()`                         | Chuỗi khớp regex                          | `expect(str).toMatch(/hello/i);`                         |
| `toMatchObject()`                   | Object chứa các property xác định         | `expect(obj).toMatchObject({ a: 1 });`                   |
| `toStrictEqual()`                   | So sánh chính xác cả kiểu dữ liệu         | `expect(obj).toStrictEqual({ a: 1 });`                   |
| `toThrow()`                         | Hàm ném lỗi                               | `expect(() => func()).toThrow();`                        |
| `any()`                             | Khớp mọi kiểu dữ liệu                     | `expect(value).any(Number);`                             |
| `anything()`                        | Khớp mọi giá trị                          | `expect(value).anything();`                              |
| `arrayContaining()`                 | Mảng chứa phần tử cụ thể                  | `expect(array).arrayContaining(['foo']);`                |
| `closeTo()`                         | Số gần đúng                                | `expect(value).closeTo(3.14, 2);`                         |
| `objectContaining()`               | Object chứa property xác định             | `expect(obj).objectContaining({ a: 1 });`                |
| `stringContaining()`               | Chuỗi chứa substring                      | `expect(str).stringContaining('hello');`                 |
| `stringMatching()`                 | Chuỗi khớp regex                          | `expect(str).stringMatching(/hello/i);`                  |