# @ohos.file.photoAccessHelper (Album Management)

The **photoAccessHelper** module provides APIs for album management, including creating an album and accessing and modifying media data an album.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import photoAccessHelper from '@ohos.file.photoAccessHelper';
```

## photoAccessHelper.getPhotoAccessHelper

getPhotoAccessHelper(context: Context): PhotoAccessHelper

Obtains a **PhotoAccessHelper** instance for accessing and modifying media files in the album.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**Parameters**

| Name | Type   | Mandatory| Description                      |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](js-apis-inner-app-context.md) | Yes  | Context of the ability instance.|

**Return value**

| Type                           | Description   |
| ----------------------------- | :---- |
| [PhotoAccessHelper](#photoaccesshelper) | Returns the **PhotoAccessHelper** instance created.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
// The phAccessHelper instance obtained is a global object. It is used by default in subsequent operations. If the code snippet is not added, an error will be reported indicating that phAccessHelper is not defined.
const context = getContext(this);
let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);
```

## PhotoAccessHelper

### getAssets

getAssets(options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;PhotoAsset&gt;&gt;): void;

Obtains image and video assets. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| options  | [FetchOptions](#fetchoptions)        | Yes  | Options for fetching the image and video assets.             |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Yes  | Callback invoked to return the image and video assets obtained.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAssets');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };

  phAccessHelper.getAssets(fetchOptions, async (err, fetchResult) => {
    if (fetchResult != undefined) {
      console.info('fetchResult success');
      let photoAsset = await fetchResult.getFirstObject();
      if (photoAsset != undefined) {
        console.info('photoAsset.displayName : ' + photoAsset.displayName);
      }
    } else {
      console.error('fetchResult fail' + err);
    }
  });
}
```

### getAssets

getAssets(options: FetchOptions): Promise&lt;FetchResult&lt;PhotoAsset&gt;&gt;;

Obtains image and video assets. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**Parameters**

| Name | Type               | Mandatory| Description            |
| ------- | ------------------- | ---- | ---------------- |
| options | [FetchOptions](#fetchoptions)   | Yes  | Options for fetching the image and video assets.    |

**Return value**

| Type                       | Description          |
| --------------------------- | -------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Promise used to return the image and video assets obtained.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAssets');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult = await phAccessHelper.getAssets(fetchOptions);
    if (fetchResult != undefined) {
      console.info('fetchResult success');
      let photoAsset = await fetchResult.getFirstObject();
      if (photoAsset != undefined) {
        console.info('photoAsset.displayName :' + photoAsset.displayName);
      }
    }
  } catch (err) {
    console.error('getAssets failed, message = ', err);
  }
}
```

### createAsset

createAsset(displayName: string, callback: AsyncCallback&lt;PhotoAsset&gt;): void;

