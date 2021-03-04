# Firebase Builder

This creates a personal image that you can use to run your firebase
This install firebase in the image as well as update the NPM to the latest version via `npm update -g`

This is managed via the `Dockerfile` which creates the image and installs it via the cloudbuild.yaml default file name.

```yaml
steps:
  - name: 'gcr.io/cloud-builders/docker'
    args: ['build', '-t', 'gcr.io/$PROJECT_ID/firebase', '.']
images:
- 'gcr.io/$PROJECT_ID/firebase'
tags: ['cloud-builders-community']
```


# Build your image

To build your image run the following command:

```shell
gcloud builds submit . --project=ENTERPROJECTNAME-ID
```

Once done you can use it in your code as such:

```yaml
steps:
  - name: 'node'
    entrypoint: yarn
    args: [ 'install' ]
  - name: 'node'
    entrypoint: yarn
    args: [ 'generate' ]
  - name: 'gcr.io/$PROJECT_ID/firebase'
    entrypoint: firebase
    args: [ 'deploy', '--project=$PROJECT_ID', '--only=hosting' ]

```
