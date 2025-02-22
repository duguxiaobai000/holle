GIF、JPEG、JPG、MOV、MP4、PNG、SVG或WEBM预演
此文件为空。缩进模式
GIF、JPEG、JPG、MOV、MP4、PNG、SVG或 WEBM
此文件为空。缩进模式
再试一次空
使用一个不空的文件。制表符
这个文件是隐藏的。缩进尺寸

on:
  workflow_dispatch:
  push:
    branches:
再试一次换行模式
  schedule:
另一份文件。无包裹

jobs:
  build:
另一份文件。无包裹
    
query为空
query为空
 
query为空
query为空
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
