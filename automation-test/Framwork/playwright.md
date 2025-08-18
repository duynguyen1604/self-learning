
# Tìm hiểu về Playwright
Playwright là một framework kiểm thử tự động do Microsoft phát triển, dùng để tự động hóa các trình duyệt web như Chromium (Chrome, Edge), Firefox và WebKit (Safari).
## Đặc điểm nổi bật
| Đặc điểm                          | Mô tả                                                                 |
|----------------------------------|----------------------------------------------------------------------|
| **Đa trình duyệt**             | Hỗ trợ Chromium, Firefox, WebKit (Safari). Chạy được trên nhiều hệ điều hành. |
| **Hỗ trợ đa tab / đa page**    | Có thể mở và điều khiển nhiều tab hoặc trang cùng lúc.               |
| **Tích hợp sẵn headless mode** | Chạy không giao diện (headless) để tăng tốc độ kiểm thử.             |
| **Tốc độ cao, ổn định**        | Rất nhanh và ít flakey (không ổn định) hơn so với Selenium.          |
| **Hỗ trợ nhiều ngôn ngữ**      | Viết test bằng JavaScript, TypeScript, Python, C#, Java.             |
| **Tích hợp record & codegen**  | Ghi lại thao tác người dùng và tạo sẵn mã test (`codegen`).          |
| **Tự động chờ (auto-wait)**    | Tự động đợi phần tử sẵn sàng (hiển thị, click được...) trước khi thao tác. |
| **Hỗ trợ test API**            | Cho phép gửi và kiểm tra request/response như Postman.               |
| **Snapshot, Video, Screenshot**| Tích hợp ghi lại video, chụp ảnh để debug khi test fail.             |
| **Tích hợp CI/CD dễ dàng**     | Dùng tốt với GitHub Actions, GitLab CI, Jenkins,...                  |
| **Hỗ trợ testing trên mobile** | Có thể giả lập thiết bị di động như iPhone, Pixel,...                |
| **Báo cáo kết quả trực quan**  | Giao diện hiển thị report rất dễ đọc và phân tích lỗi.               |
## 1. Các cài đặt, khởi tạo, chạy và xem report của playwrightplaywright
**cài đặt Playwright**:
```bash
npm install -D @playwright/test
npx playwright install
```
**Khởi tạo project**:
```bash
npm init playwright@latest
```
### Chạy toàn bộ test
  ```bash
  npx playwright test
  ```

### Chạy 1 file cụ thể
  ```bash
  npx playwright test tests/example.spec.js
  ```
### xem report
```bash
npx playwright show-report
```

---
## 2. So sánh Playwright và Selenium

Dưới đây là **so sánh chi tiết giữa Playwright và Selenium** — hai framework test tự động phổ biến nhất hiện nay:

| Tiêu chí                 | Playwright                                  | Selenium                                   |
|--------------------------|---------------------------------------------|--------------------------------------------|
| **Ngôn ngữ hỗ trợ**       | JavaScript/TypeScript, Python, C#, Java     | Hỗ trợ rất nhiều: Java, C#, Python, Ruby, JS, PHP... |
| **Trình duyệt hỗ trợ**    | Chromium, Firefox, WebKit (Safari)           | Hầu hết trình duyệt phổ biến (Chrome, Firefox, Edge, Safari, IE...) |
| **Cơ chế điều khiển trình duyệt** | Giao tiếp trực tiếp với trình duyệt qua DevTools protocol, hỗ trợ tự động chờ (auto-wait), điều khiển đa trình duyệt tốt | Sử dụng WebDriver giao tiếp qua trình duyệt, có thể chậm và phức tạp hơn |
| **Tính năng tự động chờ (waiting)** | Tự động chờ các sự kiện DOM, AJAX, animation giúp giảm flaky test | Cần phải code thủ công hoặc dùng thư viện bên ngoài để handle chờ đợi |
| **Tốc độ thực thi**       | Nhanh hơn do giao tiếp trực tiếp và hỗ trợ chạy song song | Thường chậm hơn, giao tiếp qua WebDriver tốn thời gian hơn |
| **Setup & cấu hình**     | Dễ dàng, có CLI hỗ trợ, tích hợp tốt với nhiều ngôn ngữ | Phức tạp hơn, nhiều bước cấu hình, driver cần tải riêng (chromedriver, geckodriver...) |
| **Hỗ trợ test đa trình duyệt** | Hỗ trợ cả Chromium, Firefox, WebKit (Safari) với API đồng nhất | Hỗ trợ nhiều trình duyệt, nhưng cần driver riêng cho từng trình duyệt |
| **Hỗ trợ test mobile**   | Hỗ trợ giả lập WebKit cho iOS, có thể tích hợp test web mobile | Selenium có Appium để test mobile nhưng là tool riêng biệt |
| **Quay video & chụp ảnh màn hình** | Hỗ trợ ghi video test và screenshot tích hợp sẵn | Cần setup thủ công hoặc dùng tool bên ngoài |
| **Cộng đồng & độ phổ biến** | Mới hơn, cộng đồng đang phát triển nhanh | Rất lớn, lâu đời, nhiều tài liệu và plugin hỗ trợ |
| **Khả năng mở rộng**     | Hỗ trợ tốt với các CI/CD pipelines hiện đại, dễ tích hợp | Rất tốt, được dùng rộng rãi trong doanh nghiệp lớn |
| **Độ ổn định test (Flaky test)** | Ít flaky hơn nhờ tự động chờ và API hiện đại | Dễ bị flaky test nếu không xử lý chờ đợi tốt |

