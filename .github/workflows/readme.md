NPM BUILD
```yml
on: 
  push:
  workflow_dispatch:
jobs:
  call-npm-build:
    uses: multipleof4/.github/.github/workflows/npm-build.yml@master
    permissions:
      contents: write
```
```yml
on:
  workflow_dispatch:
    inputs:
      name:
        required: true
jobs:
  gen:
    uses: multipleof4/.github/.github/workflows/gen-keystore.yml@master
    with:
      name: ${{ github.event.inputs.name }}
    secrets:
      KEYSTORE_PASS: ${{ secrets.KEYSTORE_PASS }}
      KEY_PASS: ${{ secrets.KEY_PASS }}
```
```yml
on:
  workflow_dispatch:
    inputs:
      unsigned_apk:
        required: false
        default: sune-1500-unsigned.apk
jobs:
  call:
    uses: multipleof4/.github/.github/workflows/sign-apk.yml@master
    with:
      unsigned_apk: ${{ github.event.inputs.unsigned_apk }}
    secrets:
      KEY_ALIAS: ${{ secrets.KEY_ALIAS }}
      KEYSTORE_PASS: ${{ secrets.KEYSTORE_PASS }}
      KEY_PASS: ${{ secrets.KEY_PASS }}
      JKS_BASE64: ${{ secrets.JKS_BASE64 }}
```
```yml
on:
  workflow_dispatch:
    inputs:
      repo:
        required: true
        type: string
permissions:
  contents: write
jobs:
  mirror:
    uses: multipleof4/.github/.github/workflows/repo-mirror.yml@master
    with:
      repo: ${{ inputs.repo }}
```
