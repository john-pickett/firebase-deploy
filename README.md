## Note: I have not used or updated this package in several months, and it may be broken. 

# Deploy to Firebase

A GitHub Action to deploy to Firebase Hosting

- This action only deploys the `master` branch
- Make sure you have the `firebase.json` file in the repository
- Get the Firebase token by running `firebase login:ci` and [store it](https://help.github.com/en/articles/virtual-environments-for-github-actions#creating-and-using-secrets-encrypted-variables) as the `FIREBASE_TOKEN` secret
- Set the project name in the `FIREBASE_PROJECT` env var

Example workflow

```
name: Build and Deploy
on:
  push:
    branches:
    - master
jobs:
  main:
    name: Build and Deploy
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@master
    - name: Build Hugo
      uses: lowply/build-hugo@v0.0.2
    - name: Deploy to Firebase Hosting
      uses: john-pickett/firebase-deploy
      env:
        FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
        FIREBASE_PROJECT: name-of-the-project
```

## Notes

This repo is taken from [Deploy to Firebase](https://github.com/lowply/deploy-firebase) by [Lowply](https://github.com/lowply) with only some minor edits. His repo works great, but I needed to be able to deploy to Firebase from other branches than `master`. Thanks to Lowply for the original repo.
