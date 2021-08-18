# How to prepare the spec file

We should have a single file named `openapi.json` placed here.
If we have multiple files in different formats (ex: `yaml` / `json` mixed) with `$ref` we should merge them into one file to exclude any issues when it will be accessed.

to do that we should use `swagger-merger` like that:

```bash
❯ npx swagger-merger -i openapi.yaml -o openapi.json
```

then, to make sure file is valid and have no parsing issues:

```bash
❯ npx jsonlint ./openapi.json -q
```

It will output nothing if there is no issues and will throw an issues if there will be one.