# react-qiniu

React Component to upload file to [Qiniu](http://www.qiniu.com/)

![img](https://raw.githubusercontent.com/paramaggarwal/react-dropzone/master/screenshot.png)

Demo will avaiable soon

## Usage

Just `require('react-qiniu')` and specify an `onDrop` method that accepts an array of dropped files and pass your Qiniu `token` as prop.

You can also specify a style object to apply to the Drop Zone.
Optionally pass in a size property to configure the size of the Drop Zone.

```jsx
var React = require('react');
var Qiniu = require('react-qiniu');

var ReactQiniuDemo = React.createClass({
    getInitialState: function () {
        return {
            files: [],
            token: 'YOUR_UPLOAD_TOKEN',
            prefix: 'YOUR_QINIU_KEY_PREFIX' // Optional
        };
    },
    onDrop: function (files) {
        this.setState({
            files: files
        });
        // files is a FileList(https://developer.mozilla.org/en/docs/Web/API/FileList) Object
        // and with each file, we attached two functions to handle upload progress and status
        // file.progress => return upload progress of file
        // file.uploadPromise => return a Promise to handle uploading status(what you can do when upload failed)
        // `react-qiniu` using bluebird, check bluebird API https://github.com/petkaantonov/bluebird/blob/master/API.md
      console.log('Received files: ', files);
    },

    render: function () {
      return (
          <div>
            <Qiniu onDrop={this.onDrop} size={150} token={this.state.token}>
              <div>Try dropping some files here, or click to select files to upload.</div>
            </Qiniu>
          </div>
      );
    }
});

React.render(<ReactQiniuDemo />, document.body);
```

when upload, we will add a `promise` to file object, see [index.js](https://github.com/lenage/react-qiniu/blob/master/index.js#L68),
so, you can deal with this promise to handle upload status. (do something when success/failure)

see more in `example/app.js`

## Contributing

1. Fork it ( https://github.com/lingochamp/react-qiniu/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## Thanks

[@paramaggarwal](https://github.com/paramaggarwal/react-dropzone)

## License

MIT