---
## 3.So sánh Framework vs Tool

| Tiêu chí              | Framework                                                  | Tool                                                        |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------|
| **Khái niệm**         | Là một **bộ khung** gồm nhiều thư viện, cấu trúc sẵn để phát triển hoặc kiểm thử | Là **công cụ đơn lẻ** hỗ trợ thực hiện một tác vụ cụ thể     |
| **Tính tổ chức**      | Có **cấu trúc rõ ràng**, quy định cách viết mã, tổ chức dự án | Không có cấu trúc cố định, dùng linh hoạt                    |
| **Tính mở rộng**      | Dễ dàng **mở rộng, tái sử dụng**, tích hợp CI/CD           | Thường giới hạn trong khả năng đã có                         |
| **Thành phần tích hợp** | Bao gồm **thư viện, công cụ hỗ trợ, định dạng test, cấu hình...** | Thường chỉ có một **chức năng chính** duy nhất               |
| **Ví dụ**             | Playwright, Selenium, Cypress, JUnit, TestNG            | Postman (test API), Chrome DevTools, JMeter (load test) |
---
## 4. Getting started with Playwright: 
#### A. Input 
- **Fill**: điền thẳng một đoạn text vào ô input 
```js
// Text input
await page.getByRole('textbox').fill('Peter');

// Date input
await page.getByLabel('Birth date').fill('2020-02-02');

// Time input
await page.getByLabel('Appointment time').fill('13:15');

// Local datetime input
await page.getByLabel('Local time').fill('2020-03-02T05:15');
```
---
#### B. Checkboxes and radio buttons 
- **Kiểm tra checkbox (check)**:
```js
await page.check('#checkbox-selector');
await page.check('#radio-selector');
```
- **Bỏ chọn checkbox (uncheck)**:
```js
await page.uncheck('#checkbox-selector');
```
- **Kiểm tra trạng thái**:
```js
const isChecked = await page.isChecked('#checkbox-selector');
console.log(isChecked); // true hoặc false
const isSelected = await page.isChecked('#radio-selector');
console.log(isSelected); // true hoặc false
```
---
#### C. Mouse click
- **click**:
```js
await page.getByRole('button').click();
```
- **Double click**:
```js
await page.getByText('Item').dblclick();
```
- **Right click**:
```js
await page.getByText('Item').click({ button: 'right' });
```
- **Shift + Click**:
```js
await page.getByText('Item').click({ modifiers: ['Shift'] });
```
- **Ctrl + Click**:
```js
await page.getByText('Item').click({ modifiers: ['ControlOrMeta'] });
```
- **Click the top left corner**:
```js
await page.getByText('Item').click({ position: { x: 0, y: 0 } });
```
---
#### D. Drag and Drop
- **dragTo()**:Playwright sẽ tự động:
    + Hover phần tử kéo,
    + Nhấn giữ chuột trái,
    + Di chuyển chuột đến phần tử thả,
    + Thả chuột.
