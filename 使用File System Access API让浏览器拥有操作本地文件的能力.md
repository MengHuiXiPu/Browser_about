# 使用File System Access API让浏览器拥有操作本地文件的能力

## 什么是 File System Access API

`File System Access API` 是一项 `Web API`，允许 `Web` 应用程序从用户设备的本地文件系统中读取和写入文件。

它提供了一种简单且安全的方法，让用户在不离开 `Web` 应用的情况下，从本地文件系统中操作文件。

这项 `API` 为 `Web` 应用程序提供了更多的灵活性和功能，使其更接近于本地应用程序的体验。

`File System Access API` 遵循同源策略，只允许 `Web` 应用程序在具有相同源的文件系统上进行操作。

当用户使用该 `API` 时，会提示用户授权应用程序访问他们的文件系统。

如果用户授权，则应用程序可以使用该 `API` 访问用户选择的文件和目录。

使用 `File System Access API` 可以访问本地文件系统，从而实现一些有用的功能，例如：

- 将文件从本地文件系统上传到 `Web` 应用程序；
- 将 `Web` 应用程序中的数据写入到本地文件系统中；
- 在用户的本地文件系统上创建、重命名和删除文件；
- 读取本地文件系统上的文件内容。

## 如何使用 File System Access API

我不是很喜欢概念性的东西，上面的内容是网上借鉴的（文化人），我更喜欢直接上代码，所以我们直接上代码。

### 选择文件

首先我们来看看如何选择文件，这个功能是 `File System Access API` 中最基础的功能，我们可以通过 `showOpenFilePicker` 方法来实现。

```
const fileHandle = await window.showOpenFilePicker();
console.log(fileHandle);
复制代码
```

可以看到我们这里使用了`async/await`语法，这是因为`showOpenFilePicker`异步方法，它会返回一个`Promise`对象，我们可以通过`await`来等待它的结果。

`showOpenFilePicker`方法会返回一个`FileHandle`对象，我们可以通过它来获取文件的信息。

我们来看看它最后返回的结果：

