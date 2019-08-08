
# Passing file list to Chonky

The `FileBrowser` component accepts a prop called `files`, which should be an array of file objects. It also the only
required component, so the most basic Chonky usage could look like this:
 
```typescript jsx
export const ExampleComponent = () => {
    const myFiles = [];
    return <FileBrowser files={myFiles}/>
}
```

## File object type

Each object in the `files` array should describe a file. To be precise, each object should satisfy the `FileData` 
type. The full definition of `FileData` type can be seen below (taken from
[TypeScript definitions](https://github.com/TimboKZ/Chonky/blob/master/src/typedef.ts)).

```typescript
// Required properties are marked with `!!`
export type FileData = {
    id: string; // !! String that uniquely identifies the file

    base: string; // !! Full name, e.g. `MyImage.jpg`
    name: string; // !! Name without extension, e.g. `MyImage`
    ext: string; // !! Extension, e.g. `.jpg`

    isDir: boolean; // !! Is a directory
    isHidden?: boolean; // Is a hidden file, default: false
    isSymLink?: boolean; // Is a symlink, default: false
    openable?: boolean // Can be opened, default: true
    selectable?: boolean, // Can be selected, default: true

    size?: number; // File size in bytes
    modDate?: Date; // Last change date

    parentId?: string; // ID of the parent folder
    childrenIds?: string[]; // An array of IDs of children (only for folders)
}
``` 

The main idea to take away here is that each file object must, at the very least, have the following 5 properties:
`id`, `base`, `name`, `ext` and `isDir`. All of the other properties are optional, but they could significantly 
improve user experience if they are present.

### Custom file properties

You are also free to add custom properties to objects, e.g. `file.encryption = 'RSA'`. `FileBrowser` will just 
ignore them, but they might be useful for your action handlers.

### Loading placeholders

If you want to have a nice loading animation, you can pass several `null` values instead of a file object. For example,
if you know that a directory has 6 files in total, but only 2 of them were loaded, your `files` array could look like
this:
```js
const files = [myFile1, myFile2, null, null, null, null];
``` 

This configuration will render 2 files and 4 loading placeholders. Check the examples below to get a better idea.

## Example with different files

## Generating file descriptions


## Loading placeholders



MIT © [Tim Kuzhagaliyev](https://github.com/TimboKZ), 2019