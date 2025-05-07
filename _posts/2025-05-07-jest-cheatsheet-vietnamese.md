---
title: "Jest Unit Test Cheat Sheet (Tiếng Việt)"
toc: true
toc_label: "Table of Content"
toc_icon: "heart"  # corresponding Font Awesome icon name (without fa prefix)
categories:
  - Technical
tags:
  - jest
  - unit test
---

## 1. Thiết lập và dọn dẹp test

```js
beforeAll(() => { /* chạy 1 lần trước tất cả các test */ });
afterAll(() => { /* chạy 1 lần sau tất cả các test */ });
beforeEach(() => { /* chạy trước mỗi test */ });
afterEach(() => { /* chạy sau mỗi test */ });
```

---

## 2. Cú pháp test cơ bản

```js
test('mô tả test', () => {
  expect(giá_trị_thực_tế).toBe(giá_trị_mong_đợi);
});

it('cũng giống như test', () => {
  expect(true).toBe(true);
});
```

---

## 3. Các matchers thường dùng

### So sánh giá trị

```js
expect(1 + 1).toBe(2);
expect(value).not.toBe(null);
```

### So sánh object hoặc mảng

```js
expect(obj).toEqual({ a: 1 });
```

### Kiểm tra giá trị đặc biệt

```js
expect(value).toBeNull();
expect(value).toBeDefined();
expect(value).toBeTruthy();
expect(value).toBeFalsy();
```

### So sánh số

```js
expect(num).toBeGreaterThan(5);
expect(num).toBeLessThanOrEqual(10);
```

### Chuỗi

```js
expect(str).toMatch(/regex/);
```

### Mảng

```js
expect(arr).toContain('item');
expect(arr).toHaveLength(3);
```

---

## 4. Hàm mock (giả lập)

```js
const mockFn = jest.fn();
mockFn('arg1');
expect(mockFn).toHaveBeenCalled();
expect(mockFn).toHaveBeenCalledWith('arg1');

mockFn.mockReturnValue('giá trị');
mockFn.mockResolvedValue('giá trị async');
mockFn.mockRejectedValue(new Error('lỗi'));
```

---

## 5. Spy hàm thật

```js
const obj = {
  method: () => 'real',
};

jest.spyOn(obj, 'method');
obj.method();
expect(obj.method).toHaveBeenCalled();
```

---

## 6. Giả lập module

```js
jest.mock('./module');
const module = require('./module');
module.someFunc.mockReturnValue('mocked');
```

---

## 7. Test async/await

```js
test('dùng async/await', async () => {
  const data = await fetchData();
  expect(data).toBeDefined();
});

test('Promise resolve', () => {
  return expect(fetchData()).resolves.toEqual('kết quả');
});

test('Promise reject', () => {
  return expect(fetchData()).rejects.toThrow('lỗi');
});
```

---

## 8. Giả lập thời gian (Timers)

```js
jest.useFakeTimers();
jest.advanceTimersByTime(1000);
jest.runAllTimers();
```