![图片](https://mmbiz.qpic.cn/mmbiz/bwG40XYiaOKna8LkgGSaJotSLmvWIlZFsicGGTayWiawD1scIfE8byPSWvkAnUaDaEbwNokUk5LcksamNtuCLR73Q/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)image.png

可以看到的是最后的结果是一个数组，这是因为我们可以选择多个文件；

而这个数组的每一项都是一个`FileSystemFileHandle`对象，我们可以通过它来获取和操作文件。

#### FileSystemFileHandle

`FileSystemFileHandle`对象是一个代表文件的对象，它提供了一些方法来获取和操作文件。

`FileSystemFileHandle`提供了一些方法来获取和操作文件，例如：

- `getFile`：返回一个`Promise`对象，用于获取文件；
- `createSyncAccessHandle`：返回一个`FileSystemSyncAccessHandle`对象，用于同步访问文件；
- `createWritable`：返回一个`Promise`对象，用于创建一个可写流，用于写入文件；

我们来看看如何使用`getFile`方法来获取文件。

```
const fileHandle = await window.showOpenFilePicker();
const file = await fileHandle[0].getFile();
console.log(file);
复制代码
```

![图片](https://mmbiz.qpic.cn/mmbiz/bwG40XYiaOKna8LkgGSaJotSLmvWIlZFsZngN7VBCwjnAItB6vaqzYiaXdeibHoJnfHgtS1mG8LZKABQ4bPTkGMOw/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)image.png

可以看到，我们通过`getFile`方法获取到了文件，它返回的是一个`File`对象，我们可以通过它来获取文件的信息。

都拿到`File`对象了，后面怎么操作就很熟悉了吧，直接使用`FileReader`对象来获取文件内容，后面你爱怎么操作就怎么操作。

#### FileSystemHandle

通过截图我们还看到了有`kind`属性和`name`属性，这两个属性是继承自`FileSystemHandle`对象的。

`FileSystemFileHandle`继承自`FileSystemHandle`，它是一个代表文件系统中的文件或目录的对象。

`FileSystemHandle`提供了一些方法来获取和操作文件系统中的文件或目录，例如：

- `kind`：返回一个字符串，用于表示文件或目录；
- `name`：返回一个字符串，用于表示文件或目录的名称；
- `isSameEntry`：返回一个`boolean`值，用于表示两个文件或目录是否相同；
- `queryPermission`：返回一个`Promise`对象，用于查询文件或目录的权限；
- `requestPermission`：返回一个`Promise`对象，用于请求文件或目录的权限；
- `remove`：返回一个`Promise`对象，用于删除文件或目录；

我们可以通过`kind`属性来判断当前的`FileSystemHandle`对象是文件还是目录。

```
const fileHandle = await window.showOpenFilePicker();
const file = await fileHandle[0].getFile();
console.log(fileHandle[0].kind);
复制代码
```

当然我们使用的是`showOpenFilePicker`方法，所以它返回的肯定是文件，所以还有一个`showDirectoryPicker`方法，它可以用来选择目录。

### 选择目录

选择目录的方法和选择文件的方法是一样的，只是我们需要使用`showDirectoryPicker`方法。

```
const directoryHandle = await window.showDirectoryPicker();
console.log(directoryHandle);
复制代码
```

![图片](https://mmbiz.qpic.cn/mmbiz/bwG40XYiaOKna8LkgGSaJotSLmvWIlZFsCyh3Pmutj9zuxK4GcjF3yU6T9abKkV25JORnMXb7ryOyxp9RnsF9rg/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)image.png

可以看到，我们通过`showDirectoryPicker`方法获取到了目录，它返回的是一个`FileSystemDirectoryHandle`对象，我们可以通过它来获取和操作目录。

> 使用`showDirectoryPicker`方法时，浏览器会提示用户授权应用程序访问他们的文件系统，请不要拒绝哟。

#### FileSystemDirectoryHandle

`FileSystemDirectoryHandle`对象是一个代表文件系统中的目录的对象，它提供了一些方法来获取和操作目录。

`FileSystemDirectoryHandle`提供的方法就比较多了，例如：

- `entries`：返回一个`AsyncIterable`对象，用于获取目录中的所有文件和目录；
- `keys`：返回一个`AsyncIterable`对象，用于获取目录中的所有文件和目录的名称；
- `values`：返回一个`AsyncIterable`对象，用于获取目录中的所有文件和目录的`FileSystemHandle`对象；
- `getFileHandle`：返回一个`Promise`对象，用于获取目录中的文件；
- `getDirectoryHandle`：返回一个`Promise`对象，用于获取目录中的目录；
- `removeEntry`：返回一个`Promise`对象，用于删除目录中的文件或目录；
- `resolve`：返回一个`Promise`对象，用于获取目录中的文件或目录；

`entries`、`keys`、`values`这三个方法都是用来获取目录中的所有文件和目录的，它们返回的都是一个`AsyncIterable`对象，我们可以通过`for await...of`语法来遍历它。

```
const directoryHandle = await window.showDirectoryPicker();
for await (const [name, handle] of directoryHandle.entries()) {
    if (handle.kind === 'file') {
        console.log(name, 'file');
    } else {
        console.log(name, 'directory');
    }
}
复制代码
```

我们可以通过`handle.kind`来判断当前的`FileSystemHandle`对象是文件还是目录。

而这里的`getFileHandle`、`getDirectoryHandle`就是用来获取目录中的文件和目录的，它们都返回一个`Promise`对象，我们可以通过`await`来获取它们。

```
const directoryHandle = await window.showDirectoryPicker();
for await (const [name, handle] of directoryHandle.entries()) {
    if (handle.kind === 'file') {
        const fileHandle = await directoryHandle.getFileHandle(name);
        console.log(fileHandle);
    } else {
        const directoryHandle = await directoryHandle.getDirectoryHandle(name);
        console.log(directoryHandle);
    }
}
复制代码
```

这里大家可以自己尝试一下，我就不截图了。

## 操作文件

上面我们了解到了如何获取文件和目录，那么我们接下来就来看看如何操作文件和目录。

### 读取文件

读取文件做过文件上传的同学应该都很熟悉了，我们可以使用`FileReader`对象来读取文件。

```
const fileHandle = await window.showOpenFilePicker({
    excludeAcceptAllOption: false,
    types: [
        {
            description: 'Text files',
            accept: {
                'text/plain': ['.txt'],
            },
        },
    ],
});
const file = await fileHandle[0].getFile();
const reader = new FileReader();
reader.onload = () => {
    console.log(reader.result);
};
reader.readAsText(file);
复制代码
```

这里我们在使用`showOpenFilePicker`方法时，我们通过`types`属性来限制文件的类型，这样用户就只能选择文本文件了。

`showOpenFilePicker`还有其他的属性，例如：

- `multiple`：一个`boolean`值，默认为`false`，是否允许用户选择多个文件；

- `excludeAcceptAllOption`：一个`boolean`值，默认为`false`，是否允许用户选择所有类型的文件（就是选择文件下拉的所有文件选项）；

- `types`：一个数组，用于限制用户选择的文件类型（就是选择文件的下拉选项）；

- - `description`：一个字符串，用于描述文件类型（就是下拉选项的文字）；
  - `accept`：一个对象，用于描述文件类型（就是控制选择文件的类型，例如`image/*`表示图片类型），具体可以参考：**MIME types**[1]；

### 写入文件

写入文件可以使用上面提到的`FileSystemFileHandle`对象的`createWritable`方法来创建一个`FileSystemWritableFileStream`对象，然后通过它来写入文件。

```
const fileHandle = await window.showSaveFilePicker({
    types: [
        {
            description: 'Text files',
            accept: {
                'text/plain': ['.txt'],
            },
        },
    ],
});

// 创建一个可写流
const writable = await fileHandle.createWritable();

// 写入数据
await writable.write('Hello World!');

// 关闭流
await writable.close();
复制代码
```

这里我们使用`showSaveFilePicker`方法来创建一个文件，然后通过`createWritable`方法来创建一个可写流，然后通过`write`方法来写入数据，最后通过`close`方法来关闭流。

`showSaveFilePicker`也是文件选择器的一种，它和`showOpenFilePicker`的区别在于，`showSaveFilePicker`是用来创建文件的，而`showOpenFilePicker`是用来选择文件的。

`showSaveFilePicker`返回的是新创建的文件的`FileSystemFileHandle`对象，而`showOpenFilePicker`返回的是选择的文件的`FileSystemFileHandle`对象。

> 注意：操作文件流时，一定要记得关闭流哟，否则会导致文件锁定，无法进行其他操作，做前端的同学可能对这一块并不熟悉，所以特此提醒一下。

## 操作目录

上面我们已经知道了如何操作文件了，那么接下来我们就来看看如何操作目录。

### 创建目录

创建目录可以使用`FileSystemDirectoryHandle`对象的`getDirectoryHandle`方法来创建一个目录。

```
const directoryHandle = await window.showDirectoryPicker();
const newDirectoryHandle = await directoryHandle.getDirectoryHandle('new-directory', {
    create: true,
});
复制代码
```

`getDirectoryHandle`方法接收两个参数：

- `name`：一个字符串，用于指定目录的名称；

- `options`：一个对象，用于指定目录的选项（可选）；

- - `create`：一个`boolean`值，默认为`false`，是否创建目录；

目前只有`create`一个选项，如果设置为`true`，则会创建一个目录，如果设置为`false`，则会获取一个目录。

如果目录不存在，且`create`为`false`，则会报错。

### 删除目录

删除目录可以使用`FileSystemDirectoryHandle`对象的`removeEntry`方法来删除一个目录。

```
const directoryHandle = await window.showDirectoryPicker();
await directoryHandle.removeEntry('new-directory');
复制代码
```

`removeEntry`方法接收一个参数，一个字符串，用于指定要删除的目录的名称。

## 兼容性

截止到现在，`showDirectoryPicker`和`showOpenFilePicker`这两个方法在`Chrome 86版本`中已经可以正常使用了，但是在`Firefox`中还不支持。

下面是来自**caniuse**[2]的兼容性数据：

![图片](https://mmbiz.qpic.cn/mmbiz/bwG40XYiaOKna8LkgGSaJotSLmvWIlZFsiaoGicrUKVeUZEf4OeicwhucLY1DHvohAZqJyAjHZNkd4ujBBliaib4ZVHw/640?wx_fmt=other&wxfrom=5&wx_lazy=1&wx_co=1)image.png

虽然`Firefox`还不支持，但是在一些实验性的项目上我们可以使用这些`API`，指定用户使用`Chrome`浏览器来访问。