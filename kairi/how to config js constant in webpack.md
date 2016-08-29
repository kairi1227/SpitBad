#1���滻html�����ݡ������滻js��cdn��
##webpack������
```
const cdn = '//cdn.bootcss.com';
new ReplacePlugin({
      entry: './src/assignment-instructor.html',
      //hash: '[hash]',
      output: `${psweb_path}/assignment-instructor.html`,
      data: {react: `<script src="${cdn}/react/0.14.7/react.min.js"></script>`}
    }),
```
##htmlҳ��д��
```
  <!-- replace:react -->
  <script src="../js/react.min.js"></script>
  <!-- endreplace -->
```
��ϸ�ɲο� [replace-webpack-plugin](https://github.com/otelnov/replace-webpack-plugin)

#2��JS�г������滻

## webpack������ ��plugins�м���
```
new webpack.DefinePlugin({
            'process.env.NODE_ENV': '"development"',
            'process.env.webSocket': '"192.168.0.193"'
        }),
```
##js��ʹ�ã�
```
export const webSocketUrl = `ws://${process.env.webSocket}/notice/websocket`;
```
��js ʹ�ã�������webpack�ж���ı������뼴�ɡ�
��ϸ�ɲο�[webpack DefinePlugin](https://webpack.github.io/docs/list-of-plugins.html#defineplugin)