Creates an image or video asset with the specified file name. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | Yes  | File name of the image or video to create.             |
| callback |  AsyncCallback&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Callback invoked to return the image or video created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md) and [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if type displayName is not string.         |
| 14000001   | if type of displayName is invalid.         |

**Example**

```ts
async function example() {
  console.info('createAssetDemo');
  let testFileName = 'testFile' + Date.now() + '.jpg';
  phAccessHelper.createAsset(testFileName, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(displayName: string): Promise&lt;PhotoAsset&gt;;

Creates an image or video asset with the specified file name. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | Yes  | File name of the image or video to create.             |

**Return value**

| Type                       | Description          |
| --------------------------- | -------------- |
| Promise&lt;[PhotoAsset](#photoasset)&gt; | Promise used to return the created image and video asset.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md) and [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if type displayName or albumUri is not string.         |
| 14000001   | if type of displayName is invalid.         |

**Example**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    let photoAsset = await phAccessHelper.createAsset(testFileName);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error('createAsset failed, message = ', err);
  }
}
```

### createAsset

createAsset(displayName: string, options: PhotoCreateOptions, callback: AsyncCallback&lt;PhotoAsset&gt;): void;

Creates an image or video asset with the specified file name and options. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | Yes  | File name of the image or video to create.             |
| options  | [PhotoCreateOptions](#photocreateoptions)        | Yes  | Options for creating an image or video asset.             |
| callback |  AsyncCallback&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Callback invoked to return the image or video created.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md) and [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if type displayName is not string.         |
| 14000001   | if type displayName invalid.         |

**Example**

```ts
async function example() {
  console.info('createAssetDemo');
  let testFileName = 'testFile' + Date.now() + '.jpg';
  let createOption = {
    subtype: photoAccessHelper.PhotoSubtype.DEFAULT
  }
  phAccessHelper.createAsset(testFileName, createOption, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(displayName: string, options: PhotoCreateOptions): Promise&lt;PhotoAsset&gt;;

Creates an image or video asset with the specified file name and options. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | Yes  | File name of the image or video to create.             |
| options  |  [PhotoCreateOptions](#photocreateoptions)       | Yes  | Options for creating an image or video asset.             |

**Return value**

| Type                       | Description          |
| --------------------------- | -------------- |
| Promise&lt;[PhotoAsset](#photoasset)&gt; | Promise used to return the created image and video asset.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md) and [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |  
| 401   | if type displayName is not string.         |
| 14000001   | if type of displayName is invalid.         |

**Example**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    let createOption = {
      subtype: photoAccessHelper.PhotoSubtype.DEFAULT
    }
    let photoAsset = await phAccessHelper.createAsset(testFileName, createOption);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error('createAsset failed, message = ', err);
  }
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, options: CreateOptions, callback: AsyncCallback&lt;string&gt;): void;

Creates an image or video asset with the specified file type, file name extension, and options. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | Yes  | Type of the file to create, which can be **IMAGE** or **VIDEO**.             |
| extension  | string        | Yes  | File name extension, for example, **jpg**.             |
| options  | [CreateOptions](#createoptions)        | Yes  | Options for creating the image or video asset, for example, **{title: 'testPhoto'}**.             |
| callback |  AsyncCallback&lt;string&gt; | Yes  | Callback invoked to return the URI of the created image or video.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type createOption is wrong.         |

**Example**

```ts
async function example() {
  console.info('createAssetDemo');
  let photoType = photoAccessHelper.PhotoType.IMAGE;
  let extension = 'jpg';
  let options = {
    title: 'testPhoto'
  }
  phAccessHelper.createAsset(photoType, extension, options, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, callback: AsyncCallback&lt;string&gt;): void;

Creates an image or video asset with the specified file type and file name extension. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | Yes  | Type of the file to create, which can be **IMAGE** or **VIDEO**.             |
| extension  | string        | Yes  | File name extension, for example, **jpg**.             |
| callback |  AsyncCallback&lt;string&gt; | Yes  | Callback invoked to return the URI of the created image or video.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type createOption is wrong.         |

**Example**

```ts
async function example() {
  console.info('createAssetDemo');
  let photoType = photoAccessHelper.PhotoType.IMAGE;
  let extension = 'jpg';
  phAccessHelper.createAsset(photoType, extension, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error('createAsset failed, message = ', err);
    }
  });
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, options?: CreateOptions): Promise&lt;string&gt;;

Creates an image or video asset with the specified file type, file name extension, and options. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | Yes  | Type of the file to create, which can be **IMAGE** or **VIDEO**.             |
| extension  | string        | Yes  | File name extension, for example, **jpg**.             |
| options  | [CreateOptions](#createoptions)        | No  | Options for creating the image or video asset, for example, **{title: 'testPhoto'}**.             |

**Return value**

| Type                       | Description          |
| --------------------------- | -------------- |
| Promise&lt;string&gt; | Promise used to return the URI of the created image or video asset.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type createOption is wrong.         |

**Example**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let photoType = photoAccessHelper.PhotoType.IMAGE;
    let extension = 'jpg';
    let options = {
      title: 'testPhoto'
    }
    let photoAsset = await phAccessHelper.createAsset(photoType,extension, options);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error('createAsset failed, message = ', err);
  }
}
```

### createAlbum

createAlbum(name: string, callback: AsyncCallback&lt;Album&gt;): void;

Creates an album. This API uses an asynchronous callback to return the result.

The album name must meet the following requirements:
- The album name is a string of 1 to 255 characters.
- The album name cannot contain any of the following characters:<br>.. \ / : * ? " ' ` < > | { } [ ]
- The album name is case-insensitive.
- Duplicate album names are not allowed.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| name  | string         | Yes  | Name of the album to create.             |
| callback |  AsyncCallback&lt;[Album](#album)&gt; | Yes  | Callback invoked to return the created album instance.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
async function example() {
  console.info('createAlbumDemo');
  let albumName = 'newAlbumName' + new Date().getTime();
  phAccessHelper.createAlbum(albumName, (err, album) => {
    if (err) {
      console.error('createAlbumCallback failed with err: ' + err);
      return;
    }
    console.info('createAlbumCallback successfully, album: ' + album.albumName + ' album uri: ' + album.albumUri);
  });
}
```

### createAlbum

createAlbum(name: string): Promise&lt;Album&gt;;

Creates an album. This API uses a promise to return the result.

The album name must meet the following requirements:
- The album name is a string of 1 to 255 characters.
- The album name cannot contain any of the following characters:<br>.. \ / : * ? " ' ` < > | { } [ ]
- The album name is case-insensitive.
- Duplicate album names are not allowed.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| name  | string         | Yes  | Name of the album to create.             |

**Return value**

| Type                       | Description          |
| --------------------------- | -------------- |
| Promise&lt;[Album](#album)&gt; | Promise used to return the created album instance.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
async function example() {
  console.info('createAlbumDemo');
  let albumName = 'newAlbumName' + new Date().getTime();
  phAccessHelper.createAlbum(albumName).then((album) => {
    console.info('createAlbumPromise successfully, album: ' + album.albumName + ' album uri: ' + album.albumUri);
  }).catch((err) => {
    console.error('createAlbumPromise failed with err: ' + err);
  });
}
```

### deleteAlbums

deleteAlbums(albums: Array&lt;Album&gt;, callback: AsyncCallback&lt;void&gt;): void;

Deletes albums. This API uses an asynchronous callback to return the result.

Ensure that the albums to be deleted exist. Only user albums can be deleted.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| albums  | Array&lt;[Album](#album)&gt;         | Yes  | Albums to delete.             |
| callback |  AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // Delete the album named newAlbumName.
  console.info('deleteAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album = await fetchResult.getFirstObject();
  phAccessHelper.deleteAlbums([album], (err) => {
    if (err) {
      console.error('deletePhotoAlbumsCallback failed with err: ' + err);
      return;
    }
    console.info('deletePhotoAlbumsCallback successfully');
  });
  fetchResult.close();
}
```

### deleteAlbums

deleteAlbums(albums: Array&lt;Album&gt;): Promise&lt;void&gt;;

Deletes albums. This API uses a promise to return the result.

Ensure that the albums to be deleted exist. Only user albums can be deleted.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| albums  |  Array&lt;[Album](#album)&gt;          | Yes  | Albums to delete.             |

**Return value**

| Type                       | Description          |
| --------------------------- | -------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // Delete the album named newAlbumName.
  console.info('deleteAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album = await fetchResult.getFirstObject();
  phAccessHelper.deleteAlbums([album]).then(() => {
    console.info('deletePhotoAlbumsPromise successfully');
    }).catch((err) => {
      console.error('deletePhotoAlbumsPromise failed with err: ' + err);
  });
  fetchResult.close();
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void;

Obtains albums based on the specified options and album type. This API uses an asynchronous callback to return the result.

Before the operation, ensure that the albums to obtain exist.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | Yes  | Type of the album to obtain.             |
| subtype  | [AlbumSubtype](#albumsubtype)         | Yes  | Subtype of the album.             |
| options  | [FetchOptions](#fetchoptions)         | Yes  |  Options for fetching the albums.             |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | Yes  | Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOption.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // Obtain the album named newAlbumName.
  console.info('getAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions, async (err, fetchResult) => {
    if (err) {
      console.error('getAlbumsCallback failed with err: ' + err);
      return;
    }
    if (fetchResult == undefined) {
      console.error('getAlbumsCallback fetchResult is undefined');
      return;
    }
    let album = await fetchResult.getFirstObject();
    console.info('getAlbumsCallback successfully, albumName: ' + album.albumName);
    fetchResult.close();
  });
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void;

Obtains albums by type. This API uses an asynchronous callback to return the result.

Before the operation, ensure that the albums to obtain exist.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | Yes  | Type of the album to obtain.             |
| subtype  | [AlbumSubtype](#albumsubtype)         | Yes  | Subtype of the album.             |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | Yes  | Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOption.         |

**Example**

```ts
async function example() {
  // Obtain the system album VIDEO, which is preset by default.
  console.info('getAlbumsDemo');
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.VIDEO, async (err, fetchResult) => {
    if (err) {
      console.error('getAlbumsCallback failed with err: ' + err);
      return;
    }
    if (fetchResult == undefined) {
      console.error('getAlbumsCallback fetchResult is undefined');
      return;
    }
    let album = await fetchResult.getFirstObject();
    console.info('getAlbumsCallback successfully, albumUri: ' + album.albumUri);
    fetchResult.close();
  });
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, options?: FetchOptions): Promise&lt;FetchResult&lt;Album&gt;&gt;;

Obtains albums based on the specified options and album type. This API uses a promise to return the result.

Before the operation, ensure that the albums to obtain exist.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**Parameters**

| Name  | Type                    | Mandatory| Description                     |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | Yes  | Type of the album to obtain.             |
| subtype  | [AlbumSubtype](#albumsubtype)         | Yes  | Subtype of the album.             |
| options  | [FetchOptions](#fetchoptions)         | No  |  Options for fetching the albums. If this parameter is not specified, the albums are obtained based on the album type by default.             |

**Return value**

| Type                       | Description          |
| --------------------------- | -------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOption.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // Obtain the album named newAlbumName.
  console.info('getAlbumsDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions).then( async (fetchResult) => {
    if (fetchResult == undefined) {
      console.error('getAlbumsPromise fetchResult is undefined');
      return;
    }
    let album = await fetchResult.getFirstObject();
    console.info('getAlbumsPromise successfully, albumName: ' + album.albumName);
    fetchResult.close();
  }).catch((err) => {
    console.error('getAlbumsPromise failed with err: ' + err);
  });
}
```

### deleteAssets

deleteAssets(uriList: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

Deletes media files. This API uses an asynchronous callback to return the result. The deleted files are moved to the trash.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | Yes  | URIs of the media files to delete.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteAssetDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  phAccessHelper.deleteAssets([asset.uri], (err) => {
    if (err == undefined) {
      console.info('deleteAssets successfully');
    } else {
      console.error('deleteAssets failed with error: ' + err);
    }
  });
}
```

### deleteAssets

deleteAssets(uriList: Array&lt;string&gt;): Promise&lt;void&gt;;

Deletes media files. This API uses a promise to return the result. The deleted files are moved to the trash.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | Yes  | URIs of the media files to delete.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  try {
    await phAccessHelper.deleteAssets([asset.uri]);
    console.info('deleteAssets successfully');
  } catch (err) {
    console.error('deleteAssets failed with error: ' + err);
  }
}
```

### registerChange

registerChange(uri: string, forChildUris: boolean, callback: Callback&lt;ChangeData&gt;) : void

Registers listening for the specified URI. This API uses a callback to return the result.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name   | Type                                       | Mandatory| Description                                                        |
| --------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| uri       | string                                      | Yes  | URI of the photo asset, URI of the album, or [DefaultChangeUri](#defaultchangeuri).|
| forChildUris | boolean                                     | Yes  | Whether to perform fuzzy listening.<br>If **uri** is the URI of an album, the value **true** means to listen for the changes of the files in the album; the value **false** means to listen for the changes of the album only. <br>If **uri** is the URI of a **photoAsset**, there is no difference between **true** and **false** for **forChildUris**.<br>If **uri** is **DefaultChangeUri**, **forChildUris** must be set to **true**. If **forChildUris** is **false**, the URI cannot be found and no message can be received.|
| callback  | Callback&lt;[ChangeData](#changedata)&gt; | Yes  | Callback invoked to return the [ChangeData](#changedata). <br>**NOTE**<br>Multiple callback listeners can be registered for a URI. You can use [unRegisterChange](#unregisterchange) to unregister all listeners for the URI or a specified callback listener.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('registerChangeDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset = await fetchResult.getFirstObject();
  if (photoAsset != undefined) {
    console.info('photoAsset.displayName : ' + photoAsset.displayName);
  }
  let onCallback1 = (changeData) => {
      console.info('onCallback1 success, changData: ' + JSON.stringify(changeData));
    //file had changed, do something
  }
  let onCallback2 = (changeData) => {
      console.info('onCallback2 success, changData: ' + JSON.stringify(changeData));
    //file had changed, do something
  }
  // Register onCallback1.
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback1); 
  // Register onCallback2.
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback2);

  photoAsset.favorite(true, (err) => {
    if (err == undefined) {
      console.info('favorite successfully');
    } else {
      console.error('favorite failed with error:' + err);
    }
  });
}
```

### unRegisterChange

unRegisterChange(uri: string, callback?: Callback&lt;ChangeData&gt;): void

Unregisters listening for the specified URI. Multiple callbacks can be registered for a URI for listening. You can use this API to unregister the listening of the specified callbacks or all callbacks.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                                       | Mandatory| Description                                                        |
| -------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| uri      | string                                      | Yes  | URI of the photo asset, URI of the album, or [DefaultChangeUri](#defaultchangeuri).|
| callback | Callback&lt;[ChangeData](#changedata)&gt; | No  | Callback to unregister. If this parameter is not specified, all the callbacks for listening for the URI will be canceled. <br>**NOTE**: The specified callback unregistered will not be invoked when the data changes.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('offDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset = await fetchResult.getFirstObject();
  if (photoAsset != undefined) {
    console.info('photoAsset.displayName : ' + photoAsset.displayName);
  }
  let onCallback1 = (changeData) => {
    console.info('onCallback1 on');
  }
  let onCallback2 = (changeData) => {
    console.info('onCallback2 on');
  }
  // Register onCallback1.
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback1);
  // Register onCallback2.
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback2);
  // Unregister the listening of onCallback1.
  phAccessHelper.unRegisterChange(photoAsset.uri, onCallback1);
  photoAsset.favorite(true, (err) => {
    if (err == undefined) {
      console.info('favorite successfully');
    } else {
      console.error('favorite failed with error:' + err);
    }
  });
}
```

### createDeleteRequest

createDeleteRequest(uriList: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

Creates a dialog box for deleting photos. This API uses an asynchronous callback to return the result. The deleted photos are moved to the trash.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | Yes  | URIs of the media files to delete.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('createDeleteRequestDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  phAccessHelper.createDeleteRequest([asset.uri], (err) => {
    if (err == undefined) {
      console.info('createDeleteRequest successfully');
    } else {
      console.error('createDeleteRequest failed with error: ' + err);
    }
  });
}
```

### createDeleteRequest

createDeleteRequest(uriList: Array&lt;string&gt;): Promise&lt;void&gt;;

Creates a dialog box for deleting photos. This API uses a promise to return the result. The deleted photos are moved to the trash.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | Yes  | URIs of the media files to delete.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('createDeleteRequestDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    const fetchResult = await phAccessHelper.getAssets(fetchOptions);
    var asset = await fetchResult.getFirstObject();
  } catch (err) {
    console.info('fetch failed, message =', err);
  }

  if (asset == undefined) {
    console.error('asset not exist');
    return;
  }
  try {
    await phAccessHelper.createDeleteRequest([asset.uri]);
    console.info('createDeleteRequest successfully');
  } catch (err) {
    console.error('createDeleteRequest failed with error: ' + err);
  }
}
```

### release

release(callback: AsyncCallback&lt;void&gt;): void

Releases the **PhotoAccessHelper** instance. This API uses an asynchronous callback to return the result.
Call this API when the APIs of the **PhotoAccessHelper** instance are no longer used.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description                |
| -------- | ------------------------- | ---- | -------------------- |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**Example**

```ts
async function example() {
  console.info('releaseDemo');
  phAccessHelper.release((err) => {
    if (err != undefined) {
      console.error('release failed. message = ', err);
    } else {
      console.info('release ok.');
    }
  });
}
```

### release

release(): Promise&lt;void&gt;

Releases the **PhotoAccessHelper** instance. This API uses a promise to return the result.
Call this API when the APIs of the **PhotoAccessHelper** instance are no longer used.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type               | Description                             |
| ------------------- | --------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**Example**

```ts
async function example() {
  console.info('releaseDemo');
  try {
    await phAccessHelper.release();
    console.info('release ok.');
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

## PhotoAsset

Provides APIs for encapsulating file asset attributes.

### Attributes

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name                     | Type                    | Readable| Writable| Description                                                  |
| ------------------------- | ------------------------ | ---- | ---- | ------------------------------------------------------ |
| uri                       | string                   | Yes  | No  | File asset URI, for example, **file://media/image/2**.        |
| photoType   | [PhotoType](#phototype) | Yes  | No  | Type of the file.                                              |
| displayName               | string                   | Yes  | No  | File name, including the file name extension, to display.                                |

### get

get(member: string): MemberType;

Obtains a **PhotoAsset** member parameter.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                       | Mandatory  | Description   |
| -------- | ------------------------- | ---- | ----- |
| member | string | Yes   | Name of the member parameter to obtain. Except **uri**, **photoType**, and **displayName**, you need to pass in [PhotoKeys](#photokeys) in **fetchColumns** in **get()**. For example, to obtain the title attribute, set **fetchColumns: ['title']**.|

**Return value**

| Type               | Description                             |
| ------------------- | --------------------------------- |
| [MemberType](#membertype) | Returns the **PhotoAsset** member parameter obtained.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401    | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('photoAssetGetDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: ['title'],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let photoAsset = await fetchResult.getFirstObject();
    let title = photoAccessHelper.PhotoKeys.TITLE;
    let photoAssetTitle = photoAsset.get(title.toString());
    console.info('photoAsset Get photoAssetTitle = ', photoAssetTitle);
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

### set

set(member: string, value: string): void;

Sets a **PhotoAsset** member parameter.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                       | Mandatory  | Description   |
| -------- | ------------------------- | ---- | ----- |
| member | string | Yes   | Name of the member parameter to set. For example, **[PhotoKeys](#photokeys).TITLE**.|
| value | string | Yes   | Member parameter to set. Only the value of **[PhotoKeys](#photokeys).TITLE** can be modified.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401    | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('photoAssetSetDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: ['title'],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let photoAsset = await fetchResult.getFirstObject();
    let title = photoAccessHelper.PhotoKeys.TITLE.toString();
    photoAsset.set(title, 'newTitle');
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

### commitModify

commitModify(callback: AsyncCallback&lt;void&gt;): void

Commits the modification on the file metadata to the database. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                       | Mandatory  | Description   |
| -------- | ------------------------- | ---- | ----- |
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401    | if values to commit is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('commitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: ['title'],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getFirstObject();
  let title = photoAccessHelper.PhotoKeys.TITLE.toString();
  let photoAssetTitle = photoAsset.get(title);
  console.info('photoAsset get photoAssetTitle = ', photoAssetTitle);
  photoAsset.set(title, 'newTitle2');
  photoAsset.commitModify((err) => {
    if (err == undefined) {
      let newPhotoAssetTitle = photoAsset.get(title);
      console.info('photoAsset get newPhotoAssetTitle = ', newPhotoAssetTitle);
    } else {
      console.error('commitModify failed, message =', err);
    }
  });
}
```

### commitModify

commitModify(): Promise&lt;void&gt;

Commits the modification on the file metadata to the database. This API uses a promise to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type                 | Description        |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401    | if values to commit is invalid.         |

**Example** 

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('commitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: ['title'],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getFirstObject();
  let title = photoAccessHelper.PhotoKeys.TITLE.toString();
  let photoAssetTitle = photoAsset.get(title);
  console.info('photoAsset get photoAssetTitle = ', photoAssetTitle);
  photoAsset.set(title, 'newTitle3');
  try {
    await photoAsset.commitModify();
    let newPhotoAssetTitle = photoAsset.get(title);
    console.info('photoAsset get newPhotoAssetTitle = ', newPhotoAssetTitle);
  } catch (err) {
    console.error('release failed. message = ', err);
  }
}
```

### open

open(mode: string, callback: AsyncCallback&lt;number&gt;): void

Opens this file asset. This API uses an asynchronous callback to return the result.

**NOTE**<br>The write operations are mutually exclusive. After a write operation is complete, you must call **close** to close the file.

**System API**: This is a system API.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO or ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                         | Mandatory  | Description                                 |
| -------- | --------------------------- | ---- | ----------------------------------- |
| mode     | string                      | Yes   | File open mode, which can be **r** (read-only), **w** (write-only), or **rw** (read-write).|
| callback | AsyncCallback&lt;number&gt; | Yes   | Callback invoked to return the file descriptor of the file opened.                           |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
async function example() {
  console.info('openDemo');
   let testFileName = 'testFile' + Date.now() + '.jpg';
  const photoAsset = await phAccessHelper.createAsset(testFileName);
  photoAsset.open('rw', (err, fd) => {
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error('File err' + err);
    }
  });
}
```

### open

open(mode: string): Promise&lt;number&gt;

Opens this file asset. This API uses a promise to return the result.

**NOTE**<br>The write operations are mutually exclusive. After a write operation is complete, you must call **close** to close the file.

**System API**: This is a system API.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO or ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name | Type    | Mandatory  | Description                                 |
| ---- | ------ | ---- | ----------------------------------- |
| mode | string | Yes   | File open mode, which can be **r** (read-only), **w** (write-only), or **rw** (read-write).|

**Return value**

| Type                   | Description           |
| --------------------- | ------------- |
| Promise&lt;number&gt; | Promise used to return the file descriptor of the file opened.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
async function example() {
  console.info('openDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    const photoAsset = await phAccessHelper.createAsset(testFileName);
    let fd = await photoAsset.open('rw');
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error(' open File fail');
    }
  } catch (err) {
    console.error('open Demo err' + err);
  }
}
```

### getReadOnlyFd

getReadOnlyFd(callback: AsyncCallback&lt;number&gt;): void

Opens this file in read-only mode. This API uses an asynchronous callback to return the result.

**NOTE**<br>After the read operation is complete, call **close** to close the file.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                         | Mandatory  | Description                                 |
| -------- | --------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback&lt;number&gt; | Yes   | Callback invoked to return the file descriptor of the file opened.                           |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
async function example() {
  console.info('getReadOnlyFdDemo');
   let testFileName = 'testFile' + Date.now() + '.jpg';
  const photoAsset = await phAccessHelper.createAsset(testFileName);
  photoAsset.getReadOnlyFd((err, fd) => {
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error('File err' + err);
    }
  });
}
```

### getReadOnlyFd

getReadOnlyFd(): Promise&lt;number&gt;

Opens this file in read-only mode. This API uses a promise to return the result.

**NOTE**<br>After the read operation is complete, call **close** to close the file.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type                   | Description           |
| --------------------- | ------------- |
| Promise&lt;number&gt; | Promise used to return the file descriptor of the file opened.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
async function example() {
  console.info('getReadOnlyFdDemo');
  try {
    let testFileName = 'testFile' + Date.now() + '.jpg';
    const photoAsset = await phAccessHelper.createAsset(testFileName);
    let fd = await photoAsset.getReadOnlyFd();
    if (fd != undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error(' open File fail');
    }
  } catch (err) {
    console.error('open Demo err' + err);
  }
}
```

### close

close(fd: number, callback: AsyncCallback&lt;void&gt;): void

Closes a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                       | Mandatory  | Description   |
| -------- | ------------------------- | ---- | ----- |
| fd       | number                    | Yes   | File descriptor of the file to close.|
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('closeDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    const photoAsset = await fetchResult.getFirstObject();
    let fd = await photoAsset.open('rw');
    console.info('file fd', fd);
    photoAsset.close(fd, (err) => {
      if (err == undefined) {
        console.info('asset close succeed.');
      } else {
        console.error('close failed, message = ' + err);
      }
    });
  } catch (err) {
    console.error('close failed, message = ' + err);
  }
}
```

### close

close(fd: number): Promise&lt;void&gt;

Closes a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name | Type    | Mandatory  | Description   |
| ---- | ------ | ---- | ----- |
| fd   | number | Yes   | File descriptor of the file to close.|

**Return value**

| Type                 | Description        |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('closeDemo');
  try {
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    const asset = await fetchResult.getFirstObject();
    let fd = await asset.open('rw');
    console.info('file fd', fd);
    await asset.close(fd);
    console.info('asset close succeed.');
  } catch (err) {
    console.error('close failed, message = ' + err);
  }
}
```

### getThumbnail

getThumbnail(callback: AsyncCallback&lt;image.PixelMap&gt;): void

Obtains the thumbnail of this file. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                                 | Mandatory  | Description              |
| -------- | ----------------------------------- | ---- | ---------------- |
| callback | AsyncCallback&lt;[image.PixelMap](js-apis-image.md#pixelmap7)&gt; | Yes   | Callback invoked to return the PixelMap of the thumbnail.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getThumbnailDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail((err, pixelMap) => {
    if (err == undefined) {
      console.info('getThumbnail successful ' + pixelMap);
    } else {
      console.error('getThumbnail fail', err);
    }
  });
}
```

### getThumbnail

getThumbnail(size: image.Size, callback: AsyncCallback&lt;image.PixelMap&gt;): void

Obtains the file thumbnail of the given size. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name     | Type                                 | Mandatory  | Description              |
| -------- | ----------------------------------- | ---- | ---------------- |
| size     | [image.Size](js-apis-image.md#size) | Yes   | Size of the thumbnail.           |
| callback | AsyncCallback&lt;[image.PixelMap](js-apis-image.md#pixelmap7)&gt; | Yes   | Callback invoked to return the PixelMap of the thumbnail.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getThumbnailDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let size = { width: 720, height: 720 };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail(size, (err, pixelMap) => {
    if (err == undefined) {
      console.info('getThumbnail successful ' + pixelMap);
    } else {
      console.error('getThumbnail fail', err);
    }
  });
}
```

### getThumbnail

getThumbnail(size?: image.Size): Promise&lt;image.PixelMap&gt;

Obtains the file thumbnail of the given size. This API uses a promise to return the result.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name | Type            | Mandatory  | Description   |
| ---- | -------------- | ---- | ----- |
| size | [image.Size](js-apis-image.md#size) | No   | Size of the thumbnail.|

**Return value**

| Type                           | Description                   |
| ----------------------------- | --------------------- |
| Promise&lt;[image.PixelMap](js-apis-image.md#pixelmap7)&gt; | Promise used to return the PixelMap of the thumbnail.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getThumbnailDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let size = { width: 720, height: 720 };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail(size).then((pixelMap) => {
    console.info('getThumbnail successful ' + pixelMap);
  }).catch((err) => {
    console.error('getThumbnail fail' + err);
  });
}
```

### setFavorite

setFavorite(favoriteState: boolean, callback: AsyncCallback&lt;void&gt;): void

Favorites or unfavorites this file. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name       | Type                       | Mandatory  | Description                                |
| ---------- | ------------------------- | ---- | ---------------------------------- |
| favoriteState | boolean                   | Yes   | Operation to perform. The value **true** means to favorite the file asset, and **false** means the opposite.|
| callback   | AsyncCallback&lt;void&gt; | Yes   | Callback that returns no value.                             |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setFavoriteDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setFavorite(true, (err) => {
    if (err == undefined) {
      console.info('favorite successfully');
    } else {
      console.error('favorite failed with error:' + err);
    }
  });
}
```

### setFavorite

setFavorite(favoriteState: boolean): Promise&lt;void&gt;

Favorites or unfavorites this file asset. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name       | Type     | Mandatory  | Description                                |
| ---------- | ------- | ---- | ---------------------------------- |
| favoriteState | boolean | Yes   | Operation to perform. The value **true** means to favorite the file asset, and **false** means the opposite.|

**Return value**

| Type                 | Description        |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setFavoriteDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setFavorite(true).then(function () {
    console.info('setFavorite successfully');
  }).catch(function (err) {
    console.error('setFavorite failed with error:' + err);
  });
}
```

### setHidden

setHidden(hiddenState: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets this file to hidden state. This API uses an asynchronous callback to return the result.

Private files are stored in the private album. After obtaining private files from the private album, users can set **hiddenState** to **false** to remove them from the private album.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name       | Type                       | Mandatory  | Description                                |
| ---------- | ------------------------- | ---- | ---------------------------------- |
| hiddenState | boolean                   | Yes   | Whether to set a file to hidden state. The value **true** means to hide the file; the value **false** means the opposite.|
| callback   | AsyncCallback&lt;void&gt; | Yes   | Callback that returns no value.                             |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setHiddenDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setHidden(true, (err) => {
    if (err == undefined) {
      console.info('setHidden successfully');
    } else {
      console.error('setHidden failed with error:' + err);
    }
  });
}
```

### setHidden

setHidden(hiddenState: boolean): Promise&lt;void&gt;

Sets this file asset to hidden state. This API uses a promise to return the result.

Private files are stored in the private album. After obtaining private files from the private album, users can set **hiddenState** to **false** to remove them from the private album.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name       | Type     | Mandatory  | Description                                |
| ---------- | ------- | ---- | ---------------------------------- |
| hiddenState | boolean | Yes   | Whether to set a file to hidden state. The value **true** means to hide the file; the value **false** means the opposite.|

**Return value**

| Type                 | Description        |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // Restore a file from a hidden album. Before the operation, ensure that the file exists in the hidden album.
  console.info('setHiddenDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let albumList = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.HIDDEN);
  const album = await albumList.getFirstObject();
  let fetchResult = await album.getAssets(fetchOption);
  const asset = await fetchResult.getFirstObject();
  asset.setHidden(false).then(() => {
    console.info('setHidden successfully');
  }).catch((err) => {
    console.error('setHidden failed with error:' + err);
  });
}
```

## FetchResult

Provides APIs to manage the file retrieval result.

### getCount

getCount(): number

Obtains the total number of files in the result set.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type    | Description      |
| ------ | -------- |
| number | Returns the total number of files obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getCountDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const fetchCount = fetchResult.getCount();
  console.info('fetchCount = ', fetchCount);
}
```

### isAfterLast

isAfterLast(): boolean

Checks whether the cursor is in the last row of the result set.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type     | Description                                |
| ------- | ---------------------------------- |
| boolean | Returns **true** if the cursor is in the last row of the result set; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  const fetchCount = fetchResult.getCount();
  console.info('count:' + fetchCount);
  let photoAsset = await fetchResult.getLastObject();
  if (fetchResult.isAfterLast()) {
    console.info('photoAsset isAfterLast displayName = ', photoAsset.displayName);
  } else {
    console.info('photoAsset  not isAfterLast ');
  }
}
```

### close

close(): void

Releases this **FetchFileResult** instance to invalidate it. After this instance is released, the APIs in this instance cannot be invoked.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('fetchResultCloseDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    fetchResult.close();
    console.info('close succeed.');
  } catch (err) {
    console.error('close fail. message = ' + err);
  }
}
```

### getFirstObject

getFirstObject(callback: AsyncCallback&lt;T&gt;): void

Obtains the first file asset in the result set. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                                         | Mandatory| Description                                       |
| -------- | --------------------------------------------- | ---- | ------------------------------------------- |
| callback | AsyncCallback&lt;T&gt; | Yes  | Callback invoked to return the first file asset obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getFirstObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getFirstObject((err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error('photoAsset failed with err:' + err);
    }
  });
}
```

### getFirstObject

getFirstObject(): Promise&lt;T&gt;

Obtains the first file asset in the result set. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type                                   | Description                      |
| --------------------------------------- | -------------------------- |
| Promise&lt;T&gt; | Promise used to return the first object in the result set.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getFirstObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getFirstObject();
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getNextObject

 getNextObject(callback: AsyncCallback&lt;T&gt;): void

Obtains the next file asset in the result set. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name   | Type                                         | Mandatory| Description                                     |
| --------- | --------------------------------------------- | ---- | ----------------------------------------- |
| callbacke | AsyncCallback&lt;T&gt; | Yes  | Callback invoked to return the next file asset.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getNextObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  await fetchResult.getFirstObject();
  if (fetchResult.isAfterLast()) {
    fetchResult.getNextObject((err, photoAsset) => {
      if (photoAsset != undefined) {
        console.info('photoAsset displayName: ', photoAsset.displayName);
      } else {
        console.error('photoAsset failed with err: ' + err);
      }
    });
  }
}
```

### getNextObject

 getNextObject(): Promise&lt;T&gt;

Obtains the next file asset in the result set. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise used to return the next object in the result set.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getNextObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  await fetchResult.getFirstObject();
  if (fetchResult.isAfterLast()) {
    let photoAsset = await fetchResult.getNextObject();
    console.info('photoAsset displayName: ', photoAsset.displayName);
  }
}
```

