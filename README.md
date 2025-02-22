appHooks.put("com.example.app", new HookInfo[]{
                new HookInfo("com.example.ClassName", new String[]{"methodName"}, 0),
                new HookInfo("com.example.ClassName", new String[]{"methodName"}, null),
                new HookInfo("com.example.ClassName", new String[]{"methodName"}, false),
                new HookInfo("com.example.ClassName", new String[]{"method1", "method2"}, null)# holle
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
