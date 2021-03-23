구글 apiKey를 잘못 올리는 실수를 저질렀을 때 사용할 수 있는 방법이다.

### 1. **파일 삭제**

```bash
git rm --cached [파일명]
git rm --cached -r [폴더명]
```

- **--cached**

원격저장소의 폴더 또는 파일을 삭제한다고 알려주는 옵션. 만약 —cached가 없으면 로컬저장소의 폴더 또는 파일도 삭제한다.

- -r

폴더명이 주어졌을 때 recursive removal을 허용하게 해주는 옵션.

### **2. git history 전체에서 특정 file 관련 히스토리 삭제**

```bash
git filter-branch -f --index-filter "git rm --cached --ignore-unmatch '[경로/파일명]'" --prune-empty -- --all
```
- **git filter-branch**

브랜치를 재작성하는 명령어. 필터를 제공해서 필터에 적용된 파일만 가지고 히스토리를 다시 구축한다. 이 기능을 이용해 특정 파일에 대한 history와 해당 파일을 지운다.

- 결과

```bash
Ref 'refs/heads/main' was rewritten
Ref 'refs/remotes/origin/main' was rewritten
WARNING: Ref 'refs/remotes/origin/main' is unchanged
```

- push

```bash
git push origin main --force --all
```
