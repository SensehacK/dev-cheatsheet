
## CLI 

Checking a Local Clone

If you have a local copy of the repository, you can use Git commands to determine its size accurately. 

- Open a terminal and navigate to your local repository directory.

Run the command

```sh
git count-objects -vH
```


Look for the `size-pack` entry in the output, which provides the size of all packed commit objects in a human-readable format (e.g., MiB). This is generally the most reliable representation of the repository's size on the remote. 

Tools and Extensions

Third-party tools and browser extensions can also help: 

- **Browser Extensions**: Extensions like "GitHub Repository Size" display the size directly in the GitHub interface.
- **`git-sizer`**: This open-source command-line tool analyzes your local repository and reports on various size metrics, which is useful for identifying large files or objects that might be causing bloat.
  
  
```