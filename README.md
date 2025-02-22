# holle
测试项目
name: push

on:
  workflow_dispatch:
  push:
    branches:
      - main
  schedule:
    - cron: "* * * * *"

jobs:
  build:
    runs-on: ubuntu-latest
    
    permissions:
      contents: write
 
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0
 
    - name: Make changes
      run: |
        echo "Some changes" >> changes.txt
        date > time
        date
        echo 1 > 1
 
    - name: Commit changes
      uses: stefanzweifel/git-auto-commit-action@v5