```js
await page.locator('#item-to-be-dragged').dragTo(page.locator('#item-to-drop-at'));
```
- **Cách thủ công**:
```js
// Di chuột tới phần tử nguồn
await page.locator('#item-to-be-dragged').hover();
// Nhấn giữ chuột
await page.mouse.down();
// Di chuột tới phần tử đích
await page.locator('#item-to-drop-at').hover();
// Thả chuột
await page.mouse.up();
```
---
#### E. Upload files
- **Upload file bằng cách set input files trực tiếp (setInputFiles())**:
```js
const path = require('path');
// Upload 1 file
await page.getByLabel('Upload file').setInputFiles(path.join(__dirname, 'myfile.pdf'));
// Upload nhiều file
await page.getByLabel('Upload files').setInputFiles([
  path.join(__dirname, 'file1.txt'),
  path.join(__dirname, 'file2.txt'),
]);
// Upload thư mục (nếu input hỗ trợ)
await page.getByLabel('Upload directory').setInputFiles(path.join(__dirname, 'mydir'));
// Xóa file đã chọn
await page.getByLabel('Upload file').setInputFiles([]);
```
- **Upload file từ buffer trong bộ nhớ (không cần file vật lý)**:
```js
await page.getByLabel('Upload file').setInputFiles({
  name: 'file.txt',
  mimeType: 'text/plain',
  buffer: Buffer.from('this is test'),
});
```
- **Upload file khi input file được tạo động (file chooser popup)**:
  + Đợi sự kiện filechooser
  + Mở popup chọn file
  + Sau đó set file cho file chooser
```js
const fileChooserPromise = page.waitForEvent('filechooser');
await page.getByLabel('Upload file').click();  // Mở dialog chọn file
const fileChooser = await fileChooserPromise;
await fileChooser.setFiles(path.join(__dirname, 'myfile.pdf'));
```
#### Các Loại Test Hooks
+ `beforeAll`: Chạy một lần duy nhất trước khi tất cả các bài kiểm tra bắt đầu. Dùng để thiết lập trước tất cả các test.
+ `beforeEach`: Chạy trước mỗi bài kiểm tra trong một suite. Dùng để thiết lập trước mỗi test
+ `afterEach`: Chạy sau mỗi bài kiểm tra trong một suite. Dùng để kiểm tra sau mỗi test.
+ `afterAll`: Chạy một lần duy nhất sau khi tất cả các bài kiểm tra trong một suite đã được thực thi. Dùng để làm sạch sau tất cả các test.
##### Lợi Ích của Test Hooks:
1. Tái sử dụng mã: Bạn không cần phải viết lại các bước thiết lập và dọn dẹp trong mỗi test. Hooks giúp bạn tổ chức mã kiểm tra rõ ràng và giảm thiểu sự lặp lại.
2. Kiểm soát tốt hơn: Bạn có thể dễ dàng chuẩn bị môi trường, kiểm tra các điều kiện trước và sau mỗi test, từ đó đảm bảo tính chính xác và tính toàn vẹn của mỗi bài kiểm tra.
3. Dễ dàng duy trì: Nếu cần thay đổi cách thiết lập hoặc dọn dẹp môi trường, bạn chỉ cần chỉnh sửa một lần trong hooks thay vì mỗi bài kiểm tra riêng biệt.
Ví dụ:
```js
import { test, expect } from '@playwright/test';

let page;

test.beforeAll(async ({ browser }) => {
  // Mở trình duyệt và điều hướng đến trang đăng nhập
  page = await browser.newPage();
  await page.goto('https://example.com/login');
});

test.beforeEach(async () => {
  // Chắc chắn rằng trang đăng nhập luôn có sẵn trước mỗi test
  await page.reload();
});

test.afterEach(async () => {
  // Sau mỗi test, kiểm tra nếu có thông báo lỗi và làm sạch
  const errorMessages = await page.locator('.error-message').count();
  expect(errorMessages).toBe(0); // Đảm bảo không có lỗi
});

test.afterAll(async () => {
  // Đóng trình duyệt sau khi tất cả các test đã hoàn thành
  await page.close();
});

test('should log in successfully', async () => {
  // Thực hiện đăng nhập
  await page.fill('input[name="username"]', 'testuser');
  await page.fill('input[name="password"]', 'password123');
  await page.click('button[type="submit"]');

  // Kiểm tra nếu chuyển hướng đến trang dashboard
  await expect(page).toHaveURL('https://example.com/dashboard');
});

test('should show error for incorrect login', async () => {
  // Thực hiện đăng nhập với thông tin sai
  await page.fill('input[name="username"]', 'wronguser');
  await page.fill('input[name="password"]', 'wrongpassword');
  await page.click('button[type="submit"]');

  // Kiểm tra thông báo lỗi
  const errorMessage = await page.locator('.error-message').textContent();
  expect(errorMessage).toBe('Invalid username or password');
});
```
---
## 5. Assertions
Lời khuyên sử dụng
- Luôn ưu tiên dùng auto-retrying assertions khi kiểm tra trạng thái UI hoặc page.
- Khi cần kiểm tra giá trị hoặc logic thuần (không phụ thuộc trạng thái UI), dùng non-retrying assertion.
- Nếu cần retry với logic phức tạp, có thể dùng thêm:
  + expect.poll() — poll giá trị cho đến khi thỏa điều kiện. Dùng khi giá trị thay đổi theo thời gian.