### getLastObject

getLastObject(callback: AsyncCallback&lt;T&gt;): void

Obtains the last file asset in the result set. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                                         | Mandatory| Description                       |
| -------- | --------------------------------------------- | ---- | --------------------------- |
| callback | AsyncCallback&lt;T&gt; | Yes  | Callback invoked to return the last file asset obtained.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getLastObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getLastObject((err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error('photoAsset failed with err: ' + err);
    }
  });
}
```

### getLastObject

getLastObject(): Promise&lt;T&gt;

Obtains the last file asset in the result set. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise used to return the last object in the result set.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042   | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getLastObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getLastObject();
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getObjectByPosition

getObjectByPosition(index: number, callback: AsyncCallback&lt;T&gt;): void

Obtains a file asset with the specified index in the result set. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name      | Type                                      | Mandatory  | Description                |
| -------- | ---------------------------------------- | ---- | ------------------ |
| index    | number                                   | Yes   | Index of the file asset to obtain. The value starts from **0**.    |
| callback | AsyncCallback&lt;T&gt; | Yes   | Callback invoked to return the file asset obtained.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401    | if type index is not number.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getObjectByPositionDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getObjectByPosition(0, (err, photoAsset) => {
    if (photoAsset != undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error('photoAsset failed with err: ' + err);
    }
  });
}
```

