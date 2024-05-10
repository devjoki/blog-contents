![post_logo](../images/git_hook.jpg)
# Maximizing Productivity
## The power of the Prepare Commit Message hook

Working in teams sometimes requires the use of git feature branches, and this usually involves some additional processes.<br/>
The most common one is that the task ID needs to be included in the git branch name so that it can be tracked more easily.
If this is the case, it is also useful to include the task id in the commit message, to improve this tracking even further.<br/>
The exact process may vary from team to team; sometimes this is just an agreement between developers, or sometimes the rule is even enforced by a server-side hook, but what all these processes have in common is that doing all the steps manually is frustrating and error-prone.<br/>
So what can you do to make it more efficient?<br/>
Well, the same thing you would do with any repetitive manual task: `automate it`. How? simply by adding a simple git prepare commit message hook:<br/>
```
  #!/bin/bash
  project_name="<project-name>"
  message_file="$1"	
  # sha1 is empty in case of amend
  sha1="$3"
  branch_name=$(git branch --show-current)
  ticket_number=$(echo "$branch_name" | grep -oE "$project_name-[0-9]{1,7}")

  if [[ -n "$ticket_number" && -z "$sha1" ]]; then
          sed -i.bup "1s/^/$ticket_number - /" "$message_file"
  fi
```
Lets see what happens in the script (straitforward things are omitted):
* getting the ticket number from branch name with grep
  * **-o(--only-matching)** "print  only  the  matched  (non-empty)  parts of a matching line, with each such part on a separate output line"
  * **-E(--extended-regexp)** "interpret  patterns  as extended regular expressions"
* conditional execution 
  * if the ticket number is present in the branch name
    * the hook should not fail on non-feature branches
  * if the commit for which the message is being prepared is a new commit
    * this can be determined by the presence of the commit hash
* modifying the message with sed
  * **-i(--in-place)** "this option specifies that files are to be edited in-place. gnu sed does this by creating a temporary file and sending output to this file rather than to the standard output"
    * here, a temp fill will be suffixed with 'bup'
  * the script:
    * **1** - specifies the line number, **s** - the substitution command for sed
    * **^** - regex to match the start of the line
    * The next section is the text to insert

This is good, but how does it apply to every single repository? having to add it manually is not efficient at all...<br/>
Well, by using a global git config, it can be set up once for all repositories:<br/>
```
 git config --global core.hooksPath "/path/to/hooks"
```
The above command sets the given path as the global git hook directory, so any hooks in it will be applied to every single repository.<br/><br/>
Of course, you could argue that merging pull requests will clean up the commit history, so this whole thing is unnecessary... or that it's a stupid rule anyway... but sometimes it's easier to adapt and make these annoying things easy to deal with than it is to keep fighting them.<br/><br/>
Thanks for reading, I hope you learned something.<br/>
See you next time.