```js
await expect.poll(async () => {
  return await page.locator('#status').textContent();
}).toBe('Success');
//Playwright sẽ lặp lại việc lấy giá trị và kiểm tra, cho đến khi điều kiện đúng (Success).
```
  + expect.toPass() — để retry custom assertion. Dùng khi kiểm tra nhiều bước, hoặc custom logic.
```js
await expect(async () => {
  const items = await page.locator('.item');
  expect(await items.count()).toBe(5); // số lượng item phải là 5
}).toPass();
//Hàm expect(() => {...}).toPass() sẽ thực hiện lại đoạn code trong callback nhiều lần cho đến khi tất cả các dòng kiểm tra đều thành công
```


#### A. Auto-retrying assertions
- Những lệnh assert này sẽ tự động lặp lại cho đến khi:
  + Assertion thành công, hoặc
  + Hết timeout (mặc định là 5 giây, có thể tùy chỉnh).
- Điều này rất hữu ích với UI test vì trang web thường load dữ liệu bất đồng bộ, trạng thái element có thể thay đổi sau vài giây.
- Luôn phải dùng await vì là async.
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
| `page.toHaveURL()`          | Page có URL chính xác                         | `await expect(page).toHaveURL('https://example.com/home');`     |
| `response.toBeOK()`         | HTTP response status 200-299                  | `await expect(response).toBeOK();`                              |
#### B. Non-Retrying Assertions
- Những assertion này không retry.
- Kiểm tra ngay lập tức và trả về kết quả.
- Dùng cho các kiểm tra giá trị tĩnh, không liên quan UI thay đổi theo thời gian.
- Dùng sai chỗ (vd kiểm tra UI bất đồng bộ) dễ dẫn đến test flaky.

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

## 6. Auto-waiting
- Là cơ chế tự động chờ đợi mà Playwright sử dụng để đảm bảo các thao tác trên trang web diễn ra khi phần tử sẵn sàng và trạng thái phù hợp, mà bạn không cần phải tự viết các đoạn code chờ (wait) phức tạp.
- Playwright sẽ tự động chờ đợi (auto-wait) các kiểm tra này thành công trong khoảng thời gian timeout (mặc định 5s).
- Nếu kiểm tra không thành công sau timeout, hành động sẽ bị lỗi TimeoutError.
### A. Các Kiểm Tra Đối Với Phần Tử
| **Kiểm tra**        | **Ý nghĩa**                                                                 |
|---------------------|------------------------------------------------------------------------------|
| **Visible**         | Phần tử phải hiển thị (không bị ẩn, có kích thước khác 0, không `display: none`) |
| **Stable**          | Phần tử không đang di chuyển hoặc chuyển động (bounding box giữ nguyên qua 2 frame) |
| **Receives Events** | Phần tử có thể nhận sự kiện (không bị che phủ bởi phần tử khác, là mục tiêu của sự kiện) |
| **Enabled**         | Phần tử không bị disable (không có thuộc tính `disabled` hoặc `aria-disabled=true`) |
| **Editable**        | Phần tử có thể chỉnh sửa (không `readonly`, không `disabled`)   