### getObjectByPosition

getObjectByPosition(index: number): Promise&lt;T&gt;

Obtains a file asset with the specified index in the result set. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name   | Type    | Mandatory  | Description            |
| ----- | ------ | ---- | -------------- |
| index | number | Yes   | Index of the file asset to obtain. The value starts from **0**.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise used to return the file asset obtained.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type index is not number.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getObjectByPositionDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAsset = await fetchResult.getObjectByPosition(0);
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getAllObjects

getAllObjects(callback: AsyncCallback&lt;Array&lt;T&gt;&gt;): void

Obtains all the file assets in the result set. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                                         | Mandatory| Description                                       |
| -------- | --------------------------------------------- | ---- | ------------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;T&gt;&gt; | Yes  | Callback invoked to return an array of all file assets in the result set.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAllObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getAllObjects((err, photoAssetList) => {
    if (photoAssetList != undefined) {
      console.info('photoAssetList length: ', photoAssetList.length);
    } else {
      console.error('photoAssetList failed with err:' + err);
    }
  });
}
```

### getAllObjects

getAllObjects(): Promise&lt;Array&lt;T&gt;&gt;

Obtains all the file assets in the result set. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type                                   | Description                      |
| --------------------------------------- | -------------------------- |
| Promise&lt;Array&lt;T&gt;&gt; | Promise used to return an array of all file assets in the result set.|

**Error codes**

For details about the error codes, see [File Management Error Codes](../errorcodes/errorcode-filemanagement.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 13900042    | Unknown error.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAllObjectDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult = await phAccessHelper.getAssets(fetchOption);
  let photoAssetList = await fetchResult.getAllObjects();
  console.info('photoAssetList length: ', photoAssetList.length);
}
```

