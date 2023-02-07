# SETUP
- [install hugo](https://gohugo.io/installation/)
- clone env
    ``` shell
    git clone https://github.com/wei-yh/blog.git blog/
    cd blog/
    git submodule update --init
    git clone https://github.com/wei-yh/wei-yh.github.io.git public
    ```
- clone public
    ``` shell 
    git clone https://github.com/wei-yh/wei-yh.github.io.git public
    ```
# write a new post
` hugo new posts/xxxx.md `

# public post
    ``` shell
    hugo -D
    cd public/
    git add .
    git commit
    git push
    ```
