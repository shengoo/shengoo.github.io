title: "git add -A" 和 "git add ." 的区别
link: http://www.sheng00.com/1841.html
author: admin
description: 
post_id: 1841
created: 2014/12/07 20:33:10
created_gmt: 2014/12/07 12:33:10
comment_status: open
post_name: git-add-difference-between-git-add-a-and-git-add-stack-overflow
status: publish
post_type: post

# "git add -A" 和 "git add ." 的区别

"`git add -A`" 相当于 "`git add .; git add -u`". "`git add .`"虽然看起来像是把目录下所有文件都添加，但是其实并没有，它只会添加新建和更改过的文件。 "`git add -u`" 中-u代表的是`update`，只会记录已有文件的update，不会记录新建的文件。 "`git add -A`" 可以做上面两件事的. 你可以按照下面的命令去测试这些区别: 
    
    
    git init
    echo Change me > change-me
    echo Delete me > delete-me
    git add change-me delete-me
    git commit -m initial
    
    echo OK >> change-me
    rm delete-me
    echo Add me > add-me
    
    git status
    # Changed but not updated:
    #   modified:   change-me
    #   deleted:    delete-me
    # Untracked files:
    #   add-me
    
    git add .
    git status
    
    # Changes to be committed:
    #   new file:   add-me
    #   modified:   change-me
    # Changed but not updated:
    #   deleted:    delete-me
    
    git reset
    
    git add -u
    git status
    
    # Changes to be committed:
    #   modified:   change-me
    #   deleted:    delete-me
    # Untracked files:
    #   add-me
    
    git reset
    
    git add -A
    git status
    
    # Changes to be committed:
    #   new file:   add-me
    #   modified:   change-me
    #   deleted:    delete-me

### 总结:

  * `git add -A`?_添加**所有**_
  * `git add .`?_添加新文件和修改的文件,?**不包括删除的**_
  * `git add -u`?_添加修改和和删除的文件,?**不包括新增的**_