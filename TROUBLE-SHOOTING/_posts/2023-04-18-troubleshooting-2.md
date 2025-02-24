---
layout: post
title: MAK-E-AT TroubleShooting #2
image: /assets/img/blog/err/err-2.png
accent_image: 
  background: url('/assets/img/sidebar/puzzle.jpg') center/cover
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  untracked working tree files 때문에 다른 브랜치로 변경이 안되는 상황 
invert_sidebar: true
---

# [Error] The following untracked working tree files would be overwritten by checkout

* toc
{:toc}


```bash
error: The following untracked working tree files would be overwritten by checkout:
    makeat_fe/ios/Runner.xcodeproj/project.pbxproj
    makeat_fe/ios/Runner.xcodeproj/project.xcworkspace/contents.xcworkspacedata
    makeat_fe/ios/Runner.xcodeproj/project.xcworkspace/xcshareddata/IDEWorkspaceChecks.plist
    makeat_fe/ios/Runner.xcodeproj/project.xcworkspace/xcshareddata/WorkspaceSettings.xcsettings
    makeat_fe/ios/Runner.xcodeproj/xcshareddata/xcschemes/Runner.xcscheme
    makeat_fe/ios/Runner.xcworkspace/contents.xcworkspacedata
    makeat_fe/ios/Runner.xcworkspace/xcshareddata/IDEWorkspaceChecks.plist
    makeat_fe/ios/Runner.xcworkspace/xcshareddata/WorkspaceSettings.xcsettings
Please move or remove them before you switch branches.
Aborting
```

## 상황

다른 브랜치로 checkout하려고 하면, untracked working tree files가 덮어씌워질 것이라며 작업을 수행하지 않는 현상.


## 에러 분석

로컬 내 파일과 동일한 파일이 원격으로 추적되고 있어서, 추적되지 않은 작업 트리 파일이 덮어씌워지는 것을 사전에 방지하는 것으로 보인다.
브랜치를 스위칭하기 전에 추적되지 않은 작업 트리 파일을 옮기거나 제거하는 작업을 수행하도록 안내하고 있다.


## 해결 방법

`git stash`를 통해 추적되지 않은 작업 트리 파일을 임시로 저장하거나 `git clean`을 통해 제거한다.
나의 경우, 추적되지 않은 파일을 삭제해도 무방한 상황이었기 때문에 제거를 통해 문제를 해결했다.

- `git clean -d -f`
    
    현재 디렉토리에서 추적되지 않는 파일과 디렉터리를 모두 삭제한다.

`git clean` 명령어를 실행하기 전에는 삭제할 파일들이나 디렉터리들을 다시 한번 확인하고 실행하는 것을 권장한다.


### 만약 위 방법으로도 해결이 되지 않는다면...

- `git fetch --all`
    
    원격 저장소의 모든 브랜치의 최신 변경 내용을 가져온다.

- `git reset --hard {remote_name}/{branch_name}`
    
    로컬 브랜치를 원격 저장소의 {branch_name} 브랜치의 상태로 변경한다.
    이때, 로컬 브랜치의 모든 변경 내용을 삭제하고 원격 저장소의 최신 버전으로 덮어쓴다는 것에 주의해야 한다.

- `git pull {remote_name}/{branch_name}`
    
    (만약 로컬 브랜치와 원격 저장소의 {branch_name} 브랜치 간에 차이가 있는 경우) 원격 저장소의 {branch_name} 브랜치에서 로컬 브랜치로 최신 변경 내용을 병합한다.
    
로컬 브랜치에 작업한 내용이 있다면, 위 명령어를 실행하기 전에 작업한 내용을 백업하거나 `stash`를 사용하여 임시로 저장해두어야 합니다!
    

## 기타 참고 링크
[stackoverflow - The following untracked working tree files would be overwritten by merge, but I don't care](https://stackoverflow.com/questions/17404316/the-following-untracked-working-tree-files-would-be-overwritten-by-merge-but-i)

[git clean 매뉴얼 페이지](https://mirrors.edge.kernel.org/pub/software/scm/git/docs/git-clean.html)
