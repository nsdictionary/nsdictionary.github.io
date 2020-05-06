---
layout: default
title: Rails
---

# {{page.title}}

Switch DB bash script
---------
여러 개발자와 하나의 레일즈 프로젝트로 협업을 할경우 브랜치가 바뀔때
디비 스키마도 같이 바뀌는 경우가 많은데, 스키마 컨플릭으로 에러가 발생할수 있다.
그때 사용하려고 임시로 스크립트를 만들었었는데 좀더 보강이 필요할듯 하다.


```bash
#!/bin/bash

RAILS_DB_DIR="/Users/sam/Dropbox/rails_dbs"
RAILS_ROOT="/Users/sam/Workspace/sentbe-rails-restful"
RAILS_TMP_DIR="$RAILS_ROOT/tmp"

[ $# -eq 0 ] && { echo "Usage: $0 dir-name"; exit 1; }

TARGET_DIR="$RAILS_DB_DIR/$1"

if [ ! -d "$TARGET_DIR" ]
then
  echo "Error: Directory(branch name) $1 does not exists."
    exit
fi

if [ -d "$RAILS_TMP_DIR" ]
then
	docker stop mysql && docker rm mysql
	docker stop postgres && docker rm postgres

	rm -rf $RAILS_TMP_DIR/mysql
	rm -rf $RAILS_TMP_DIR/postgres
	ln -s $TARGET_DIR/mysql $RAILS_TMP_DIR/mysql
	ln -s $TARGET_DIR/postgres $RAILS_TMP_DIR/postgres

	docker-compose -f $RAILS_ROOT/docker-compose.yml up -d mysql
	docker-compose -f $RAILS_ROOT/docker-compose.yml up -d postgres

  echo "Success switch rails db on $1"
else
    echo "Error: rails directory does not exists."
fi
```

Section 2
---------

[...]
