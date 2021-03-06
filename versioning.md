## No Versioning

You can use without versioning - just using the default *latest* set of resources. For smaller projects with continues deployment or no deployment process at all this can be a suitable solution.

## "Rolling" Versioning

Most bigger projects will do a versioning divided into stages like:

<div class="center" style="margin-top: 40px; margin-bottom: 40px;">
<div class="pricing" style="text-transform: none">
development (latest) &rarr; staging &rarr; production
</div>
</div>

Everytime you want to deploy to next stage you can copy the resources eg. from *latest* to *staging* by creating a new version (and retype staging for new version name).



## Semantic Versioning

Semantic Versioning can be useful if you deploy an application in different versions and you got no control over the users upgrading (eg. iOS Applications,…).

<div class="center" style="margin-top: 40px; margin-bottom: 40px;">
<div class="pricing" style="text-transform: none">
1.0.0 &rarr; patch (bugfix) &rarr; 1.0.1 <br />
1.0.1 &rarr; minor (feature) &rarr; 1.1.0 <br />
1.1.0 &rarr; major (breaking) &rarr; 2.0.0
</div>
</div>

When deploying - just create a new version based on your lastest version and update your production code to use that new version.

<div class="center" style="margin-top: 40px; margin-bottom: 40px;">
<div class="pricing" style="text-transform: none">
<strong>development</strong> &rarr; use <strong>latest</strong> <br />
published <strong>1.0.0</strong> &rarr; use <strong>1.0.0</strong> <br />
published <strong>1.1.0</strong> &rarr; use <strong>1.1.0</strong> <br />
published <strong>1.1.1</strong> &rarr; keep using <strong>1.1.0</strong> if no changes <br />
</div>
</div>

Most time you won't need to create a new version when doing bugfix.

## Update your code

Update your locizify script to include targeted version:

```html
<script id="locizify" version="staging" ...
  src="https://unpkg.com/locizify@^2.0.0" />
```

Update i18next with locize backend:

```js
i18next.init({
  // ...
  backend: {
    referenceLng: '{{referenceLanguage}}',
    apiKey: '{{apiKey}}',
    version: 'staging',
    projectId: '{{project_Id}}'
  }
});
```