## Album

Provides APIs to manage albums.

### Attributes

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name          | Type   | Readable  | Writable | Description  |
| ------------ | ------ | ---- | ---- | ------- |
| albumType | [AlbumType]( #albumtype) | Yes   | No   | Type of the album.   |
| albumSubtype | [AlbumSubtype]( #albumsubtype) | Yes   | No  | Subtype of the album.   |
| albumName | string | Yes   | Yes for a user album; no for a system album.  | Name of the album.   |
| albumUri | string | Yes   | No   | URI of the album.  |
| count | number | Yes   | No   |  Number of files in the album.|
| coverUri | string | Yes   | No   | URI of the cover file of the album.|

### getAssets

getAssets(options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;PhotoAsset&gt;&gt;): void;

Obtains image and video assets. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| options | [FetchOptions](#fetchoptions) | Yes  | Options for fetching the album files.|
| callback | AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Yes  | Callback invoked to return the image and video assets obtained.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumGetPhotoAssetsDemoCallback');

  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.getAssets(fetchOption, (err, albumFetchResult) => {
    if (albumFetchResult != undefined) {
      console.info('album getAssets successfully, getCount: ' + albumFetchResult.getCount());
    } else {
      console.error('album getAssets failed with error: ' + err);
    }
  });
}
```

### getAssets

getAssets(options: FetchOptions): Promise&lt;FetchResult&lt;PhotoAsset&gt;&gt;;

Obtains image and video assets. This API uses a promise to return the result.

**Required permissions**: ohos.permission.READ_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| options | [FetchOptions](#fetchoptions) | Yes  | Options for fetching the album files.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Promise used to return the image and video assets obtained.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if type options is not FetchOptions.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumGetPhotoAssetsDemoPromise');

  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  let fetchOption = {
    fetchColumns: [],
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.getAssets(fetchOption).then((albumFetchResult) => {
    console.info('album getPhotoAssets successfully, getCount: ' + albumFetchResult.getCount());
  }).catch((err) => {
    console.error('album getPhotoAssets failed with error: ' + err);
  });
}
```

### commitModify

commitModify(callback: AsyncCallback&lt;void&gt;): void;

Commits the modification on the album attributes to the database. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if value to modify is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumCommitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.albumName = 'hello';
  album.commitModify((err) => {
    if (err != undefined) {
      console.error('commitModify failed with error: ' + err);
    } else {
      console.info('commitModify successfully');
    }
  });
}
```

### commitModify

commitModify(): Promise&lt;void&gt;;

Commits the modification on the album attributes to the database. This API uses a promise to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Return value**

| Type                 | Description          |
| ------------------- | ------------ |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if value to modify is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumCommitModifyDemo');
  let predicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions = {
    predicates: predicates
  };
  const albumList = await phAccessHelper.getAlbums(albumFetchOptions);
  const album = await albumList.getFirstObject();
  album.albumName = 'hello';
  album.commitModify().then(() => {
    console.info('commitModify successfully');
  }).catch((err) => {
    console.error('commitModify failed with error: ' + err);
  });
}
```

### addAssets

addAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

Adds image and video assets to an album. Before the operation, ensure that the image and video assets to add and the album exist. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image and video assets to add.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('addAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.addAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album addAssets successfully');
      } else {
        console.error('album addAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('addAssetsDemoCallback failed with error: ' + err);
  }
}
```

### addAssets

addAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

Adds image and video assets to an album. Before the operation, ensure that the image and video assets to add and the album exist. This API uses a promise to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image and video assets to add.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('addAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await phAccessHelper.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.addAssets([asset]).then(() => {
      console.info('album addAssets successfully');
    }).catch((err) => {
      console.error('album addAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('addAssetsDemoPromise failed with error: ' + err);
  }
}
```

