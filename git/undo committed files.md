#git #commit #undo
1. How to undo committed files?
```bash
Source: https://gist.github.com/rcanepa/8a334d7c4f46df948c676aab489fe2c2 (Author: Renzo Canepa https://gist.github.com/rcanepa)

- Reset current branch to the parent of HEAD  
git reset --soft HEAD~

- Reset the unwanted files in order to leave them out from the commit:
git reset HEAD path/to/unwanted_file

- Commit again using the same commit message:
git commit -c ORIG_HEAD  

(*) git reset --soft HEAD~ 
    The last commit will be undone and the files touched will be back on the stage again. Also,
    index and staging remains untouched.
    
(*) git reset HEAD -- file
    Moves file from stage to the working directory (unstage a file).
     
(*) git reset --hard 
    Unstage files AND undo any changes in the working directory since last commit
    
```