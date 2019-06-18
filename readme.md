# GitHub Tricks

## README Symlinks

When in a particular folder (such as the root directory), GitHub displays content from README files underneath the files in that folder:

<img src="github-readme.png" alt="Screenshot showing readme content below file list">

However, these README files need to be named `README.md`, `readme.md`, `README.mdx` or `readme.mdx` in order to be recognized. GitHub doesn't display the content of certain common Markdown index filenames such as `index.md` or `index.mdx` ([❓MDX file extension](https://github.com/mdx-js/mdx)) ([as of 18 June 2019](https://twitter.com/karlhorky/status/1140962752858677249)).

GitHub does however follow symlinks named `README.md`, `readme.md`, `README.mdx` and `readme.mdx`.

So if you want to use another file (also in a subdirectory) as the contents displayed within a directory, create a symlink pointing at it:

```sh
ln -s index.md README.md
```

### Shell Script: Create README Symlinks

If you have many directories with `index.mdx` files that you want to display as the readme content when you enter those directories on the web version of GitHub, you can run this script in the containing directory.

```sh
# Create symlinks for all directories within the current directory that
# do not yet have README.mdx files.
find . -mindepth 1 -maxdepth 1 -type d '!' -exec test -e "{}/README.mdx" ';' -print0 | while IFS= read -r -d $'\0' line; do
    cd $line && ln -s index.mdx README.mdx && cd ..
done
```