#### Bảng Điều Kiện Kiểm Tra Cho Các Hành Động `locator`

| **Action**                     | **Visible** | **Stable** | **Receives Events** | **Enabled** | **Editable** |
|--------------------------------|-------------|------------|----------------------|-------------|---------------|
| `locator.check()`              | Yes         | Yes        | Yes                  | Yes         | -             |
| `locator.click()`              | Yes         | Yes        | Yes                  | Yes         | -             |
| `locator.dblclick()`           | Yes         | Yes        | Yes                  | Yes         | -             |
| `locator.setChecked()`         | Yes         | Yes        | Yes                  | Yes         | -             |
| `locator.tap()`                | Yes         | Yes        | Yes                  | Yes         | -             |
| `locator.uncheck()`            | Yes         | Yes        | Yes                  | Yes         | -             |
| `locator.hover()`              | Yes         | Yes        | Yes                  | -           | -             |
| `locator.dragTo()`             | Yes         | Yes        | Yes                  | -           | -             |
| `locator.screenshot()`         | Yes         | Yes        | -                    | -           | -             |
| `locator.fill()`               | Yes         | -          | -                    | Yes         | Yes           |
| `locator.clear()`              | Yes         | -          | -                    | Yes         | Yes           |
| `locator.selectOption()`       | Yes         | -          | -                    | Yes         | -             |
| `locator.selectText()`         | Yes         | -          | -                    | -           | -             |
| `locator.scrollIntoViewIfNeeded()` | -       | Yes        | -                    | -           | -             |
| `locator.blur()`               | -           | -          | -                    | -           | -             |
| `locator.dispatchEvent()`      | -           | -          | -                    | -           | -             |
| `locator.focus()`              | -           | -          | -                    | -           | -             |
| `locator.press()`              | -           | -          | -                    | -           | -             |
| `locator.pressSequentially()`  | -           | -          | -                    | -           | -             |
| `locator.setInputFiles()`      | -           | -          | -                    | -           | -             |

### B. Force Option
+ Một số action (ví dụ: locator.click({ force: true })) cho phép bỏ qua một số kiểm tra không cần thiết, dùng khi bạn chắc chắn muốn thao tác bất chấp trạng thái phần tử (ví dụ ẩn, không nhận sự kiện,...).
### C. Auto-Retrying Assertions

| **Assertion**                             | **Ý nghĩa**                             |
|------------------------------------------|------------------------------------------------------|
| `expect(locator).toBeAttached()`         | Phần tử đã được gắn vào DOM                          |
| `expect(locator).toBeChecked()`          | Checkbox được chọn                                   |
| `expect(locator).toBeDisabled()`         | Phần tử bị vô hiệu hóa                               |
| `expect(locator).toBeEditable()`         | Phần tử có thể chỉnh sửa                             |
| `expect(locator).toBeEmpty()`            | Phần tử (container) rỗng                             |
| `expect(locator).toBeEnabled()`          | Phần tử được kích hoạt                               |
| `expect(locator).toBeFocused()`          | Phần tử đang được focus                              |
| `expect(locator).toBeHidden()`           | Phần tử không hiển thị (ẩn)                          |
| `expect(locator).toBeInViewport()`       | Phần tử nằm trong vùng nhìn thấy (viewport)          |
| `expect(locator).toBeVisible()`          | Phần tử hiển thị trên giao diện                      |
| `expect(locator).toContainText()`        | Phần tử chứa đoạn văn bản xác định                   |
| `expect(locator).toHaveAttribute()`      | Phần tử có thuộc tính DOM xác định                   |
| `expect(locator).toHaveClass()`          | Phần tử có class tương ứng                           |
| `expect(locator).toHaveCount()`          | Danh sách có số phần tử con đúng                     |
| `expect(locator).toHaveCSS()`            | Phần tử có thuộc tính CSS xác định                   |
| `expect(locator).toHaveId()`             | Phần tử có thuộc tính ID xác định                    |
| `expect(locator).toHaveJSProperty()`     | Phần tử có thuộc tính JavaScript                     |
| `expect(locator).toHaveText()`           | Phần tử có nội dung văn bản chính xác                |
| `expect(locator).toHaveValue()`          | Input có giá trị xác định                            |
| `expect(locator).toHaveValues()`         | Select có các option được chọn                       |
| `expect(page).toHaveTitle()`             | Trang có tiêu đề xác định                            |
| `expect(page).toHaveURL()`               | Trang có URL xác định                                |
| `expect(response).toBeOK()`              | Phản hồi có trạng thái thành công (200–299)          |
### D. Visible 
- Phần tử được xem là visible nếu:
  - Có bounding box không rỗng (kích thước khác 0)
  - Không có display:none
