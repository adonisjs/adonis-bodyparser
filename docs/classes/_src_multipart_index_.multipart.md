[@adonisjs/bodyparser](../README.md) > ["src/Multipart/index"](../modules/_src_multipart_index_.md) > [Multipart](../classes/_src_multipart_index_.multipart.md)

# Class: Multipart

Multipart class offers a low level API to interact the incoming HTTP request data as a stream. This makes it super easy to write files to s3 without saving them to the disk first.

### Usage

```js
const multipart = new Multipart(options)

multipart.onFile('profile', async (stream) => {
 stream.pipe(fs.createWriteStream('./profile.jpg'))
})

multipart.onField('*', async (key, value) => {
})

try {
  await multipart.process()
} catch (error) {
  // all errors are sent to the process method
}
```

## Hierarchy

**Multipart**

## Implements

* `MultipartContract`

## Index

### Constructors

* [constructor](_src_multipart_index_.multipart.md#constructor)

### Properties

* [consumed](_src_multipart_index_.multipart.md#consumed)

### Methods

* [onField](_src_multipart_index_.multipart.md#onfield)
* [onFile](_src_multipart_index_.multipart.md#onfile)
* [process](_src_multipart_index_.multipart.md#process)

---

## Constructors

<a id="constructor"></a>

###  constructor

⊕ **new Multipart**(_request: *`IncomingMessage`*): [Multipart](_src_multipart_index_.multipart.md)

**Parameters:**

| Name | Type |
| ------ | ------ |
| _request | `IncomingMessage` |

**Returns:** [Multipart](_src_multipart_index_.multipart.md)

___

## Properties

<a id="consumed"></a>

###  consumed

**● consumed**: *`boolean`* = false

Consumed is set to true when `process` is called. Calling process multiple times is not possible and hence this boolean must be checked first

___

## Methods

<a id="onfield"></a>

###  onField

▸ **onField**(name: *`string`*, handler: *`FieldHandler`*): `this`

Get notified on a given field or all fields. An exception inside the callback will abort the request body parsing and raises and exception.

*__example__*:
 ```
multipart.onField('username', (key, value) => {
})

multipart.onField('*', (key, value) => {
})
```

**Parameters:**

| Name | Type |
| ------ | ------ |
| name | `string` |
| handler | `FieldHandler` |

**Returns:** `this`

___
<a id="onfile"></a>

###  onFile

▸ **onFile**(name: *`string`*, handler: *`PartHandler`*): `this`

Attach handler for a given file. To handle all files, you can attach a wildcard handler. Also only can handler can be defined, since processing a stream at multiple locations is not possible.

*__example__*:
 ```
multipart.onFile('package', async (stream) => {
})

multipart.onFile('*', async (stream) => {
})
```

**Parameters:**

| Name | Type |
| ------ | ------ |
| name | `string` |
| handler | `PartHandler` |

**Returns:** `this`

___
<a id="process"></a>

###  process

▸ **process**(): `Promise`<`void`>

Process the request by going all the file and field streams.

**Returns:** `Promise`<`void`>

___
