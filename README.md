# asset-cli
`asset-cli` is a command-line tool that serializes and manages data tables in protobuf format for sharing static data between layers in the server-client model.

![screenshot of asset-cli](https://user-images.githubusercontent.com/12756996/123517170-77706000-d6da-11eb-9610-3b3daa5a9db4.png)

## Pre requirement
| Dependence        | Version           |
| ----------------- | ----------------- |
| JDK               | 15.+              |
| protoc            | 3.+               |

The above dependencies are required to build and run the project.

## Installation

I will guide you after the project packaging work

## Usage examples

```
asset gen-proto --package=com.sample.vo.asset --scope=CLIENT --schema_dist=schema/ sample/
```

The `.proto` file is created by parsing the `*.xlsx` datasheet in the `sample/` path to the client and share according to the `-scope` option.  
`--package` option is the package name of the proto file to be created

---

```
asset gen-struct --java_out=schema/proto schema/
```

The `--java_out` option is that of `*_out` arguments in `protoc`.  
Compile the `*.proto` file in the desired language and output it to the `schema/` path.  
In this case, it compiles to the `Java` language.

---

```
asset serialize --dist=data/ --package=com.sample.vo.asset --scope=CLIENT --struct=schema/proto sample/
```

Serialize the `*.xlsx` datasheets in `sample/` using the structure created by the `gen-struct` command.

---

```
asset integrity --package=com.sample.vo.asset sample/
```

Check the consistency of the dependency relationship between data tables with the link column value defined in the data sheet.  
For example, if the link value of `FooData.columnB` is `BarData`, check whether the values used in `FooData.columnB` are defined as `BarData.code`.