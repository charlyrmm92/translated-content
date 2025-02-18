---
title: FileSystemHandle：requestPermission() 方法
slug: Web/API/FileSystemHandle/requestPermission
---

{{securecontext_header}}{{APIRef("File System Access API")}}{{SeeCompatTable}}

{{domxref("FileSystemHandle")}} 接口的 **`queryPermission()`** 方法用于为文件句柄请求读取或读写权限。

## 语法

```js-nolint
requestPermission(fileSystemHandlePermissionDescriptor)
```

### 参数

- FileSystemHandlePermissionDescriptor {{optional_inline}}

  - : 一个对象，指定需要查询的权限模式，包含以下选项：

    - `'mode'`：可以是 `'read'` 或 `'readwrite'`。

### 返回值

{{domxref('PermissionStatus.state')}}，值为 `'granted'`、`'denied'` 或 `'prompt'` 三者之一。

### 异常

- {{jsxref("TypeError")}}
  - : 如果没有指定参数或者 `mode` 的值不是 `'read'` 或 `'readwrite'`，则抛出此异常。

## 示例

以下异步函数会在句柄没有获得授权时请求权限。

```js
// fileHandle 是一个 FileSystemFileHandle
// withWrite 是一个布尔值，如果要求写入则需传入 true

async function verifyPermission(fileHandle, withWrite) {
  const opts = {};
  if (withWrite) {
    opts.mode = "readwrite";
  }

  // 检查是否已经拥有相应权限，如果是，返回 true。
  if ((await fileHandle.queryPermission(opts)) === "granted") {
    return true;
  }

  // 为文件请求权限，如果用户授予了权限，返回 true。
  if ((await fileHandle.requestPermission(opts)) === "granted") {
    return true;
  }

  // 用户没有授权，返回 false。
  return false;
}
```

## 规范

{{Specifications}}

## 浏览器兼容性

{{Compat}}

## 参见

- [文件系统访问 API](/zh-CN/docs/Web/API/File_System_Access_API)
- [文件系统访问 API：简化本地文件访问](https://web.dev/file-system-access/)
