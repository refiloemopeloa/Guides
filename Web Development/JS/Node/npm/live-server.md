# Live Server

## Install Live Server

In your project directory, type the following:

```shell
npm install live-server
```

This will install Live Server as a module in your directory. Then, to run your project, simply type:

```shell
npx live-server
```

You can also add it to your `package.json` file and use `npm run start` to run it:

```json
"scripts": {  
  "start": "live-server"  
}
```

Now, whenever you save, your changes will automatically update.

## Change server attributes

You can change the server attributes by typing the following in the terminal with the `live-server` command:

| command                | usage                                                                                          |
| ---------------------- | ---------------------------------------------------------------------------------------------- |
| `--port=NUMBER`        | select port to use, default: PORT env var or 8080                                              |
| `--host=ADDRESS`       | select host address to bind to, default: IP env var or 0.0.0.0 ("any address")                 |
| `--no-browser`         | suppress automatic web browser launching                                                       |
| `--browser=BROWSER`    | specify browser to use instead of system default                                               |
| `--quiet`              | suppress logging                                                                               |
| `--open=PATH`          | launch browser to PATH instead of server root                                                  |
| `--watch=PATH`         | comma-separated string of paths to exclusively watch for changes (default: watch everything)   |
| `--ignore=PATH`        | comma-separated string of paths to ignore                                                      |
| `--ignorePattern=RGXP` | Regular expression of files to ignore (ie `.*\.jade`)                                          |
| `--entry-file=PATH`    | serve this file in place of missing files (useful for single page apps)                        |
| `--mount=ROUTE:PATH`   | serve the paths contents under the defined route (multiple definitions possible)               |
| `--spa`                | translate requests from /abc to /#/abc (handy for Single Page Apps)                            |
| `--wait=MILLISECONDS`  | wait for all changes, before reloading                                                         |
| `--htpasswd=PATH`      | Enables http-auth expecting htpasswd file located at PATH                                      |
| `--cors`               | Enables CORS for any origin (reflects request origin, requests with credentials are supported) |
| `--https=PATH`         | PATH to a HTTPS configuration module                                                           |
| `--proxy=ROUTE:URL`    | proxy all requests for ROUTE to URL                                                            |
| `--help \| -h`         | display terse usage hint and exit                                                              |
| `--version \| -v`      | display version and exit                                                                       |
These commands can also be added to your `package.json` file.