### removeAssets

removeAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

Removes image and video assets from an album. The album and file resources must exist. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image and video assets to remove.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('removeAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.removeAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album removeAssets successfully');
      } else {
        console.error('album removeAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('removeAssetsDemoCallback failed with error: ' + err);
  }
}
```

### removeAssets

removeAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

Removes image and video assets from an album. The album and file resources must exist. This API uses a promise to return the result.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image and video assets to remove.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 401   | if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('removeAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.removeAssets([asset]).then(() => {
      console.info('album removeAssets successfully');
    }).catch((err) => {
      console.error('album removeAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('removeAssetsDemoPromise failed with error: ' + err);
  }
}
```

### recoverAssets

recoverAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

Recovers image or video assets from the trash. Before the operation, ensure that the image or video assets exist in the trash. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image or video assets to recover.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   |  if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('recoverAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.recoverAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album recoverAssets successfully');
      } else {
        console.error('album recoverAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('recoverAssetsDemoCallback failed with error: ' + err);
  }
}
```

### recoverAssets

recoverAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

Recovers image or video assets from the trash. Before the operation, ensure that the image or video assets exist in the trash. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image or video assets to recover.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   |  if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('recoverAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.recoverAssets([asset]).then(() => {
      console.info('album recoverAssets successfully');
    }).catch((err) => {
      console.error('album recoverAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('recoverAssetsDemoPromise failed with error: ' + err);
  }
}
```

