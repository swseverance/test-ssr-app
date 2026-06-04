# Demonstration that upgrading @angular/ssr and @angular/core does not fix Firebase App Hosting issue

This project was generated with the following command:
```
npx @angular/cli@21 new test-ssr-app --ssr=true --style=css --ai-config=none
```

The installed dependencies are the latest available versions (v21 at least) of @angular/core and @angular/ssr:
```
@angular/core@21.2.16
@angular/ssr@21.2.14
```

Setup the Firebase App Hosting configuration via:
```
firebase init apphosting --project=ghreactionsdev
```

Use the Firebase UI to connect to GitHub and point to the main branch, using "/" as the root directory.

After visiting https://test-ssr-app--ghreactionsdev.us-east4.hosted.app you will see the following:
```
Header "host" with value "t-25955752---test-ssr-app-5wu2geqsna-uk.a.run.app" is not allowed.
```

In my opinion the stated workaround should be one of the two following options:

## Option 1

Add the following at the top of src/server.ts:
```
delete process.env['NG_TRUST_PROXY_HEADERS'];
delete process.env['NG_ALLOWED_HOSTS']
```
Then the environment variables no longer override the configuration the user attempted to provide

## Option 2

Encourage users to override NG_TRUST_PROXY_HEADERS and NG_ALLOWED_HOSTS in their apphosting.yaml files