# Authentication failed

## Issus

I can't push any source to remote git respository.

## error message

```text
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: Authentication failed for '{my git repository url}'
```

## Why i get this error

Why is you use password based authentication.<br>
Git changed git's authentication policy in favor of more secure before.<br>
That is If you use cloning with https urls, you can't use password based authentication from now.<br>
So you must deal with that policy change.<br>
Specifically, you should use authenctication other than password based authentication, for instance personal accessToken, Git Credential Manager and so on.<br>

if you would like to see more detail, you can see it on following link<br>
https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls

## Solution

If you would like to use personal token to solve this issus.<br>
You shold see a document on following link.<br>
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token
<br>

If you would like to use Git Credential Manager, you should see a document on following link.<br>
https://github.com/git-ecosystem/git-credential-manager/blob/main/README.md





