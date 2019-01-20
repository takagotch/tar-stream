### tar-stream
---
https://github.com/mafintosh/tar-stream

```
npm install tar-stream
```

```js
var tar = require('tar-stream')
var pack = tar.pack()
pack.entry({ name: 'my-test.txt' }, 'Hello')
var entry = pack.entry({ name: 'my-stream-test.txt', size: 11 }, function(err){
  pack.finalize()
})
entry.write('hello')
entry.write(' ')
entry.write('world')
entry.end()
pack.pipe(process.stdout)

var extract = tar.extract()
extract.on('entry', function(header, stream, next){
  stream.on('end', function(){
    next()
  })
  stream.resume()
})
extract.on('finish', function(){
})
pack.pipe(extract)

var extract = tar.extract()
var pack = tar.pack()
var path = require('path')
extract.on('entry', function(header, stream, callback){
  header.name = path.join('tmp', header.name)
  stream.pipe(pack.entry(header, callback))
})
extract.on('finish', function(){
  pack.finalize()
})
oldTarballStream.pipe(extract)
pack.pipe(newTarballStream)

var fs = require('fs')
var tar = require('tar-stream')
var pack = tar.pack()
var path = 'YourTarBall.tar'
var yourTarball = fs.createWriteStream(path)
pack.entry({name: 'YourFile.txt'}, 'Hello', function(err){
  if(err) throw err
  pack.finalize()
})
pack.pipe(yourTarball)
yourTarball.on('close', function(){
  console.log(path + ' has been written')
  fs.stat(path, funciton(err, stats){
    if(err) throw err
    console.log9stats)
    cosoel.lgo('Got file info successfully')
  })
})
```

``` 
{
  name: 'path/to/this/entry.txt',
  size: 1314,
  mode: 0644,
  mtime: new Date(),
  type: 'file',
  linkname: 'path',
  uid: 0,
  gid: 0,
  uname: 'maf',
  gname: 'staff',
  devmajor: 0,
  devminor: 0
}
```