### deleteAssets

deleteAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void;

Deletes image or video assets from the trash. Before the operation, ensure that the image or video assets exist in the trash. This API uses an asynchronous callback to return the result.

**CAUTION**<br>This operation is irreversible. The file assets deleted cannot be restored. Exercise caution when performing this operation.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image or video assets to delete.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   | if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('deleteAssetsDemoCallback');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.deleteAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album deleteAssets successfully');
      } else {
        console.error('album deleteAssets failed with error: ' + err);
      }
    });
  } catch (err) {
    console.error('deleteAssetsDemoCallback failed with error: ' + err);
  }
}
```

### deleteAssets

deleteAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;;

Deletes image or video assets from the trash. Before the operation, ensure that the image or video assets exist in the trash. This API uses a promise to return the result.

**CAUTION**<br>This operation is irreversible. The file assets deleted cannot be restored. Exercise caution when performing this operation.

**System API**: This is a system API.

**Required permissions**: ohos.permission.WRITE_IMAGEVIDEO

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

**Parameters**

| Name  | Type                     | Mandatory| Description      |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | Yes  | Array of the image or video assets to delete.|

**Return value**

| Type                                   | Description             |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcodes/errorcode-universal.md).

| ID| Error Message|
| -------- | ---------------------------------------- |
| 202   | Called by non-system application.                |
| 401   | if PhotoAssets is invalid.         |

**Example**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('deleteAssetsDemoPromise');
    let predicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album = await albumFetchResult.getFirstObject();
    let fetchResult = await album.getAssets(fetchOption);
    let asset = await fetchResult.getFirstObject();
    album.deleteAssets([asset]).then(() => {
      console.info('album deleteAssets successfully');
    }).catch((err) => {
      console.error('album deleteAssets failed with error: ' + err);
    });
  } catch (err) {
    console.error('deleteAssetsDemoPromise failed with error: ' + err);
  }
}
```

