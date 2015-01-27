# Vim Profiling

I recently encountered a situation where Vim was taking an *excruciatingly* long
time to launch. From some manual testing, I was able to isolate the problem to a
particular directory, but I wasn't sure what was causing it. I then discovered
Vim ships with profiling tools that would tell me how much time was spent in
each of the functions that ran during startup.

The following command will launch Vim, enable function profiling, open the
`config/routes.rb` file, and quit, saving the profiling results to `vim.log`.

```sh
vim -c 'profile start vim.log' -c 'profile func *' -c 'e config/routes.rb' -c 'q'
```

The `vim.log` file has a lot of detail about the functions that were executed.
Here's a short one that was near the top for me.

```text
FUNCTION  fugitive#is_git_dir()
Called 18 times
Total time:   0.000396
 Self time:   0.000233

count  total (s)   self (s)
   18   0.000271   0.000108   let path = s:sub(a:path, '[\/]$', '') . '/'
   18              0.000107   return isdirectory(path.'objects') && isdirectory(path.'refs') && getfsize(path.'HEAD') > 10

```

That's interesting, for sure, but the good stuff is at the bottom of the file,
where functions are sorted by execution time. Here's my top offender.

```text
count  total (s)   self (s)  function
    1   2.203751   0.000457  rails#buffer_syntax()
```
