# Merging two repos


[Source](https://www.youtube.com/watch?v=2JqWvl3HFfQ)

Thank you for the helpful guide/tutorial. I couldn't remember all those commands. So I think it would be useful to sum it up for others here again:          
1.)  git remote add <RemoteName> <RemoteURL>       
2.) git fetch <RemoteName>       
3.) check to see whether remote is available with git remote -v       4.) Create a new branch with git checkout -b <NewBranchName> <Branch/master>     
5.) move all the files into a subdirectory so there aren't any conflicts with names (git mv)  and commit that (git commit -m "moved")     
 6.) git checkout master   
 7.) git merge <NewBranchName> --allow-unrelated-histories     7.) cleanup everything with: git remote rm <RemoteName>      git branch -d <NewBranchName>   
 8.) check to see whether everything is correct with: git remote -v     git branch -a -v     git status   
 9.) git push
 
 
 One more Guide [Link](https://thoughts.t37.net/merging-2-different-git-repositories-without-losing-your-history-de7a06bba804)