## MemberType

Enumerates the member types.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name |  Type|  Readable |  Writable |  Description |
| ----- |  ---- |  ---- |  ---- |  ---- |
| number |  number | Yes| Yes| The member is a number.|
| string |  string | Yes| Yes| The member is a string.|
| boolean |  boolean | Yes| Yes| The member is a Boolean value.|

## PhotoType

Enumerates media file types.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name |  Value|  Description|
| ----- |  ---- |  ---- |
| IMAGE |  1 |  Image.|
| VIDEO |  2 |  Video.|

## PhotoSubtype

Enumerates the [PhotoAsset](#photoasset) types.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name |  Value|  Description|
| ----- |  ---- |  ---- |
| DEFAULT |  0 |  Default (photo) type.|
| SCREENSHOT |  1 |  Screenshot and screen recording file.|

## PositionType

Enumerates the file locations.

**System API**: This is a system API.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name |  Value|  Description|
| ----- |  ---- |  ---- |
| LOCAL |  1 << 0 |  Stored only on a local device.|
| CLOUD |  1 << 1 |  Stored only on the cloud.|

## AlbumType

Enumerates the album types.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name |  Value|  Description|
| ----- |  ---- |  ---- |
| USER |  0 |  User album.|
| SYSTEM |  1024 |  System album.|

## AlbumSubtype

Enumerate the album subtypes.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name |  Value|  Description|
| ----- |  ---- |  ---- |
| USER_GENERIC |  1 |  User album.|
| FAVORITE |  1025 |  Favorites.|
| VIDEO |  1026 |  Video album.|
| HIDDEN |  1027 |  Hidden album. **System API**: This is a system API.|
| TRASH |  1028 |  Trash. **System API**: This is a system API.|
| SCREENSHOT |  1029 |  Album for screenshots and screen recording files. **System API**: This is a system API.|
| CAMERA |  1030 |  Album for photos and videos taken by the camera. **System API**: This is a system API.|
| ANY |  2147483647 |  Any album.|

## PhotoKeys

Defines the key information about an image or video file.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name         | Value             | Description                                                      |
| ------------- | ------------------- | ---------------------------------------------------------- |
| URI           | 'uri'                 | URI of the file.                                                  |
| PHOTO_TYPE    | 'media_type'           | Type of the file.                                             |
| DISPLAY_NAME  | 'display_name'        | File name displayed.                                                  |
| SIZE          | 'size'                | File size.                                                  |
| DATE_ADDED    | 'date_added'          | Date when the file was added. The value is the number of seconds elapsed since the Epoch time.            |
| DATE_MODIFIED | 'date_modified'       | Date when the file content (not the file name) was last modified. The value is the number of seconds elapsed since the Epoch time.|
| DURATION      | 'duration'            | Duration, in ms.                                   |
| WIDTH         | 'width'               | Image width, in pixels.                                   |
| HEIGHT        | 'height'              | Image height, in pixels.                                     |
| DATE_TAKEN    | 'date_taken'          | Date when the file (photo) was taken. The value is the number of seconds elapsed since the Epoch time.               |
| ORIENTATION   | 'orientation'         | Orientation of the image file.                                            |
| FAVORITE      | 'is_favorite'            | Whether the file is added to favorites.                                                   |
| TITLE         | 'title'               | Title in the file.                                                  |
| POSITION  | 'position'            | File location type. **System API**: This is a system API.                              |
| DATE_TRASHED  | 'date_trashed'  | Date when the file was deleted. The value is the number of seconds between the time when the file is deleted and January 1, 1970. **System API**: This is a system API.                |
| HIDDEN  | 'hidden'            | Whether the file is hidden. **System API**: This is a system API.                              |

## AlbumKeys

Enumerates the key album attributes.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name         | Value             | Description                                                      |
| ------------- | ------------------- | ---------------------------------------------------------- |
| URI           | 'uri'                 | URI of the album.                                                  |
| ALBUM_NAME    | 'album_name'          | Name of the album.                                                  |

## PhotoCreateOptions

Defines the options for creating an image or video asset.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name                  | Type               | Mandatory| Description                                             |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
| subtype           | [PhotoSubtype](#photosubtype) | No | Subtype of the image or video. **System API**: This is a system API. |

## CreateOptions

Defines the options for creating an image or video asset.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name                  | Type               | Mandatory| Description                                             |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
| title           | string | No | Title of the image or video. |

## FetchOptions

Defines the options for fetching media files.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name                  | Type               | Readable| Writable| Description                                             |
| ---------------------- | ------------------- | ---- |---- | ------------------------------------------------ |
| fetchColumns           | Array&lt;string&gt; | Yes  | Yes  | Column names used for retrieval. If this parameter is left empty, the media files are fetched by **uri**, **name**, and **photoType** by default. The specific field names are subject to the definition of the search object. Example:<br>fetchColumns: ['uri', 'title']|
| predicates           | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md) | Yes  | Yes  | Predicates that specify the fetch criteria.|

## ChangeData

Defines the return value of the listener callback.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name   | Type                       | Readable| Writable| Description                                                        |
| ------- | --------------------------- | ---- | ---- | ------------------------------------------------------------ |
| type    | [NotifyType](#notifytype) | Yes  | No  | Notification type.                                      |
| uris    | Array&lt;string&gt;         | Yes  | No  | All URIs with the same [NotifyType](#notifytype), which can be **PhotoAsset** or **Album**.|
| extraUris | Array&lt;string&gt;         | Yes  | No  | URIs of the changed files in the album.                                   |

## NotifyType

Enumerates the notification event types.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name                     | Value  | Description                            |
| ------------------------- | ---- | -------------------------------- |
| NOTIFY_ADD                | 0    | A file asset or album is added.    |
| NOTIFY_UPDATE             | 1    | A file asset or album is updated.    |
| NOTIFY_REMOVE             | 2    | A file asset or album is removed.    |
| NOTIFY_ALBUM_ADD_ASSET    | 3    | A file asset is added to the album.|
| NOTIFY_ALBUM_REMOVE_ASSET | 4    | A file asset is removed from the album.|

## DefaultChangeUri

Enumerates the **DefaultChangeUri** subtypes.

**System capability**: SystemCapability.FileManagement.PhotoAccessHelper.Core

| Name             | Value                     | Description                                                        |
| ----------------- | ----------------------- | ------------------------------------------------------------ |
| DEFAULT_PHOTO_URI | 'file://media/Photo'      | Default **PhotoAsset** URI. The **PhotoAsset** change notifications are received based on this parameter and **forSubUri{true}**.|
| DEFAULT_ALBUM_URI | 'file://media/PhotoAlbum' | Default album URI. Album change notifications are received based on this parameter and **forSubUri{true}**. |
