[![npm package](https://nodei.co/npm/synquer.png?downloads=true&downloadRank=true?maxAge=30)](https://nodei.co/npm/synquer/)

[![NPM version](https://img.shields.io/npm/v/synquer.svg)](https://img.shields.io/npm/v/synquer.svg) [![NPM License](https://img.shields.io/npm/l/synquer.svg)](https://img.shields.io/npm/l/synquer.svg) [![Downloads](https://img.shields.io/npm/dt/synquer.svg?maxAge=43200)](https://img.shields.io/npm/dt/synquer.svg?maxAge=60) [![ISSUES](https://img.shields.io/github/issues/cirospaciari/synquer.svg?maxAge=60)](https://img.shields.io/github/issues/cirospaciari/synquer.svg?maxAge=60)

Support me for future versions:

[![BMC](https://cdn.buymeacoffee.com/buttons/default-orange.png)](https://www.buymeacoffee.com/i2yBGw7)

[![PAGSEGURO](https://stc.pagseguro.uol.com.br/public/img/botoes/doacoes/209x48-doar-assina.gif)](https://pag.ae/7VxyJphKt)


Node documentation says:

    It is unsafe to use fs.write() multiple times on the same file without waiting for the callback.
    https://nodejs.org/api/fs.html#fs_fs_write_fd_buffer_offset_length_position_callback

Synquer can be used for sync write calls to the same file.
But Synquer can be used for sync any promises not only write calls.
        
How install:

npm install synquer

# Example

```javascript

const fs = require('fs');
const util = require('util');
const writeAsync = util.promisify(fs.write);


//Wait Queue
const { Synquer } = require('synquer');
//import Synquer from 'synquer';

const write_queue = new Synquer();

async function write(){
    //write in order
    return write_queue.execute(()=> writeAsync(...arguments)); 
}

//now all writes will be queued
await Promise.all([
    write(fd, buffer, offset, length, position),
    write(fd, other_buffer, offset, length, position),
    write(fd, buffer, offset, other_length, other_position)
]);

```
