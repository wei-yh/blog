+++
title = "doom emacs 配置 ox-hugo"
date = 2023-02-08T17:52:00+08:00
draft = false
author = "Zhao Wei"
+++

## enable ox-hugo: edit .doom.d/init.el {#enable-ox-hugo-edit-dot-doom-dot-d-init-dot-el}

```lisp
(org +hugo)
```


## 配置 ox-hugo: edit .doom.d/config.el {#配置-ox-hugo-edit-dot-doom-dot-d-config-dot-el}

请参考[ox-huog 官方教程](https://ox-hugo.scripter.co/)

-   hugo 可以将一个 org 文件的每个 subtree 作为一篇 post， 也可以将每一个独立的 org 文件做为一篇 post。
-   下面配置的是 all_posts.org 里将 subtree 作为一篇 post 发布。

<!--listend-->

```lisp
;; 设置org的工作目录
(setq org-directory "~/org/")

;; 设置org-capture
(with-eval-after-load 'org-capture
  (defun org-hugo-new-subtree-post-capture-template ()
    "Returns `org-capture' template string for new Hugo post.
See `org-capture-templates' for more information."
    (let* ((title (read-from-minibuffer "Post Title: ")) ;Prompt to enter the post title
           (date (format-time-string (org-time-stamp-format :long :inactive) (org-current-time)))
           (fname (org-hugo-slug title)))
      (mapconcat #'identity
                 `(
                   ,(concat "* TODO " title)
                   ":PROPERTIES:"
                   ,(concat ":EXPORT_FILE_NAME: " fname)
                   ,(concat ":EXPORT_DATE: " date) ;Enter current date and time
                   ":END:"
                   "%?\n")          ;Place the cursor here finally
                 "\n")))

  (add-to-list 'org-capture-templates
               '("h"                ;`org-capture' binding + h
                 "Hugo post"
                 entry
                 ;; It is assumed that below file is present in `org-directory'
                 ;; and that it has a "Blog Ideas" heading. It can even be a
                 ;; symlink pointing to the actual location of all-posts.org!
                 ;; 需要提前在org目录下建立all-posts.org, 并输入Blog Ideas做为第一级的header并保存
                 (file+olp "all-posts.org" "Blog Ideas")
                 (function org-hugo-new-subtree-post-capture-template))))
```


## 配置 all-posts.org {#配置-all-posts-dot-org}

hugo_base_dir ： 你的 blog 的根文件目录在哪
hugo_section: 你再 xxx.md 文件放在 content/目录下的位置。比如我的 xxx.md 文件就放在 content/posts/目录下。所以我的 hugo_section 就是 posts

```org
#+hugo_base_dir: ~/blog
#+hugo_section: posts
#+author:
#+hugo_custom_front_matter: :author "Zhao Wei"
 * Blog Ideas
```

**\***


## creat a new hugo org capture {#creat-a-new-hugo-org-capture}

1.  org-capture

    {{< figure src="/ox-hugo/2023-02-08_20-52-59_Snipaste_2023-02-08_20-50-43.jpg" >}}

2.  选择 hugo

    {{< figure src="/ox-hugo/2023-02-08_20-53-10_Snipaste_2023-02-08_20-52-43.jpg" >}}

3.  write some thing and

    {{< figure src="/ox-hugo/2023-02-08_20-58-28_Snipaste_2023-02-08_20-57-33.jpg" >}}


## export to md file {#export-to-md-file}

1.  change the "todo" tag to "done"(will set the draft to false), 这样才能看见在网页上看见这篇文章。

    {{< figure src="/ox-hugo/2023-02-08_21-01-35_Snipaste_2023-02-08_21-01-19.jpg" >}}

2.  export

    {{< figure src="/ox-hugo/2023-02-08_21-02-46_Snipaste_2023-02-08_21-02-24.jpg" >}}

    the hi.md has been export to the hugo conent/posts/

{{< figure src="/ox-hugo/2023-02-08_21-03-59_Snipaste_2023-02-08_21-03-49.jpg" >}}
