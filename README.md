# kintone-typelify

Type definition for kintone customize and 
Type defenition generation tool from kitone form settings.


## Write kintone customize with TypeScript

In kintone JavaScript customize, there are functions which is defined in kintone.
When user try to write JavaScripot customize, there are no defenitions on typescript compile context.

So This tools has `kintone.d.ts` files which has a global function definition in TypeScripot syntax manner. And then, you can write JavaScripot customize with TypeScript.

And This tools also contains comand-line tool for type defenition gerarator which 
uses kintone form settings api.

## How to generate kintone-typelify

you can generate `sample-field.d.ts` like below:

```bash
kintone-typelify --host http://***.cybozu.com \
                 -u username \
                 -p password \
                 --app-id 12 \
                 --type-name SampleFields
                 --namespace company.name.types \
                 -o sample-fields.d.ts
```

kintone-typelify generates record field definition from kintone form settings.
And from this command line option, record field type definition(`company.name.types.SampleFields`) 
is defined in `sample-fields.d.ts`.

### demo mode
If you won't have a kintone, you can try with demo mode. 
you can generate demo type defenition like below:

```bash
kintone-typelify --demo
```

kintone-typelify generates demo record field defenition from demo data.
record field type definition(`kintone.types.Fields`)  is defined in `fields.d.ts`

### command line options
Command line options like below:

```
Options:
  -V, --version              output the version number
  --host [host]              
  -u, --username [username]  
  -p, --password [password]  
  --app-id [appId]           
  --type-name [typeName]     type name to be generated (default: "Fields")
  --namespace [namespace]    namespace of type to be generated (default: "kintone.types")
  --demo                     Generate Type definition from demo data.
  -o, --output [output]      output file name (default: "fields.d.ts")
  -h, --help                 output usage information
```

### Write Kintone JavaScript Customize with TypeScript

```typescript
/// <reference path="kintone.d.ts" />
/// <reference path="fields.d.ts" />


kintone.events.on("app.record.create.show", (event: kintone.types.events.record.create.show.Event) => {
    const type = event.record.Table_3.value[0].value;
});
```

you can compile `.ts` files with `tsc` command!


In `kintone.d.ts`, There are definitions of kintone built-in functions.
And in `fields.d.ts` is a record field defenition generate by `kintone-typelify`.
