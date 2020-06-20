# Build Your Own Voice Package

## Step 1: Create `manifest.json`

Create an empty folder, change your directory into that folder and create a `manifest.json` file. The `manifest.json` file must include the following name-value pairs as shown beloew.

```json
// manifest.json
{
  "name": "my-voice-package-name",
  // your voice package name. Must be all in low case, hyphen symbol is allowed. e.g.,"my-voice-package-name"
  "version": "0.0.1",
  // voice package verion, e.g., "1.0.0"
  "contributes": [
    // ... voice files configuration, more details in next step.
  ]
}
```

## Step 2: Configure voice files

Copy your .mp3 files to the same directory as the `manifest.json` file. For example,

```bash
├── /my-voice-package-name
│   ├── manifest.json
│   ├── function.mp3
│   └── import.mp3
```

将录制好的音频文件（mp3）拷贝与 `manifest.json` 同级的目录中，当前 `vscode-rainbow-fart` 扩展暂时不支持处理子目录内的音频文件。

然后，在 `manifest.json` 中为 `contributes` 字段增添配置。假设我们需要检测 `function` 关键字然后播放 `function.mp3` 音频，则如下填写：

```json
// manifest.json
{
  "contributes": [
    {
      "keywords": "function",
      "voices": "function.mp3"
    }
  ]
}
```

同时，扩展还支持多个关键字共用一个音频，或者对应多个音频并随机播放。如下：

```json
// manifest.json
{
  "contributes": [
    {
      "keywords": ["function", "=>"],
      // 支持 ES6 箭头函数 ()=>{}
      "voices": [
        "function_01.mp3",
        "function_02.mp3",
        "function_03.mp3"
        // ...
      ]
    }
  ]
}
```

## Step 3: 丰富语音包元信息

语音包元信息文件还有很多其他字段，可以展示很多额外的信息（如下）。

<ImageZoom src="/zh/assets/ui-settings.png" :border="true" width="300"/>

<Note>以下字段均为可选字段</Note>

### display-name <Badge>String</Badge>

`name` 字段更多的是语音包的标识 ID，而 `display-name` 字段则可以在页面上显示绝大部分字符（空格、数字、Emoji 等）

### description <Badge>String</Badge>

语音包描述，可以写一些关于语音包的声明等纯文本。

### author <Badge>String</Badge>

作者名

### avatar <Badge>String</Badge>

头像图片，需要将图片文件拷贝到语音包目录中，然后在 `avatar` 字段中填写文件名。

### avatar-dark <Badge>String</Badge>

在暗黑模式下呈现的头像图片，通过降低图片的饱和度、亮度使其在夜间也可以适宜的观看。

<Note>部分内置语音包所使用的字段并未在此呈现，因为这些字段是实验性质的。</Note>

## Step 4: 打包

最后，选中所有文件，压缩为 zip 文件。**请勿将父目录一并压缩，所有文件应处于 zip 的顶层。**