- Lưu ý:
  - Phần tử có opacity 0 vẫn được xem là visible
  - Phần tử kích thước 0 không được xem là visible
### E. Enabled
Phần tử được xem là enabled nếu:
  - Không có thuộc tính disabled trên các thẻ `<button>, <input>, <select>, <textarea>,...`
  - Không thuộc nhóm bị disable bởi `<fieldset disabled>`
  - Không có aria-disabled="true" trên hoặc trên tổ tiên
### F. Editable
- Phần tử là editable khi:
  - Được enable
  - Không có thuộc tính readonly hoặc aria-readonly="true"
### G. Stable
- Element được xem là "stable" (ổn định) khi:
  - Kích thước và vị trí của nó (bounding box) không thay đổi qua ít nhất hai frame liên tiếp của animation hoặc render.
## 7. Data Driven Test

Tạo test chạy với nhiều dữ liệu khác nhau:

```js
const testData = [
  { input: 'Playwright', expected: 'Playwright' },
  { input: 'Testing', expected: 'Testing' }
];

for (const data of testData) {
  test(`searching for ${data.input}`, async ({ page }) => {
    await page.goto('https://google.com');
    await page.fill('input[name=q]', data.input);
    await page.press('input[name=q]', 'Enter');
    await expect(page).toHaveTitle(new RegExp(data.expected));
  });
}
```
---
## 8. Tổ chức code với POM (Page Object Model), Visual Testing

### POM là gì?

Tách biệt thao tác và locator thành class riêng để dễ bảo trì.

**Ví dụ**:

```js
// pageObjects/HomePage.js
class HomePage {
  constructor(page) {
    this.page = page;
    this.searchInput = page.locator('input[name=q]');
    this.searchButton = page.locator('input[type=submit]');
  }

  async goto() {
    await this.page.goto('https://google.com');
  }

  async search(text) {
    await this.searchInput.fill(text);
    await this.searchButton.click();
  }
}

module.exports = { HomePage };
```

**Trong test**:

```js
const { HomePage } = require('./pageObjects/HomePage');

test('search test', async ({ page }) => {
  const home = new HomePage(page);
  await home.goto();
  await home.search('Playwright');
});
```

### Visual Testing

Chụp ảnh màn hình và so sánh ảnh:

```js
await expect(page).toHaveScreenshot('homepage.png');
```

So sánh ảnh để phát hiện thay đổi giao diện.

---

## 9. Configuration nâng cao, Test Generator

### Configuration nâng cao

Cấu hình `playwright.config.js`:

```js
module.exports = {
  timeout: 30000,
  use: {
    headless: true,
    viewport: { width: 1280, height: 720 },
  },
  projects: [
    { name: 'chromium', use: { browserName: 'chromium' } },
    { name: 'firefox', use: { browserName: 'firefox' } },
  ],
};
```

### Test Generator (Record Test)

Ghi lại thao tác người dùng thành mã test:

```bash
npx playwright codegen https://example.com
```

Giao diện sẽ ghi thao tác và xuất script ở định dạng JS hoặc Python.

---

## 10. API Testing với Playwright

Playwright hỗ trợ gửi request API.

**Ví dụ test API**:

```js
const { test, expect, request } = require('@playwright/test');

test('API test example', async () => {
  const apiContext = await request.newContext();
  const response = await apiContext.get('https://api.example.com/users/1');
  expect(response.status()).toBe(200);

  const data = await response.json();
  expect(data.id).toBe(1);
});
```

Có thể gửi request các phương thức: GET, POST, PUT, DELETE.

Hỗ trợ quản lý headers, cookies và kết hợp UI với API test.

---
